
### Configure Stateless DHCP server
1. enable `ipv6 unicast-routing` command
2. define `ipv6 dhcp pool` *POOL-NAME*
3. configure the DHCPv6 pool by `dns-server` and `domain-name` name
4. go to the interface by enabling `ipv6 nd other-config-flag` and `ipv6 dhcp server`*POOL-NAME*

### Configure Stateless DHCP client
1. `ipv6 unicast-routing`
2.  to the interface, `ipv6 enable`
3.  to the interface, `ipv6 address autoconfig`

### Configure Stateful DHCPv6 server
1. `ipv6 unicast-routing`
2. `ip dhcp pool` *POOL-NAME*
3. `address prefix` *ipv6-address prefix*, `dns-server`, `domain-name`
4. to the interface, `ipv6 nd managed-auto-config`, `ipv6 nd prefix default no-auto-config`, and `ipv6 dhcp server` *POOL-NAME*
	- The M flag is manually changed from 0 to 1 using the interface command **`ipv6 nd managed-config-flag`**.
	- The A flag is manually changed from 1 to 0 using the interface command **`ipv6 nd prefix default no-autoconfig`**. The A flag can be left at 1, but some client operating systems such as Windows will create a GUA using SLAAC and get a GUA from the stateful DHCPv6 server. Setting the A flag to 0 tells the client not to use SLAAC to create a GUA. **NOT AVAILABLE IN CISCO DEVICE**
	- The **`ipv6 dhcp server`** command binds the DHCPv6 pool to the interface. R1 will now respond with the information contained in the pool when it receives stateful DHCPv6 requests on this interface.
### Configure Stateful DHCPv6 client
1. `ipv6 unicast-routing`
2. to the interface, `ipv6 enable`
3. to the interface, `ipv6 address dhcp`

### DHCPv6 Server Verification Commands
1. `show ipv6 dhcp pool`
2. `show ipv6 dhcp binding`
### Configure a DHCPv6 Relay Agent
`ipv6 dhcp relay destination` *ipv6-address* *interface-to-server*
