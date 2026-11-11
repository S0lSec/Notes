## Static
Static routes are easy to use, troubleshoot and use a low amount of resources, but are hard to scale.

A static route provides simplicity, allowing a single connection to a router without the need to configure or troubleshoot additional settings. When a static route goes down you only need to look a small list, while dynamic requires much more in depth troubleshooting.

Static routes used less resources making them desirable for a low power router.
### How to Setup
When creating static routes use a single router to reach specific networks, then create a route to this router. This makes it easier to manage and allows for a easier time configuring. (This is called **router summarisation**)

**Example**
 Say networks 192.168.0.0/24 through 192.168.20.0/24 all sit behind the same router. Instead of configuring 21 separate static routes, you can use one summary route:

`ip route 192.168.0.0 255.255.224.0 10.0.0.1`

A /19 covers 192.168.0.0 to 192.168.31.255, so all 21 networks are included in a single entry, and it’s the smallest single summary that does so. It also covers 192.168.21.0 to 192.168.31.0, which is fine as long as those ranges aren’t used anywhere else. In fact, it’s good practice to reserve them for future growth behind that same router. I’ve attached a simple diagram showing this.
![[Pasted image 20261111110712.png]]

Although static routes are simple and easy to manage, they become hard to use when a number of networks increases immensely. 
## Dynamic
Dynamic routing provides scalability and automatic adaption to failures.

Dynamic routes although more difficult to troubleshoot allow for a more scalable and reliable network. Dynamic routing provides automatic reconvergence allowing data to be sent to different routes in the case the current one goes down.

Of course static routes can do this to some degree, but the main problem is if the dead link is on the other side of a router. In that case a static route will not change routes because the first link is still up. However dynamic routing has features such as IP SLA tracking allowing it to detect the dead link and redirect traffic.
![[Pasted image 20261111112654.png]]
## When to use?
The first thing to determine is how well can the IT team deal with static or dynamic routes. If you use dynamic routing and staff can not troubleshoot efficiently then it is pointless and static routes should be used.

However if dynamic and static routing are options then it depends. If you need a scalable and reliable network use dynamic routing else use static routing.