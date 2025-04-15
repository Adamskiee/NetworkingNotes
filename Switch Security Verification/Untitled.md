[[Implement Port Security]]
# Mitigate VLAN Attacks

Use the following steps to mitigate VLAN hopping attacks:

**Step 1:** Disable DTP (auto trunking) negotiations on non-trunking ports by using the **switchport mode access** interface configuration command.

**Step 2:** Disable unused ports and put them in an unused VLAN.

**Step 3:** Manually enable the trunk link on a trunking port by using the **switchport mode trunk** command.

**Step 4:** Disable DTP (auto trunking) negotiations on trunking ports by using the **switchport nonegotiate** command.

**Step 5:** Set the native VLAN to a VLAN other than VLAN 1 by using the **switchport trunk native vlan** _vlan_number_ command.

For example, assume the following:

- FastEthernet ports 0/1 through fa0/16 are active access ports
- FastEthernet ports 0/17 through 0/20 are not currently in use
- FastEthernet ports 0/21 through 0/24 are trunk ports.
```
S1(config)# interface range fa0/1 - 16
S1(config-if-range)# switchport mode access
S1(config-if-range)# exit
S1(config)#
S1(config)# interface range fa0/17 - 20
S1(config-if-range)# switchport mode access
S1(config-if-range)# switchport access vlan 1000
S1(config-if-range)# shutdown
S1(config-if-range)# exit
S1(config)#
S1(config)# interface range fa0/21 - 24
S1(config-if-range)# switchport mode trunk
S1(config-if-range)# switchport nonegotiate
S1(config-if-range)# switchport trunk native vlan 999
S1(config-if-range)# end
S1#

```

# Mitigate DHCP Attacks
Use the following steps to enable DHCP snooping:

**Step 1**. Enable DHCP snooping by using the **ip dhcp snooping** global configuration command.

**Step 2**. On trusted ports, use the **ip dhcp snooping trust** interface configuration command.

**Step 3**. Limit the number of DHCP discovery messages that can be received per second on untrusted ports by using the **ip dhcp snooping limit rate** interface configuration command.

**Step 4**. Enable DHCP snooping by VLAN, or by a range of VLANs, by using the **ip dhcp snooping** _vlan_ global configuration command.

The following is an example of how to configure DHCP snooping on S1. Notice how DHCP snooping is first enabled. Then the upstream interface to the DHCP server is explicitly trusted. Next, the range of FastEthernet ports from F0/5 to F0/24 are untrusted by default, so a rate limit is set to six packets per second. Finally, DHCP snooping is enabled on VLANS 5, 10, 50, 51, and 52.

```
S1(config)# ip dhcp snooping
S1(config)# interface f0/1
S1(config-if)# ip dhcp snooping trust
S1(config-if)# exit
S1(config)# interface range f0/5 - 24
S1(config-if-range)# ip dhcp snooping limit rate 6
S1(config-if-range)# exit
S1(config)# ip dhcp snooping vlan 5,10,50-52
S1(config)# end
S1#
```

Use the show ip dhcp snooping privileged EXEC command to verify DHCP snooping and show ip dhcp snooping binding to view the clients that have received DHCP information, as shown in the example.

Note: DHCP snooping is also required by Dynamic ARP Inspection (DAI), which is the next topic

```
S1# show ip dhcp snooping
Switch DHCP snooping is enabled
DHCP snooping is configured on following VLANs:
5,10,50-52
DHCP snooping is operational on following VLANs:
none
DHCP snooping is configured on the following L3 Interfaces:
Insertion of option 82 is enabled
   circuit-id default format: vlan-mod-port
   remote-id: 0cd9.96d2.3f80 (MAC)
Option 82 on untrusted port is not allowed
Verification of hwaddr field is enabled
Verification of giaddr field is enabled
DHCP snooping trust/rate is configured on the following Interfaces:
Interface                  Trusted    Allow option    Rate limit (pps)
-----------------------    -------    ------------    ----------------  
FastEthernet0/1            yes        yes             unlimited
  Custom circuit-ids:
FastEthernet0/5            no         no              6        
  Custom circuit-ids:
FastEthernet0/6            no         no              6        
  Custom circuit-ids:
S1# show ip dhcp snooping binding
MacAddress         IpAddress       Lease(sec) Type          VLAN Interface
------------------ --------------- ---------- ------------- ---- --------------------
00:03:47:B5:9F:AD  192.168.10.11   193185     dhcp-snooping 5    FastEthernet0/5
```

# Mitigate ARP Attacks
To mitigate the chances of ARP spoofing and ARP poisoning, follow these DAI implementation guidelines:
	Enable DHCP snooping globally.
	Enable DHCP snooping on selected VLANs.
	Enable DAI on selected VLANs.
	Configure trusted interfaces for DHCP snooping and ARP inspection.
	It is generally advisable to configure all access switch ports as untrusted and to configure all uplink ports that are connected to other switches as trusted.

As shown in the example, DHCP snooping is enabled because DAI requires the DHCP snooping binding table to operate. Next, DHCP snooping and ARP inspection are enabled for the PCs on VLAN10. The uplink port to the router is trusted, and therefore, is configured as trusted for DHCP snooping and ARP inspection.

```
S1(config)# ip dhcp snooping
S1(config)# ip dhcp snooping vlan 10
S1(config)# ip arp inspection vlan 10
S1(config)# interface fa0/24
S1(config-if)# ip dhcp snooping trust
S1(config-if)# ip arp inspection trust
```
DAI can also be configured to check for both destination or source MAC and IP addresses:

Destination MAC - Checks the destination MAC address in the Ethernet header against the target MAC address in ARP body.
Source MAC - Checks the source MAC address in the Ethernet header against the sender MAC address in the ARP body.
IP address - Checks the ARP body for invalid and unexpected IP addresses including addresses 0.0.0.0, 255.255.255.255, and all IP multicast addresses.

The `ip arp inspection validate {[src-mac] [dst-mac] [ip]}` global configuration command is used to configure DAI to drop ARP packets when the IP addresses are invalid. It can be used when the MAC addresses in the body of the ARP packets do not match the addresses that are specified in the Ethernet header. Notice in the following example how only one command can be configured. Therefore, entering multiple `ip arp inspection validate` commands overwrites the previous command. To include more than one validation method, enter them on the same command line as shown and verified in the following output.

```
S1(config)# ip arp inspection validate ?
dst-mac  Validate destination MAC address
  ip       Validate IP addresses
  src-mac  Validate source MAC address
S1(config)# ip arp inspection validate src-mac
S1(config)# ip arp inspection validate dst-mac
S1(config)# ip arp inspection validate ip
S1(config)# do show run | include validate
ip arp inspection validate ip
S1(config)# ip arp inspection validate src-mac dst-mac ip
S1(config)# do show run | include validate
ip arp inspection validate src-mac dst-mac ip
S1(config)#
```

# Mitigate STP Attacks
## Configure PortFast
PortFast can be enabled on an interface by using the **s`panning-tree portfast`** interface configuration command. Alternatively, Portfast can be configured globally on all access ports by using th`e **spanning-tree portfast default`** global configuration command.

To verify whether PortFast is enabled globally you can use either the **`show running-config | begin span`** command or the **`show spanning-tree summary`** command. To verify if PortFast is enabled an interface, use the **`show running-config interface`** _type/number_ command, as shown in the following example. The **`show spanning-tree interface`** _type/number_ **detail** command can also be used for verification.

```
S1(config)# interface fa0/1
S1(config-if)# switchport mode access
S1(config-if)# spanning-tree portfast
%Warning: portfast should only be enabled on ports connected to a single
host. Connecting hubs, concentrators, switches, bridges, etc... to this
interface when portfast is enabled, can cause temporary bridging loops.
Use with CAUTION
%Portfast has been configured on FastEthernet0/1 but will only
have effect when the interface is in a non-trunking mode.
S1(config-if)# exit
S1(config)# spanning-tree portfast default
%Warning: this command enables portfast by default on all interfaces. You
should now disable portfast explicitly on switched ports leading to hubs,
switches and bridges as they may create temporary bridging loops.
S1(config)# exit
S1# show running-config | begin span
spanning-tree mode pvst
spanning-tree portfast default
spanning-tree extend system-id
!
interface FastEthernet0/1
switchport mode access
spanning-tree portfast
!
interface FastEthernet0/2
!
interface FastEthernet0/3
!
interface FastEthernet0/4
!
interface FastEthernet0/5
!
(output 
```

## Configure BPDU Guard

If any BPDUs are received on a BPDU Guard enabled port, that port is put into error-disabled state. This means the port is shut down and must be manually re-enabled or automatically recovered through the **`errdisable recovery cause bpduguard`** global command.

BPDU Guard can be enabled on a port by using the **`spanning-tree bpduguard enable`** interface configuration command. Alternatively, Use the **`spanning-tree portfast bpduguard default`** global configuration command to globally enable BPDU guard on all PortFast-enabled ports.

To display information about the state of spanning tree, use the **`show spanning-tree summary`** command. In the example, PortFast default and BPDU Guard are both enabled as the default state for ports configured as access mode.

**Note:** Always enable BPDU Guard on all PortFast-enabled ports.
```
S1(config)# interface fa0/1
S1(config-if)# spanning-tree bpduguard enable
S1(config-if)# exit
S1(config)# spanning-tree portfast bpduguard default
S1(config)# end
S1# show spanning-tree summary
Switch is in pvst mode
Root bridge for: none
Extended system ID           is enabled
Portfast Default             is enabled
PortFast BPDU Guard Default  is enabled
Portfast BPDU Filter Default is disabled
Loopguard Default            is disabled
EtherChannel misconfig guard is enabled
UplinkFast                   is disabled
BackboneFast                 is disabled
Configured Pathcost method used is short
(output omitted)
S1#
```
