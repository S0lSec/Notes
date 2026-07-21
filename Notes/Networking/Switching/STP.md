Spanning Tree Protocol (STP) is a loop-prevention network protocol that allows for redundancy while creating a loop-free Layer 2 topology.

STP blocks paths that can cause loops, such that in a situation where two connections that go different paths but end at the same end-host exists. One of those paths will be blocked. 
![[Pasted image 20260406214240.png]]

However in the situation the path being used fails, the blocked path opens up keeping the network functioning.
![[Pasted image 20260406214251.png]]

# Spanning Tree Algorithm
1. An example Ethernet LAN with redundant connections between multiple switches
![[Pasted image 20260406214511.png]]
2. Select the Root Bridge
![[Pasted image 20260406214541.png]]
3. Block redundant paths
![[Pasted image 20260406214600.png]]
4. Loop-free topology
5. Link failure causes recalculation
# Commands
`show spanning-tree vlan num` - Shows spanning-tree information for specific VLAN