```
{secondary:node0}[edit]
root@SRX3400-1# edit interfaces ge-0/0/1 unit 0 family bridge

{secondary:node0}[edit interfaces ge-0/0/1 unit 0 family bridge]
root@SRX3400-1# set interface-mode access vlan-id 10

{secondary:node0}[edit interfaces ge-0/0/1 unit 0 family bridge]
root@SRX3400-1# up 3

{secondary:node0}[edit interfaces]
root@SRX3400-1# edit ge-0/0/2 unit 0 family bridge

{secondary:node0}[edit interfaces ge-0/0/2 unit 0 family bridge]
root@SRX3400-1# set interface-mode access vlan-id 20

{secondary:node0}[edit interfaces ge-0/0/2 unit 0 family bridge]
root@SRX3400-1# up 4

{secondary:node0}[edit]
root@SRX3400-1# set bridge-domains L2-VLAN-10 domain-type bridge vlan-id 10

{secondary:node0}[edit]
root@SRX3400-1# set bridge-domains L2-VLAN-20 domain-type bridge vlan-id 20

{secondary:node0}[edit]
root@SRX3400-1# commit and-quit
warning: Interfaces are changed from route mode to transparent mode. Please
reboot the device or all nodes in the HA cluster!
node0:
configuration check succeeds
node1:
warning: Interfaces are changed from route mode to transparent mode. Please
reboot the device or all nodes in the HA cluster!
commit complete
node0:
commit complete

{primary:node0}
root@SRX3400-1> request system reboot
```
```
{primary:node0}[edit security zones]
root@SRX3400-1# edit security-zone untrust

{primary:node0}[edit security zones security-zone untrust]
root@SRX3400-1# set interfaces ge-0/0/2.0

{primary:node0}[edit security zones security-zone untrust]
root@SRX3400-1# set host-inbound-traffic system-services ping
```
```
{primary:node0}[edit security zones]
root@SRX3400-1# edit security-zone trust

{primary:node0}[edit security zones security-zone trust]
root@SRX3400-1# set interfaces ge-0/0/1.0

{primary:node0}[edit security zones security-zone trust]
root@SRX3400-1# set host-inbound-traffic system-services ping ssh
```
### Example Firewall Config (ours will be different)
```
root@SRX3400-1# set security address-book address 172.31.20.0/24 172.31.20.0/24

{primary:node0}[edit]
root@SRX3400-1# set security address-book address 172.31.40.0/24 172.31.40.0/24

{primary:node0}[edit]
root@SRX3400-1# set security address-book address 172.31.60.0/24 172.31.60.0/24

{primary:node0}[edit]
root@SRX3400-1# set security address-book address 172.31.10.0/24 172.31.10.0/24

{primary:node0}[edit]
root@SRX3400-1# set security address-book address 172.31.30.0/24 172.31.30.0/24

{primary:node0}[edit]
root@SRX3400-1# set security address-book address 172.31.50.0/24 172.31.50.0/24

{primary:node0}[edit]
root@SRX3400-1# show security zones
security-zone untrust {
    host-inbound-traffic {
        system-services {
            ping;
        }
    }
    interfaces {
        ge-0/0/2.0;
        ge-0/0/3.10;
        ge-0/0/3.30;
        ge-0/0/4.50;
    }
}
security-zone trust {
    host-inbound-traffic {
        system-services {
            ping;
            ssh;
        }
        protocols {
            all;
        }
    }
    interfaces {
        ge-0/0/1.0;
        ge-0/0/3.40;
        ge-0/0/4.20;
        ge-0/0/4.60;
    }
}


{primary:node0}[edit]
root@SRX3400-1# edit security policies from-zone trust to-zone untrust policyAllow-Traffic

{primary:node0}[edit security policies from-zone trust to-zone untrust policy
Allow-Traffic]
root@SRX3400-1# set match source-address [ 172.31.20.0/24 172.31.40.0/24172.31.60.0/24 ]

{primary:node0}[edit security policies from-zone trust to-zone untrust policy
Allow-Traffic]
root@SRX3400-1# set match destination-address [ 172.31.10.0/24 172.31.30.0/24172.31.50.0/24 ]

{primary:node0}[edit security policies from-zone trust to-zone untrust policy
Allow-Traffic]
root@SRX3400-1# set match application [ junos-http junos-https junos-smtpjunos-ftp ]

{primary:node0}[edit security policies from-zone trust to-zone untrust policy
Allow-Traffic]
root@SRX3400-1# set then permit

{primary:node0}[edit security policies from-zone trust to-zone untrust policy
Allow-Traffic]
root@SRX3400-1# set then log session-close

{primary:node0}[edit security policies from-zone trust to-zone untrust policy
Allow-Traffic]
root@SRX3400-1# up 2

{primary:node0}[edit security policies]
root@SRX3400-1# edit from-zone untrust to-zone trust policy Allow-Inbound

{primary:node0}[edit security policies from-zone untrust to-zone trust policy
Allow-Inbound]
root@SRX3400-1# set match source-address [ 172.31.10.0/24 172.31.30.0/24172.31.50.0/24 ]

{primary:node0}[edit security policies from-zone untrust to-zone trust policy
Allow-Inbound]
root@SRX3400-1# set match destination-address [ 172.31.20.0/24 172.31.40.0/24172.31.60.0/24 ]

{primary:node0}[edit security policies from-zone untrust to-zone trust policy
Allow-Inbound]
root@SRX3400-1# set match application [ junos-dns-udp junos-ping ]

{primary:node0}[edit security policies from-zone untrust to-zone trust policy
Allow-Inbound]
root@SRX3400-1# set then permit

{primary:node0}[edit security policies from-zone untrust to-zone trust policy
Allow-Inbound]
root@SRX3400-1# set then log session-close

{primary:node0}[edit security policies from-zone untrust to-zone trust policy
Allow-Inbound]
root@SRX3400-1# up 2

{primary:node0}[edit security policies]
root@SRX3400-1# set default-policy deny-all


{primary:node0}[edit security policies]
root@SRX3400-1# show
from-zone trust to-zone untrust {
    policy Allow-Traffic {
        match {
            source-address [ 172.31.20.0/24 172.31.40.0/24 172.31.60.0/24 ];
            destination-address [ 172.31.10.0/24 172.31.30.0/24 172.31.50.0/24 ];
            application [ junos-http junos-https junos-smtp junos-ftp ];
        }
        then {
            permit;
            log {
                session-close;
            }
        }
    }
}
from-zone untrust to-zone trust {
    policy Allow-Inbound {
        match {
            source-address [ 172.31.10.0/24 172.31.30.0/24 172.31.50.0/24 ];
            destination-address [ 172.31.20.0/24 172.31.40.0/24 172.31.60.0/24 ];
            application [ junos-dns-udp junos-ping ];
        }
        then {
            permit;
            log {
                session-close;
            }
        }
    }
}
default-policy {
    deny-all;
}
```