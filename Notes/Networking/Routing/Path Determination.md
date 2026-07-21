The primary function of a router is to determine the best path to forward packets based on the information in its routing table.
![[Pasted image 20260518090954.png]]
(Example of two networks connected together)
1. Packet reaches router
2. Router checks destination address
3. Checks routing table for the address and path to destination
4. Forwards packet to destination addresses router
# Best Path Equals Longest Match
The routing table contains route entries consisting of a prefix and prefix length.
For there to be a match between the destination IP address of a packet and a route in the routing table, a minimum number of fair-left bits must match between the IP address of the packet and the route in the routing table.

The prefix length of the route in the routing table is used to determine the number of far-left bits that must match. Remember that an IP packet only contains the destination IP address and not the prefix length.

The longest match is the route in the routing table that has the greatest number of far-left matching bits with the destination IP address of the packet. The route with the greatest number of equivalent far-left bits or the longest match is always the preferred route.
# IPv4 Example
**Destination Address:** 172.16.0.10
**Binary Version:** *10101100.00010000.00000000.00*001010 

**Routing Table**

| **Route Entry** | **Prefix/Prefix Length** | **Address in Binary**                 |
| --------------- | ------------------------ | ------------------------------------- |
| 1               | 172.16.0.0/12            | *10101100.0001*0000.00000000.00001010 |
| 2               | 172.16.0.0/18            | *10101100.00010000.00*000000.00001010 |
| 3 (Match)       | 172.16.0.0/26            | *10101100.00010000.00000000.00*001010 |
# IPv6
**Destination Address:** 2001:db8:c000::99

| **Route Entry** | **Prefix/Prefix Length** | **Does it match?**               |
| --------------- | ------------------------ | -------------------------------- |
| 1               | *2001:db8:c0*00::/40     | Match of 40 bits                 |
| 2               | *2001:db8:c000*::/48     | Match of 48 bits (longest match) |
| 3               | *2001:db:c000*:5555::/64 | Does not match 64 bits           |