**Gateway Load Balancing Protocol (GLBP)** is a Cisco proprietary protocol that provides both **gateway redundancy** and **load balancing** in a network. Unlike **HSRP** and **VRRP**, which only offer failover, **GLBP** allows multiple routers to share traffic load while still providing redundancy.

### **How GLBP Works:**

1. **Active Virtual Gateway (AVG):** One router is elected as the AVG, which assigns virtual MAC addresses to participating routers.
2. **Active Virtual Forwarders (AVFs):** Multiple routers act as AVFs, forwarding traffic to share the load.
3. **Load Balancing:** Uses different methods (round-robin, weighted, or host-dependent) to distribute traffic.
4. **Failover:** If an AVF fails, another AVF takes over seamlessly.

### **Why Use GLBP?**

- **Improved Network Efficiency:** Distributes traffic among multiple gateways.
- **Automatic Failover:** Ensures uninterrupted connectivity.
- **Flexible Load Balancing:** Offers different load-sharing strategies.

[[GLBP for IPv6]] 