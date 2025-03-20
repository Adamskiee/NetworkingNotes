**FHRP (First Hop Redundancy Protocol)** is needed to ==provide alternate default gateways== in switched networks where two or more routers are connected to the same VLANs

---
# **Options:**
## **[[HSRP]] (Hot Standby Router Protocol)**
**Terminology**: Active/Standby
**Multicast IP**: 
- v1: 224.0.0.2
- v2: 224.0.0.102

**Virtual MAC**: 
- v1: 0000.0c07.acXX
- v2: 0000.0c9f.fXXX

**Cisco Proprietary**: Yes

---
## **[[VRRP]] (Virtual Router Redundancy Protocol)**
**Terminology**: Master/Standby
**Multicast IP**: 224.0.0.18
**Virtual MAC**: 0000.5e00.01XX
**Cisco Proprietary**: No

--- 
## **[[GLBP]] (Gateway Load Balancing Protocol)**
**Terminology**: AVG/AVF
**Multicast IP**: v1 224.0.0.102
**Virtual MAC**: v1 0007.b400.XXYY
**Cisco Proprietary**: Yes

[[FlashCard]]
