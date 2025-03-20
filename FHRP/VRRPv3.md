**VRRPv3 (Virtual Router Redundancy Protocol version 3)** is an enhancement of **VRRPv2**, adding support for **both IPv4 and IPv6** networks. It is defined in **RFC 5798** and allows multiple routers to provide redundancy for a virtual IP address, ensuring high availability in a network.

---

### **Key Features of VRRPv3**

1. **Supports Both IPv4 & IPv6** – Unlike VRRPv2 (which only supports IPv4), VRRPv3 supports IPv6.
2. **No Authentication** – VRRPv3 removes authentication fields for simplicity.
3. **Preemption Enabled by Default** – If a higher-priority router comes online, it takes over automatically.
4. **Multicast Addresses:**
    - **IPv4:** `224.0.0.18`
    - **IPv6:** `FF02::12`
5. **Protocol Number:** Uses **IP protocol 112**, same as VRRPv2.
6. **Reduced Header Size** – VRRPv3 optimizes packet structure, reducing overhead.

### **Basic VRRPv3 Configuration (IPv4 & IPv6)**

#### **For IPv4:**
```cisco
interface GigabitEthernet0/0
 ip address 192.168.1.2 255.255.255.0
 vrrp 1 address-family ipv4
 vrrp 1 ip 192.168.1.1
 vrrp 1 priority 110
 vrrp 1 preempt
 vrrp 1 timers advertise 1
```
#### **For IPv6:**
```cisco
interface GigabitEthernet0/0
 ipv6 address 2001:DB8:1::2/64
 vrrp 1 address-family ipv6
 vrrp 1 ipv6 2001:DB8:1::1
 vrrp 1 priority 110
 vrrp 1 preempt
 vrrp 1 timers advertise 1
```

### **Explanation:**

- `vrrp 1 address-family ipv4` → Enables VRRP for IPv4.
- `vrrp 1 ip 192.168.1.1` → Sets the **virtual IPv4 address**.
- `vrrp 1 address-family ipv6` → Enables VRRP for IPv6.
- `vrrp 1 ipv6 2001:DB8:1::1` → Sets the **virtual IPv6 address**.
- `vrrp 1 priority 110` → Defines the router priority (higher = preferred).
- `vrrp 1 preempt` → Allows the highest-priority router to take over automatically.
- `vrrp 1 timers advertise 1` → Configures VRRP advertisement interval (default: 1 second).