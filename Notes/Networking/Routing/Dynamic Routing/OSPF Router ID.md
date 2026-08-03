OSFP -> **Open Shortest Path First**
# Configuration
## Open config mode
`R1(config)# router ospf <Process ID>`
## Configure loopback interface as the router ID
Instead of relying on physical interface, the router ID can be assigned to a loopback interface.
```
R1(config-if)# interface Loopback 1
R1(config-if)# ip address 1.1.1.1 255.255.255.255
R1(config-if)# end
R1# show ip protocols | include Router ID
	Router ID 1.1.1.1
R1#
```
## Explicitly Configure a Router ID
![[Pasted image 20260731091044.png]]
```
R1(config)# router ospf 10
R1(config)# router-id 1.1.1.1
R1(config)# end
*May 23 19:33:42.689: %SYS-5-CONFIG_I: Configured from console by console
R1# show ip protocols | include Router ID
Router ID 1.1.1.1
R1#
```
## Modify a Router ID
- After a router selects a router ID, an active OSPF router does not allow the router ID to be changed until the router is reloaded or the OSPF process is reset.
```
R1# clear ip ospf process
```
# Router IDs
- An OSPF router ID is a 32-bit value, represented as an IPv4 address.
- Every router requires a router ID to participate in an OSPF domain
- The router ID can be defined by an administrator or automatically assigned by the router
- The router ID is used by an OSPF-enabled router to do the following:
	- Participate in the synchronization of OSPF database
	- Participate in the election of the designated router (DR)
# Router ID Order of Precedence
Cisco routers derive the router ID based on one of three criteria in the following preferential order:
1. The router ID is explicitly configured
2. The router ID is not explicitly configured
3. No loopback interfaces are configured, then the router chooses the highest active IPv4 address
![[Pasted image 20260731085528.png]]
