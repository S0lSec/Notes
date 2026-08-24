ACLs are used to filter traffic passing through routers, similar to a firewall. Each interface on a router can have a different ACL for both inbound and outbound traffic.

ACLs match values found in IP, TCP, UDP and other protocol headers.
ACLs are also used for other features such as QoS, by matching specific traffic type.
![[Pasted image 20260821082430.png]]
# Location and Direction
To block access from a device you need to know:
- The **path** taken by the packet from the device
- The **router** and **interface** (location)
- Is the traffic **inbound** or **outbound** (direction)
![[Pasted image 20260821082626.png]]
In this topology ACL can be applied:
- Inbound on R1 G0/1 interface
- Outbound on R1 G0/0 Interface
- Inbound on R2 G0/0 interface
- Outbound on R2 G0/1 interface
# ACL Types
## Standard
#### Standard Numbered ACLs
(1-99 & 1300-1999)
- Matches only the source IP of the packet
- Each ACL contains a list of commands
- Each command contains a matching and action logic

`Access-list 1, if Source IP is 172.16.10.10, then deny`
Match -> `172.16.10.10`
Action -> `deny`
ACL number -> `1`

**Access Control Entry (ACE)** are used to control entry based on an IP address 
e.g. `accesslist 1 deny 172.16.10.10`
e.g. `accesslist 1 permit 172.16.10.10`

- Named ACLs

Using a wildcard mask you can allow a range of IP addresses
`access-list 1 permit 17.26.16.0 0.0.0.255`

A implicit deny is active, but you can implement a implicit allow.
`access-list 1 permit any`
## Extended
- Numbered ACLs (100-1999 & 2000-2699)
- Named ACLs

Matches via the source + destination IP/port and the protocol used