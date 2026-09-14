ACLs are used to filter traffic passing through routers, similar to a firewall. Each interface on a router can have a different ACL for both inbound and outbound traffic.

Apply ACLs as close to the destination as possible.

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
- [Standard](/Networking/Routing/Access%20Control%20Lists%20(ACLs)/Standard.md)
- [Extended](/Networking/Routing/Access%20Control%20Lists%20(ACLs)/Extended.md)
