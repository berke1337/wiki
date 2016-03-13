# Palo Alto firewall

Palo Alto firewalls run an operating system called PAN-OS. Documentation may be
found on the PAN website https://www.paloaltonetworks.com/documentation.

## CLI configuration

The OS exposes a Juniper-like command line interface. This means there is a
*operational mode* (denoted with `>` in the command list below) which allows you
 to inspect the system as it is running and a *configuration mode* (denoted with
    `#` in the command list below) which allows you to stage configuration
    changes.

There does not seem to be a CLI reference for version 7 of the OS, but there is
one for version 6.1:
https://www.paloaltonetworks.com/content/dam/pan/en_US/assets/pdf/technical-documentation/pan-os-61/PAN-OS-6.1-CLI-ref.pdf

Operation                                        | Command
-------------------------------------------------|------------------------------
Find a command                                   | `find command keyword <name>`
Enter configuration mode                         | `> configure`
Run an operational-mode command                  | `> run <command>`
Show diff of current and candidate configuration | `> show config diff`
                                                 | `# run show config diff`
Revert unsaved changes                           | `# load config last-saved`
Commit and save changes                          | `# commit`

### Secure configuration

**TODO** add information for sane default configuration

### NAT

Configuration tree under `rulebase nat rules`.

Rules are evaluated in order, and a matching rule ends the translation process.
Don't forget to also add security policies for inter-zone traffic.

### Firewall

Configuration tree under `rulebase security rules`.

**NOTE** when using SNAT, use the post-NAT source *zone*, but pre-NAT source
*address*! Likewise, when using DNAT, use the post-NAT destination *zone*, but
pre-NAT destination *address*! See
https://www.paloaltonetworks.com/documentation/70/pan-os/pan-os/networking/nat-policy-rules#72366.
**TODO** figure out if these rules hold true. Netlab lab 3 suggests otherwise
for source zone...

You can test NAT rules using `> test nat-policy-match`.

**TODO** figure out difference between *applications* and *services*.

By default, intra-zone traffic is allowed and inter-zone traffic is denied. You
can change this under `rulebase default-security-rules`.

### Loading partial configuration

Loading a partial configuration is very finicky. If you do it wrong, e.g. by
using an incorrect load command syntax, you might be logged out from your terminal without warning.

```bash
scp import configuration source-ip <IP> from <user>@<host>:<file>
load config partial from <file> mode <mode> from-xpath <path> to-xpath /config/<path>
```

Those paths do not match the paths you will see in configuration mode, instead
refer to the following table:

Xpath                        | Configuration mode items under this path
-----------------------------|-----------------------------------------
...                          | mgt-config, shared
devices/entry/...            | deviceconfig, network
devices/entry/vsys/entry/... | application, application-group, import, rulebase, schedule, service, service-group, zone

There are 3 modes: *replace*, *merge* and *append*. *merge* and *append* are
both pretty much ill-defined and should basically only be used when there is a
list of multiple named entries that you want to append to.

## Guides and documentation

*Designing Networks with Palo Alto Networks Firewalls*: https://live.paloaltonetworks.com/twzvq79624/attachments/twzvq79624/IntegrationArticles/29/1/PaloAltoNetworks-Designs-Guide-RevB.pdf

SANS put together nice guide for securely configuring PA firewalls, but
unfortunately it mostly talks about the web interface. However, there are links
to the PAN website which usually include the equivalent CLI commands: https://www.sans.org/reading-room/whitepapers/auditing/palo-alto-firewall-security-configuration-benchmark-35777

## Netlab+ PA Firewall essentials lab series

https://openlabs.netdevgroup.com/local/ex/PAN7FE_0050_56A9_38CC_5682_DA4B/doc/PAN7_Lab_01.pdf
https://openlabs.netdevgroup.com/local/ex/PAN7FE_0050_56A9_38CC_5682_DA4B/doc/PAN7_Lab_02.pdf
https://openlabs.netdevgroup.com/local/ex/PAN7FE_0050_56A9_38CC_5682_DA4B/doc/PAN7_Lab_03.pdf
https://openlabs.netdevgroup.com/local/ex/PAN7FE_0050_56A9_38CC_5682_DA4B/doc/PAN7_Lab_04.pdf
https://openlabs.netdevgroup.com/local/ex/PAN7FE_0050_56A9_38CC_5682_DA4B/doc/PAN7_Lab_05.pdf
https://openlabs.netdevgroup.com/local/ex/PAN7FE_0050_56A9_38CC_5682_DA4B/doc/PAN7_Lab_06.pdf
https://openlabs.netdevgroup.com/local/ex/PAN7FE_0050_56A9_38CC_5682_DA4B/doc/PAN7_Lab_07.pdf
https://openlabs.netdevgroup.com/local/ex/PAN7FE_0050_56A9_38CC_5682_DA4B/doc/PAN7_Lab_08.pdf
https://openlabs.netdevgroup.com/local/ex/PAN7FE_0050_56A9_38CC_5682_DA4B/doc/PAN7_Lab_09.pdf
https://openlabs.netdevgroup.com/local/ex/PAN7FE_0050_56A9_38CC_5682_DA4B/doc/PAN7_Lab_10.pdf
https://openlabs.netdevgroup.com/local/ex/PAN7FE_0050_56A9_38CC_5682_DA4B/doc/PAN7_Lab_11.pdf
https://openlabs.netdevgroup.com/local/ex/PAN7FE_0050_56A9_38CC_5682_DA4B/doc/PAN7_Lab_12.pdf
https://openlabs.netdevgroup.com/local/ex/PAN7FE_0050_56A9_38CC_5682_DA4B/doc/PAN7_Lab_13.pdf
https://openlabs.netdevgroup.com/local/ex/PAN7FE_0050_56A9_38CC_5682_DA4B/doc/PAN7_Lab_14.pdf
https://openlabs.netdevgroup.com/local/ex/PAN7FE_0050_56A9_38CC_5682_DA4B/doc/PAN7_Lab_15.pdf
