# Routing Protocol Functions
1. **Learn** routing info about networks from neighboring routers
2. **Advertise** routing info about network to neighboring routers
3. **Select** the best route when multiple paths exist based on a set metric
4. **React** to network changes by updating routes and paths
![[Pasted image 20260803141315.png|507]]
# Dynamic Routing
- IGP (Interior Gateway Protocol)
	- Distance Vector
		- [RIP (Routing Information Protocol)](Notes/Networking/Routing/Dynamic%20Routing/RIP)
	- Link-state
		- [OSPF (Open Shortest Path First)](Notes/Networking/Routing/Dynamic%20Routing/OSPF%20Router%20ID)
- EGP (Exterior Gateway Protocols)
	- BGP (Border Gateway Protocol)
## Distance Vector
- Only knows what neighbors tell them
- Cant see the whole network
- Low resource usage
- Can lead to using slower paths
## Link-State
- Knows the entire network
- Needs lots of resources
- Can calculate the best path themselves
# Interior and Exterior Routing Protocols
**IGP**: A routing protocol that was designed and intended for use inside a single autonomous system (AS)
**EGP**: A routing protocol that was designed and intended for use between different autonomous systems
**Autonomous system (AS)**: An AS is a network under the administrative control of a single organization.
![[Pasted image 20260803142028.png]]
## IGP vs EGP
![[Pasted image 20260803142147.png]]
# Administrative Distance (AD)
- Measure of the trustworthiness of a routing information source.
- The routing protocol with the lowest AD is chosen.
- You usually only use one type of routing protocol
![[Pasted image 20260803143504.png]]

| **Routing Information Source** | **AD Value** |
| -------------------------- | -------- |
| Connected                  | 0        |
| Static                     | 1        |
| RIP                        | 120      |
| EIGRP (internal)           | 90       |
| OSPF                       | 110      |
| IS-IS                      | 115      |
| EIGRP (external)           | 170      |
| iBGP/eBGP                  | 200/20   |
| Unreachable                | 255      |
