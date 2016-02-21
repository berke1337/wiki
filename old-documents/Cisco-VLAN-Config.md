**Note**: I've been warned by another networking guy to ensure that ports have their mode explicitly marked as "access", and that DTP (dynamic trunk protocol) and VTP (vlan trunking protocol) are disabled. These features, if not set, could allow attackers to hop vlans. The commands to disable these protocols are ```vtp mode transparent``` and ```switchport nonegotiate```.

### Factory Reset
```
rename flash:/config.text flash:/config.text.old
delete flash:/vlan.dat
write erase
reload
```

### Cisco Catalyst 3500XL

#### Adding a VLAN
```
vlan database
vlan <vlan-id> name <vlan-name>
exit
```

#### Assign Port to a VLAN
```
configure terminal
interface <interface>
switchport mode access
switchport access vlan <vlan-id>
exit
```

#### Configure a trunk port
```
configure terminal
interface <interface-id>
switchport mode trunk
switchport trunk encapsulation {isl or dot1q}
end
```

#### Defining the Allowed VLANs on trunk
```
configure terminal
interface <interface-id>
switchport mode trunk
switchport trunk allowed vlan add <vlan-list>
end
```

### Cisco Catalyst 2960

#### Adding a VLAN
```
configure terminal
vlan <vlan-id>
end
```

#### Assign Ports to a VLAN
```
configure terminal
interface <interface>
switchport mode access
switchport access vlan <vlan-id>
end
```

#### Configure a trunk port
```
configure terminal
interface <interface-id>
switchport mode trunk
end
```

#### Defining the Allowed VLANs on trunk
```
configure terminal
interface <interface-id>
switchport mode trunk
switchport trunk allowed vlan add <vlan-list>
end
```
