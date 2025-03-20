Operation Steps
1. device send Router solicitation
2. server Router Advertisement
3. device send SOLICIT to all DHCPv6 Servers
4. server send ADVERTISE Unicast
5. device send REQUEST or INFORMATION-REQUEST Unicast
6. server send REPLY Unicast

- server to client uses UDP destination port 546 while client to server use 547
- if O flag and M flag there is error
### Enable stateless DHCPv6
- enabled by command `ipv6 nd other-config-flag`
- `show ipv6 interface g0/0/1 | begin ND` for checking

### Enable stateful DHCPv6 
- enabled by command `ipv6 nd managed-config-flag`