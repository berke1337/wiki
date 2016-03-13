# JunOS

## Intro

**JunOS** is the operating system that runs on ''Juniper Networks'' equipment.
It is a FreeBSD derivative.

## Command-line interface

If you login as `root`, you get a `csh`. The JunOS configuration shell is
`/usr/sbin/cli`. All the documentation you will find online uses this shell.

### Basic operations

http://www.juniper.net/techpubs/software/junos/

Normally, you'll get a prompt like this:
```
root@VJX0>
```
You can view the configuration with `show configuration`. As you will see, the
configuration is hierarchical, and curly braces are used to separate levels.

You can go into configuration mode:
```
root@VJX0> edit
Entering configuration mode

[edit]
root@VJX0#
```
Once in configuration mode, use `set` to configure things, or use `delete` to
unconfigure things. There is good tab-completion, or you can also type `?` to
get a list of options. You can use `edit` again to limit your scope (e.g.
  `edit system services`), and you can then use `up` to broaden your scope again
  (also `up [number]`). Use `show` to show the current configuration in the
  current scope.

Once you're done editing you can do any of the following:
```
exit              remember changes but don't use them
show | compare    show changes w.r.t. live configuration
commit check      check configuration for errors
commit            save changes and apply to live configuration
rollback          undo all uncommitted changes
```

## Transparent firewalling

Following is a template configuration for transparent firewalling on SRX or J
devices. Note that the built-in DHCP server does not work in transparent mode!
You need to reboot if you change the router from route to transparent mode or
vice-versa.

This configuration just shows a simple in-line transparent firewall. You could
do more advanced things such as use the integrated bridging/switching for
Bastion-like setups.

```
system {
    time-zone America/Los_Angeles;
    root-authentication;
    name-server {
        [DNS-IP];
    }
    services {
        ssh;
    }
}
interfaces {
    fe-0/0/0 {
        unit 0 {
            family bridge {
                interface-mode access;
                vlan-id 1;
            }
        }
    }
    fe-0/0/1 {
        unit 0 {
            family bridge {
                interface-mode access;
                vlan-id 1;
            }                           
        }
    }
    # etc...
    irb {
        unit 0 {
            family inet {
                address [ACCESS-IP]/8;
            }
        }
    }
}
security {
    policies {
    	# Policies MUST BE setup, default is block.
        default-policy {
            deny-all;
        }
    }
    zones {
        security-zone local {
            host-inbound-traffic {
                system-services {
                    ssh;
                    ping;
                }
            }
            interfaces {
                fe-0/0/1.0;
                # etc...
            }
        }
        security-zone outside {
            interfaces {
                fe-0/0/0.0;
            }
        }
    }
}
bridge-domains {
    bd1 {
        domain-type bridge;
        vlan-id 1;
        routing-interface irb.0;
    }
}
```

Below are some example security policies you could use. Capirca also supports
JunOS.

```
# Example policies
security {
    policies {
        from-zone outside to-zone local {
            policy inbound-icmp {
                match {
                    source-address any;
                    destination-address any;
                    application junos-icmp-all;
                }
                then {
                    permit;
                }
            }
        }
        from-zone local to-zone outside {
            policy outbound-icmp {
                match {
                    source-address any;
                    destination-address any;
                    application junos-icmp-all;
                }
                then {
                    permit;
                }
            }                           
            policy outbound-ssh {
                match {
                    source-address any;
                    destination-address any;
                    application junos-ssh;
                }
                then {
                    permit;
                }
            }
        }
        from-zone local to-zone local {
            policy local2local-traffic {
                match {
                    source-address any;
                    destination-address any;
                    application any;
                }
                then {
                    permit;
                }
            }
        }
    }
}
```

## Switching

All ports on separate VLANs with a trunk port, management IP is native on trunk
port. On SRX:

```
system {
    time-zone America/Los_Angeles;
    root-authentication;
    name-server {
        [DNS-IP];
    }
    services {
        ssh;
    }
}
interfaces {
    fe-0/0/0 {
        unit 0;
    }
    fe-0/0/1 {
        unit 0 {
            family ethernet-switching {
                vlan {
                    members 1;
                }
            }
        }
    }
    fe-0/0/2 {                          
        unit 0 {
            family ethernet-switching {
                vlan {
                    members 2;
                }
            }
        }
    }
    fe-0/0/7 {
        unit 0 {
            family ethernet-switching {
                port-mode trunk;
                vlan {
                    members all;
                }
                native-vlan-id 100;
            }
        }
    }
    vlan {
        unit 0 {
            family inet {
                address [ACCESS-IP]/8;
            }
        }
    }
}
security {
    zones {
        security-zone management {
            host-inbound-traffic {
                system-services {
                    ssh;
                    ping;
                }
            }
            interfaces {
                vlan.0;
            }
        }
    }
}
vlans {
    v100 {
        vlan-id 100;
        l3-interface vlan.0;
    }
    v1 {
        vlan-id 1;
    }                                   
    v2 {
        vlan-id 2;
    }
}
```

## Routing

TODO

## Layer 3 port mirroring

Step 1: Configure port mirroring in the forwarding options hierarchy:

    [edit forwarding-options]

    port-mirroring {
        input {
            rate 1;
            run-length 10;
        }
        family inet {
            output {
                interface ge-0/0/1.0 {
                    next-hop 2.2.2.1;
                }
            }
        }
    }


Step 2: Configure firewall filter to port mirror

    [edit firewall]

    filter port-mirror {
        term 1 {
            from {
                source-address {
                    0.0.0.0/0;
                }
            }
            then {
                port-mirror;
                accept;
            }
        }
    }

Step 3: Apply the filter on an interface that is to be mirrored

    [edit interfaces]
        ge-0/0/0 {
            unit 0 {
                family inet {
                    filter {
                        input port-mirror;
                        output port-mirror;
                    }
                    address 1.1.1.1/24;
                }
            }
        }

**Note:** Port mirroring with ethernet-switching is not supported.

From https://kb.juniper.net/KB21833

## References

For J- and SRX-Series:

* [Interfaces Configuration Guide for Security Devices](http://www.juniper.net/techpubs/en_US/junos11.4/information-products/topic-collections/security/software-all/interfaces/index.html): PoE
* [Layer 2 Bridging and Switching Configuration Guide for Security Devices](http://www.juniper.net/techpubs/en_US/junos11.4/information-products/topic-collections/security/software-all/layer-2/index.html): Bridging, Transparent mode, VLAN
* [Initial Configuration Guide for Security Devices](http://www.juniper.net/techpubs/en_US/junos11.4/information-products/topic-collections/security/software-all/initial-config/index.html): Users, SSH, DHCP client/server
* [Routing Protocols and Policies Configuration Guide for Security Devices](http://www.juniper.net/techpubs/en_US/junos11.4/information-products/topic-collections/security/software-all/routing/index.html): BGP
* [Security Configuration Guide](http://www.juniper.net/techpubs/en_US/junos11.4/information-products/topic-collections/security/software-all/security/index.html): Packet- and flow-based filters, Security zones/policies, NAT
* [J Series and Branch SRX Series Ethernet Switching Configuration Guide](http://www.juniper.net/us/en/local/pdf/app-notes/3500196-en.pdf): Switching, VLAN

For EX-series:

* [Ethernet Switching on EX Series Switches](http://www.juniper.net/techpubs/en_US/junos11.4/information-products/topic-collections/ex-series/software-all/book-software-ex-series-ethernet-switching.pdf): Switching, VLAN
* [Network Management and Monitoring on EX Series Switches](http://www.juniper.net/techpubs/en_US/junos11.4/information-products/pathway-pages/ex-series/network-mgmt.pdf): Port mirroring (SPAN)
