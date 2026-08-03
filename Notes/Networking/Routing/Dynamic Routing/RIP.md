**Routing Information Protocol**

- RIP is a distance vector protocol
- Best path is calculated based on the amount of hops
![[Pasted image 20260731102137.png]]
# Features
- Updates routing table every 30s
- Low resource usage
- Has its own RFC
- Max of 15 hops before it drops the packet
- Sends full updates
# Versions
## Version 1
- Classful routing
- no VLSM support
- Broadcast updates
- UDP port 520
## Version 2
- VLSM support
- Multicast instead of broadcast
- Improved interoperability
# Default Routes
- Used when no specific route exists for the destination network
- Configure a static default route on the edge router connected to the internet
- Use default-information originate to advertise the default route to RIP neighbors
![[Pasted image 20260803143908.png]]
# Configuration
- Must config all routers
```
R1(config)# router rip
R1(config-router)# version 2
R1(config-router)# no auto-summary
! Must supply all interface network addresses
R1(config-router)# network network_address
R1(config-router)# network network_address
! Default Route
R1(config-router)# default-information originate
```
