IP Address Management is a tool used to manage and coordinate DHCP and DNS services on a network. Helping administrators plan and manage IP address space. 
**Providing**:
- IP address tracking
- Subnet management
- Discovery of devices on the network
- Documentation and auditing of IP usage
-----------------------------
**Benefits:**
- IPv4/6 address space planning and allocation
- IP address space utilization statistics and trend monitoring
- Static IP inventory management, lifetime management, and DHCP + DNS record creation and deletion
- Service and zone monitoring of DNS servers
- IP address lease and sign-in event tracking

# Four Modules of IPAM
- IPAM discovery
- IP address space management
- Multiserver management and monitoring
- Operational auditing and IP address tracking

# Centralized Topology
![697](/Images/ipam_centralized_topology.png)
# Distributed Topology
![](/Images/ipam_distributed_topology.png)
# Requirements
- IPAM server must be a member server in a domain
- IPAM server should be a single-purpose server
- IPAM server needs access to the DB
- Needs plenty of storage
# Deploy IPAM Server
1. Install IPAM server feature
2. Provision IPAM servers
3. Configure and run server discovery
4. Choose and manage the discovered servers