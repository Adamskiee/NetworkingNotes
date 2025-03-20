**VRRPv2 (Virtual Router Redundancy Protocol version 2)** is an enhanced version of VRRP designed for **IPv4 networks**. It improves upon VRRPv1 with better support for authentication and faster failover mechanisms. VRRPv2 remains an **open standard (RFC 3768)**, allowing routers from different vendors to interoperate.

---
### **Key Features of VRRPv2**

1. **IPv4 Support Only** – VRRPv2 is designed specifically for IPv4 (VRRPv3 adds IPv6 support).
2. **Faster Failover** – Improves failover speed compared to VRRPv1.
3. **Preemption Enabled by Default** – If a higher-priority router comes online, it automatically becomes the Master.
4. **Multicast Address:** Uses **224.0.0.18** for VRRP advertisements.
5. **Protocol Number:** Uses **IP protocol 112** (unlike HSRP, which uses UDP 1985).
### **Basic VRRPv2 Configuration (Cisco)**
```cisco
interface GigabitEthernet0/0
 ip address 192.168.1.2 255.255.255.0
 vrrp 1 ip 192.168.1.1
 vrrp 1 priority 110
 vrrp 1 preempt
 vrrp 1 timers advertise 1
```
### **Explanation:**

- `vrrp 1 ip 192.168.1.1` → Sets the virtual IP address.
- `vrrp 1 priority 110` → Configures router priority (higher means preferred).
- `vrrp 1 preempt` → Allows a higher-priority router to take over automatically.
- `vrrp 1 timers advertise 1` → Adjusts VRRP advertisement interval (default: 1s).

[[VRRPv3]] 