### **HSRP States and Their Functions**

| **HSRP State** | **Description**                                                        | **Actions Performed**                                                         |
| -------------- | ---------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| **Initial**    | The router is starting up or restarting the HSRP process.              | No participation in HSRP yet.                                                 |
| **Learn**      | The router listens for hello messages to learn the virtual IP address. | No active/standby role yet.                                                   |
| **Listen**     | The router knows the virtual IP but is neither active nor standby.     | Listens for hello messages from active and standby routers.                   |
| **Speak**      | The router sends hello messages and participates in elections.         | Competes to become an active or standby router.                               |
| **Standby**    | The backup router that takes over if the active router fails.          | Continuously listens for hello messages from the active router.               |
| **Active**     | The primary router that forwards traffic.                              | Responds to ARP requests, sends hello messages, and maintains the HSRP group. |
