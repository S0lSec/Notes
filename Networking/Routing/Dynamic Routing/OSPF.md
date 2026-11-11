OSPFv2 - IPv4
OSPFv3 - IPv6
# OSPF components
## Routing Protocol Messages
- Hello packet (discover neighbours & keep relationships alive)
- Database description packet (Used to summarise their LSDB)
- Link-state request packet (Used to request full LSA)
- Link-state update packet (Response to LSR)
- Link-state acknowledgement packet (Used to acknowledge response)
## Data Structures
The routing protocol messages are used to maintain 3 databases:
- **Adjacency database** - Neighbour table
- **Link-state database (LSDB)** - Topology table
- **Forwarding database** - Routing table
# Link-State Operation
OSPF routers complete a generic link-state routing process to reach a state of convergence.
Each link between routers is labelled with a cost value, which is used to determine the best path.

## **Link-state routing steps:**
### 1. Establish neighbour Adjacencies
- OSPF routers must recognise each other before sharing information
- OSPF sends Hello packets out all interfaces
- If a neighbour is present the router attempts to establish a neighbour adjacency
### 2. Exchange link-state advertisement
- Once adjacencies are established the router will exchange LSAs
- LSAs contain the state and cost of each directly connected link
- Routers flood their LSAs to adjacent neighbours
- The neighbours receiving the LSAs will then flood the LSAs to the other directly connected neighbours
### 3. Build the link state database
- Once LSAs are received the routers build the topology table (LSDB)
- The database eventually holds all the information about the topology
### 4. Execute the SPF algorithm
- Router then execute the SPF algorithm which creates the SPF tree
### 5. Choose the best route
- Once the SPF tree is built the best paths to each network are offered to the IP routing table
# Single-Area and Multi-area OSPF
An OSPF area is a group of routers that share the same link-state information in their LSDBs.

**Single-Area OSPF**: All routers are in one area (best practice to use area 0)
**Multi-area OSPF**: OSPF is implemented using multiple areas, in a hierarchical fashion. All areas must connect to the backbone area (area 0)

Multi-area advantages:
- Smaller routing tables
- Reduces link-state update overhead
- Reduced frequency of SPF calculations
# OSPF Packets
1. **Hello packet** - Discovers neighbours
2. **Database Description (DBD) packet** - Checks for database synchronisation between routers
3. **Link-State Request (LSR) packet** - Requests specific link-state records from router to router
4. **Link-State Update (LSU) packet** - Sends specifically requested link-state records
5. **Link-State Acknowledgement (LSAck) packet** - Acknowledges the other packet types
# Operational States
| **State** | **Description**                                                                                                                                                |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Down      | - No Hello packets received<br>- Router sends Hello packets<br>- Transition to Init state                                                                      |
| Init      | - Hello packets are received from the neighbour<br>- They contain the Router ID of the sending router<br>- Transition to Two-Way state                         |
| Two-Way   | - Communication between the two routers is bidirectional<br>- On multi-access links the routers elect a DR and BDR<br>- Transition to ExStart state            |
| ExStart   | - On point-to-point networks, the two routers decide which router will initiate the DBD packet exchange and decide upon the initial DBD packet sequence number |
| Exchange  | - Routers exchange DBD packets<br>- If additional router information is request then transition to Loading; otherwise transition to Full state                 |
| Loading   | - LSRs and LSUs are used to gain additional route information<br>- Routes are processed using the SPF algorithm<br>- Transition to the Full state              |
| Full      | The link-state database of the router is fully synchronised                                                                                                    |
# Establish Neighbour Adjacencies
1. Down State to Init State
	Once OSPF is enabled the enabled interface transitions from the down state to the init state. The router starts sending out Hello packets out all OSPF enabled interfaces.
2. The Init State
	The other router receives the Hello packet and adds the router ID to its neighbour list. It then proceeds to send a Hello packet back. 
3. Two-Way State
	The router receives the Hello packet and adds it router ID to the list of neighbours.
4. Elect the DR and BDR
	Because both routers are interconnected over an Ethernet network a DR and BDR election takes place.
# Synchronising OSPF Database
1. Decide first router
	In the ExStart state the two routers decide which router will send the DBD packet first. The router with the higher router ID will be the first router to send DBD packet during the Exchange state.
2. Exchange DBDs
	In the exchange state, the two routers exchange one or more DBD packets. Basically providing a summary of their LSDB.
3. Send an LSR
	The LSDB are synchronised by sending each other information on networks.
# The Need for a DR
Mutli-access networks can cause flooding of LSAs. 