**(First Hop Redundancy Protocols)**

# Default Gateway Limitations
- In the case that a router or router interface fails the hosts configured with that default gateway are isolated from outside networks. FHRP provides a mechanism to provide alternate default gateway.
- An end device can only have one default gateway at a time
# Router Redundancy
- A method of preventing a single point of failure at the default gateway is to implement a virtual router.
- To implement multiple routes are configured to work together to present the illusion of a single router to the hosts on the LAN.
![[Pasted image 20260427121913.png]]
- The IPv4 address of the virtual router is configured as the default gateway
- When frames are sent from host devices to the default gateway, the hosts use ARP to resolve the MAC address that is associated with the IPv4 address of the default gateway
- The ARP resolution returns the MAC address of the virtual router
- Frames sent to the virtual routers can then be physically processed by the current active router
# Router Failover
When the active router fails, the redundancy protocol transitions the standby router to the new active router role.
**Steps taken when active router fails:**
1. The standby router stops seeing Hello messages from the forwarding router
2. The standby router assumes the role of forwarding router
3. Because the new forwarding router assumes both IPv4 and MAC addresses of the virtual router, the host devices see no disruptions in service
![[Pasted image 20260428123652.png]]
# Host Standby Router Protocol (HSRP)
- Used to avoid losing outside network access if your default router fails
- Ensures high network availability by providing first-hop redundancy for IP hosts on networks configured with an IP default gateway address
## Priority
- Used to determine active routers
- Router with highest priority becomes active router
- To configure a router to be active use the `standby priority` interface command
- (Range of priority is 0 -255, 100 is default)
## Preemption
- By default a router will remain active even if another router has a higher priority
- To force the election process use `standby preempt` interface command
![[Pasted image 20260504084339.png]]
## States and timers
**Initial**  
This state is entered through a configuration change or when an interface first becomes available.

**Learn**  
The router has not determined the virtual IP address and has not yet seen a hello message from the active router. In this state, the router waits to hear from the active router.

**Listen**  
The router knows the virtual IP address, but the router is neither the active router nor the standby router. It listens for hello messages from those routers.

**Speak**  
The router sends periodic hello messages and actively participates in the election of the active and/or standby router.

**Standby**  
The router is a candidate to become the next active router and sends periodic hello messages.

**Active**  
The router won the election.