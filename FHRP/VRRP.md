**Virtual Router Redundancy Protocol (VRRP)** is a standard (open) redundancy protocol similar to **HSRP**, but it is not proprietary to Cisco. It allows multiple routers to work together, ensuring high availability of the default gateway for devices in a network.

### **How VRRP Works:**

1. **Master Router:** The highest-priority router becomes the Master and owns the virtual IP.
2. **Backup Routers:** The other routers monitor the Master and take over if it fails.
3. **Preemption:** Enabled by default—if a higher-priority router comes online, it takes back control.
4. **Failover:** If the Master fails, the Backup router with the next highest priority takes over.

[[VRRPv2]] 
[[VRRPv3]] 