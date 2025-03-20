**GLBP (Gateway Load Balancing Protocol)** is a Cisco-proprietary **redundancy and load-balancing protocol** that provides **default gateway redundancy** while distributing traffic across multiple routers. It supports **both IPv4 and IPv6**, with IPv6 support introduced in **GLBPv2**.

---

### **Key Features of GLBP for IPv6**

✅ **Supports IPv6** – Works similarly to GLBP for IPv4 but with IPv6 addresses.  
✅ **Load Balancing** – Distributes traffic among multiple routers.  
✅ **Virtual MAC Addresses** – Assigns a unique MAC address for each gateway.  
✅ **Active Virtual Gateway (AVG) & Active Virtual Forwarders (AVF)** – Just like in IPv4:

- **AVG**: Assigns virtual MACs and manages the group.
- **AVF(s)**: Forward traffic based on load-balancing methods.  
    ✅ **Preemption & Tracking** – Allows failover when a higher-priority router comes online or a tracked interface fails.  
    ✅ **Multicast Address:** Uses **FF02::66** for GLBP advertisements (same as HSRP for IPv6).

### **Basic GLBP for IPv6 Configuration (Cisco)**
```cisco
interface GigabitEthernet0/0
 ipv6 address 2001:DB8:1::2/64
 glbp 1 ipv6 2001:DB8:1::1
 glbp 1 priority 110
 glbp 1 preempt
 glbp 1 timers 1 3
 glbp 1 load-balancing weighted
 glbp 1 track GigabitEthernet0/1
```
### **Explanation:**

- `glbp 1 ipv6 2001:DB8:1::1` → Sets the **virtual IPv6 address**.
- `glbp 1 priority 110` → Sets priority (higher is preferred as AVG).
- `glbp 1 preempt` → Enables preemption for failover.
- `glbp 1 timers 1 3` → Configures **hello (1s)** and **hold (3s)** timers.
- `glbp 1 load-balancing weighted` → Enables **weighted** load balancing (other options: round-robin, host-dependent).
- `glbp 1 track GigabitEthernet0/1` → Tracks an interface and adjusts priority if it goes down.