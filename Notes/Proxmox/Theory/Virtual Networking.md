# Role of Networking in the SDDC
Nodes and storage need a network that links them together

Networking refers to the configuration and management of both physical and virtual networking. This includes:
- Setting up network interfaces
- Creating bridges
- Setting up VLANs
- Configuring firewalls
# Essential Components
PVE admins create a **Software-Defined Network**, which simplifies advanced networking configurations. This allows segmentation and wider control.

- **Zones** - virtually separated regions in the network
- **Cluster Network** - used for internal cluster communication
- **Storage Network** - all storage-related traffic uses this network to avoid congesting other networks
- **Internal Network (LAN)** - private network where VMs, CTs and nodes can communicate with each other
- **External Network (WAN)** - allows the environment to connect to the internet
- **Virtual Network**
	- Connects VMs/CTs and allows them to interact
	- Commonly done via a Linux bridge (vmbr0)
	- Provides isolated, logical networking and features such as VLAN tagging for further segmentation
- **Subnet**
	- A subset of IP addresses inside a large network used to organize and allocate IP addresses efficiently
	- Each object is given an IP address, which allows discovery and communication with them
# Network Connections
**Linux Options:**
- **Bridge**: Acts like a virtual switch to connect VMs to the physical network. Allows communication through a virtual interface
- **Bond**: Combines multiple physical NICs into a single logical NIC. Increasing redundancy and bandwidth
- **VLAN**: A way of segmenting networks where each one is identified with a unique tag to ensure isolation and correct traffic
**OVS Options**:
- **Bridge**: Provides advanced VLAN handling, traffic shaping and flow control. Used for high-performance vNets
- **Bond**: Similar to Linux Bond but provides high control and greater performance
- **IntPort**: Virtual interface created inside an OVS Bridge. Used to connect hosts to the OVS network
# Linking VMs to Linux Bridges
**Manually**
1. Create the Linux Bridge
2. Go to the VMs networking tab
3. Link it to the desired bridge
**Automated**
```
for VMID in 100 101 102 103; do​
	qm set $VMID --net0 virtio, bridge=vmbr0​
done
```
**VMID** = the selected ID from the list of VMIDs to bulk link​
**qm** = PVE’s standard command to work with VMs​
**--net0** = the VM’s network interface name​
**virtio** = network driver type used by the VM​
**bridge=vmbr0** = sets the bridge to the one that we just created​
# PVEs Link Aggregation Protocol (LACP)
- Linux Bonds allow LACP to be configured, giving the admin a series of benefits:
	- Aggregates multiple physical network ports into a single virtual port
	- Creates redundant networks to prevent failover
![[Pasted image 20260514133559.png]]
# Linux Bond Modes
| **​**                | **Function​**                                                    | **Use Case​**                                |
| -------------------- | ---------------------------------------------------------------- | -------------------------------------------- |
| **balance-rr​**    | Transmits packages in sequential order ​                         | Provides load balance and fault tolerance​   |
| **active-backup​** | If one interface fails, the other one kicks in​                  | Provides redundancy​                         |
| **balance-xor​**   | Sends packages with same destination through the same interface​ | Provides load balancing and fault tolerance​ |
| **broadcast​**     | Sends all traffic to all interfaces​                             | Full redundancy, but no load balancing​      |
| **802.3ad/LACP​**  | Dynamically groups interfaces to act as one​                     | Requires a switch that supports LACP​        |
| **balance-tlb​**   | Balance outgoing traffic based on current load​                  | Only balances outgoing traffic​              |
| **balance-alb​**   | Inbound and outbound traffic load balancing​                     | Balances both directions​                    |
