
- manually configured using the `ipv6 address` *`ipv6-address/prefix-length`*
- can be obtained static or DHCPv6 or SLAAC
- IPv6 enables router periodically send ICMPv6 RAs which simplifies how a host can dynamically create or acquire its IPv6 configuration
	- router advertise its Network ID

### Stateless
- no device is tracking the assignment of IPv6 address
- no bindings
##### - SLAAC Only
- Router sends RA messages providing all Ipv6 address information such as network prefix, prefix-length, and default gateway
- enable host to create their own unique IPv6 GUI
- a stateless service which means there is no server
- sends periodic ICMPv6 RA messages (i.e, every 200 seconds)
- if device have ipv6 address, the SLAAC is enabled
		- then type `ipv6 unicast-routing`
- example
	- R1 has been assigned the following IPv6 addresses:
		- **Link-local IPv6 address** - fe80::1
		- **GUA and subnet** - 2001:db8:acad:1::1 and 2001:db8:acad:1::/64
		- **IPv6 all-nodes group** - ff02::1
- SLAAC host may use Duplicate Address Detection(DAD).
	- device send NS that have address of him and if someone send NA, it is duplicate
##### - SLAAC with DHCP server
- same with SLAAC but ask stateless DHCPv6 server for DNS and domain-name
### Stateful
- a DHCPv6 server is managing the assignment of IPv6 addresses
#### - DHCPv6 Server
- RA messages inform hosts to  contact a stateful DHCPv6 server for all IPv6 configuration information, except the default gateway address
	- default gateway address is in RA

### ICMPv6 RA
- A flag
	- for SLAAC
- O flag
	- for SLAAC with DHCP server
- M flag
	- for stateful DHCPv6
- wait 180 seconds if pc is new
- host can request RA using Router Solicitation(RS)

#### Router Solicitation
- use all nodes group ff02:1



