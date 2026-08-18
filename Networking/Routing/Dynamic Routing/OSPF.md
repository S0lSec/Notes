# Open Shortest Path First
![[Pasted image 20260807082714.png]]
- Area - Logical Grouping of Routers
- All areas must go back to area 0 to prevent loops
- Not a requirement but starting with Area 0 is good practice
- Keep in mind not to overwhelm routers when designing area
# OSPF Neighbors
- Link State Advertisements (LSAs) is just routers learning of one another's existence
- Runs directly over IPv4 using IP protocol number 89 (reserved by IANA)
- Both routers must be running OSPF
- Hello packets advertise OSPF parameters, which **must match** for a neighbor relationship to form
- Knowledge of existing routers are stored in the Link-State Database (LSDB), storing each routers LSA
- If a neighbor fails, OSPF floods updated LSAs and re-runs the SPF algorithm
- New routers are dynamically discovered using Hello packets
# LSA Flooding & Link State Database![[Pasted image 20260807083206.png]]
- Routers flood Link State Advertisements (LSAs) to all OSPF neighbors
- Because of LSA flooding, all routers in the same OSPF area have an identical LSDB
- The Link State Database (LSDB) is a collection of all received LSAs, representing the network topology
![[Pasted image 20260807083230.png]]
# Identical LSDB Across Routers
- LSDB can span across a wide geographical area
![[Pasted image 20260807083624.png]]
# SPF Algorithm: Determining Routers
- LSA flooding ensures all routers in the area have an identical LSDB
- LSDB describes the complete network topology, but does not directly list the routes that should be added into the routing table
- Each router independently applies the SPF (Shortest Path First) algorithm to is LSDB to calculate the best paths
- SPF calculates the best-loop free routers and adds those routes to the IP routing table
![[Pasted image 20260807085039.png]]
# OSPF Operational Phases
1. Routers form adjacencies
	`R1# show ip ospf neighbor`
![[Pasted image 20260807085309.png]]
2. Routers synchronise their LSDB via exchanging LSAs
	`R1# show ip ospf database`
3. Routers run the SPF on the LSDB and add the best routes to the routing table
	`R1# show ip route`
![[Pasted image 20260807085354.png]]
# OSPF Router ID
## How OSPF Selects its Router ID
- Manually configured Router ID (**USE `router-id` COMMAND**)
	- `R1(config-router)# router-id 0.0.0.1`
- If not manually set, OSPF chooses the highest IP address on any loopback interface (e.g `192.168.10.10` > `172.20.20.10`)
- If no loopback interfaces exist, OSPF uses the highest IP address on any active physical interface
- OSPF picks its Router ID when the OSPF process starts or router reloads
- Any change afterward takes effect only after restarting the OSPF process
![[Pasted image 20260807090011.png]]
# OSPF DR & BDR Election (Broadcast Networks)
- OSPF elects a designated router and backup designated router
- Other routers form full adjacency only with the DR and BDR and remain in 2-way state with each other
- DR & BDR is assigned per network segment, not per router
- If you have only 2 routers configure them as a point-to-point network
## Election Process
- OSPF elects a DR & BDR
- Priority:
	- The highest OSPF interface priority wins
	- Priority range: 0 - 255
	- Default priority: 1
	- If priorities are equal the router with the highest ID will be chosen
- Routers wait 40s after config then starts the election process
```
R1(config)# interface gig0/0
R1(config-if)# ip ospf priority 100
```
# OSPF Neighbor States
- **FULL/-** Neighbor state is full. The line does not use DR/BDR
- **FULL/DR** Neighbor state is full. Neighbor is a DR
- **FULL/BDR** Neighbor state is full. Neighbor is a BDR
- **FULL/DBROTHER** Neighbor state is full. Neighbor is not DR/BDR
- **2WAY/DROTHER** Neighbor state is 2-WAY. Neighbor is not DR/BDR
`R1# show ip ospf neighbor`
![[Pasted image 20260814083834.png]]
# OSPF Passive Interfaces
- OSPF enabled on interface, router looks for OSPF neighbors
- Sends **Hello** message from other routers
- Also listens for hello messages
- If no other routers exist on the link:
	- Do not advertise hello messages
	- Do no receive hello messages
	- Still advertise the subnet
```
R1(config)# router ospf 1
R1(config)# passive-interface Gig0/0
```
# OSPF Default Routes
- **Internal Routing**: All routers learn specific routers to internal company subnets through OSPF, so no default route is needed for internal traffic.
- **Internet Access**: The router connected to the internet has a default route to the ISP and injects this default route into OSPF, allowing all routers to dynamically learn and use it for external traffic
![[Pasted image 20260814093238.png]]
```
R2(config)# ip route 0.0.0.0 0.0.0.0 1.2.3.4
R2(config)# router ospf 1
R2(config-router)# default-information originate
```
# Hello & Dead Intervals
- **Hello Interval**: How often a router sends Hello message
- **Dead Interval**: How long a router waits for a Hello message before declaring the neighbor down
```
!Does not need to be configured

R1(config)# interface g0/0
R1(config-if)# ip ospf hello-interval 5
R1(config-if)# ip ospf dead-interval 15
```
# OSPF Cost
- OSPF uses cost to determine the best path.
- OSPF calculates the cost via reference bandwidth / interface bandwidth.
- **Change the reference bandwidth to your fastest link or higher**
```
R2(config)# router ospf 1
R2(config-router)# auto-cost reference-bandwidth 1000
```
# Loopbacks
- OSPF will not advertise loopbacks as a network instead they will be advertised as a /32
- To simulate a real LAN configure the loopback as a point-to-point network
```
R1(config)# interface loopback 1
R1(config-if)# ip ospf network point-to-point
```
# Configuration
![[Pasted image 20260807091242.png]]
```
! Perth
Perth(config)# router ospf 1
Perth(config)# router-id 0.0.0.1
Perth(config)# network 172.16.10.0 0.0.0.255 area 0
Perth(config)# network 10.10.10.0 0.0.0.3 area 0
```

```
! Sydeny
Perth(config)# router ospf 1
Perth(config)# router-id 0.0.0.2
Perth(config)# network 182.168.10.0 0.0.0.255 area 0
Perth(config)# network 10.10.10.0 0.0.0.3 area 0
```

`router id` - Not an IP address
`network` - Enable the OSPF process on all interfaces that have an IP address
`0.0.0.255` - Used to specify what part of the network address must match
![[Pasted image 20260807091643.png]]![[Pasted image 20260807091647.png|257]]
**If you forget to assign a Router ID** run `clear ip ospf process` to stop and reset the ospf process

Set router as default gateway - `R1(router-config)# default-information originate`
Show LSADB - `show ip ospf database`

Reset OSPF - `clear ip ospf process`
# Troubleshooting
Show OSPF information - `show ip ospf brief`
Show neighbours - `show ip ospf neighbor`
**Check matching**
1. Subnet
2. Area number
3. Hello Timer
4. Dead timer
5. Network type