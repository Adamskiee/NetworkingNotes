HSRP (Hot Standby Router Protocol) is a Cisco proprietary redundancy protocol designed to provide network resilience by ensuring high availability of the default gateway. It allows multiple routers to work together, with one router acting as the active gateway and another as a standby. If the active router fails, the standby router automatically takes over, minimizing downtime and ensuring continuous network connectivity.

---
### Key Features of HSRP:

- **Active and Standby Routers:** One router is elected as the active router, while another serves as the standby.
- **Virtual IP Address:** Hosts on the network use a virtual IP instead of a physical router IP.
- **Failover Mechanism:** If the active router fails, the standby router takes over automatically.
- **Preemption (Optional):** A higher-priority router can take over once it becomes available again.
- **Multicast Communication:** Uses multicast address **224.0.0.2** and UDP port **1985** for communication between HSRP-enabled routers.

### HSRP Priority
HSRP priority can be ==used to determine the active router==. The router with the highest HSRP priority will become the active router. By default, the HSRP priority is 100. If the priorities are equal, the router with the numerically highest IPv4 address is elected as the active router.
To configure a router to be the active router, use the **standby priority** interface command. The range of the HSRP priority is 0 to 255.

### HSRP Preemption
To force a new HSRP election process to take place when a higher priority router comes online, preemption must be enabled using the **standby preempt** interface command. Preemption is the ==ability of an HSRP router to trigger the re-election process==. With preemption enabled, a router that comes online with a higher HSRP priority will assume the role of the active router.

Preemption ==only allows a router to become the active router if it has a higher priority==. A router enabled for preemption, with equal priority but a higher IPv4 address will not preempt an active router. Refer to the topology in the figure.

![[Pasted image 20250311103852.png]]
[[HSRP for IPv6]] 
[[HSRP States]] 
[[FHRP/GAGA]]  