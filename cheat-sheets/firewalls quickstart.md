# Firewall Quickstart

## Linux - iptables

iptables is a user-space application program that allows a system administrator
to configure the tables provided by the Linux kernel firewall (implemented as
different Netfilter modules) and the chains and rules it stores. Different
kernel modules and programs are currently used for different protocols;
iptables applies to IPv4, ip6tables to IPv6, arptables to ARP, and ebtables
to Ethernet frames.

1. List firewall rules

    ```bash
iptables-save | tee iptables.rules
```

2. Edit the file you created in the last step to lock it down, or start from
   scratch. Here is an example file:

    ```
# Drop incoming packets by default
*filter
:INPUT DROP
:FORWARD DROP
:OUTPUT ACCEPT

  # Allow established connections
# If conntrack is supported use this:
-A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
# Otherwise use
# -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT

  # Allow pings to this box
-A INPUT -p icmp -j ACCEPT

  # Allow traffic on loopback
-A INPUT -i lo -j ACCEPT

  # For each port you want to open (i.e. ssh)
-A INPUT -p tcp --dport 22 -j ACCEPT

  # Save rules
COMMIT
```

3. Load the firewall rules you just created

    ```bash
iptables-restore < iptables.rules
```

## Solaris - ipf

1. List active rules

    ```bash
ipfstat -io
```

2. Create a file to store firewall rules, here is an example:

    ```
    # Allow all traffic on loopback.
pass in quick on lo0 all
pass out quick on lo0 all

  # Allow all out, including incoming packets from established connections
pass out quick keep state

  # Allow pings in
pass in quick proto icmp keep state

  # Allow certain ports (i.e. ssh)
pass in quick proto tcp from any to any port = 22 keep state

  # Drop incoming packets by default
block in all
```

3. Load rules

    ```bash
# Make sure ipfilter is enabled
svcadm enable network/ipfilter
# Load rules
ipf -Fa -f ipf.rules
```
