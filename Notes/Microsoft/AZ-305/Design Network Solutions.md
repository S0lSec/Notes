# Recommend a network architecture solution based on workload requirements
## Network Requirements
- Naming
- Regions
- Subscriptions
- IP addresses
- Segmentation
- Filtering
## Considerations when defining workload requirements
- Segmentation options for your virtual network
- Required interfaces and IP address
- Network security groups
- Network traffic routing
## Best Practices
- **Plan IP addressing for virtual networks**
	- Assign an address space that isn't larger than a CIDR range of /16 for each virtual network
	- Don't overlap virtual network address space with on-premises network ranges
- **Implement hub-spoke network topology**
	- A hub and spoke network topology isolates workloads while sharing services
	- The hub is an Azure virtual network that acts as a central point of connectivity
	- The spokes are virtual networks
	- Implement a hub-spoke topology in Azure to centralize common services
	- Use spoke virtual networks to isolate workloads with each spoke manage separately from others
	- Configure hub and spoke virtual networks in different resource groups and even in different subscriptions
![[Pasted image 20260421220732.png]]

# Design patterns for Azure network connectivity services
## Pattern 1: Single virtual network
- All components are placed in a single virtual network
- Possible if operating in a single region
- Use NSGs to create segments
- Use ASGs to simplify administration
![[Pasted image 20260421221126.png]]
Here's how you might implement a single virtual network pattern:
- One subnet (`Subnet 1`) can contain your database workloads.
- Another subnet (`Subnet 2`) can contain your web workloads.
- To govern subnet traffic, you can implement NSGs to specify that `Subnet 1` can talk only with `Subnet 2`, and `Subnet 2` can talk to the internet.
- You can enforce segmentation by using an NVA from Azure Marketplace or Azure Firewall.
- You can modify the pattern to segment and support many different workloads.
## Pattern 2: Multiple virtual networks with peering
- Extends single virtual network to support multiple virtual networks
![[Pasted image 20260421221205.png]]
## Pattern 3: Multiple virtual networks in hub-spoke topology
- Choose a virtual network in a given region as the hub for all the other virtual networks in that region
![[Pasted image 20260421221423.png]]
## Compare Patterns
| Compare                                             | Single virtual network                                                      | Multiple networks with peering                                              | Multiple networks in hub-spoke topology                                                                                                                          |
| --------------------------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Connectivity/Routing** (how segments communicate) | System routing provides default connectivity to any workload in any subnet. | System routing provides default connectivity to any workload in any subnet. | No default connectivity between spoke virtual networks. A layer 3 router (such as Azure Firewall) in the hub virtual network is required to enable connectivity. |
| **Network-level traffic filtering**                 | Traffic is allowed by default. NSG can be used for filtering.               | Traffic is allowed by default. NSG can be used for filtering.               | Traffic between spoke virtual networks is denied by default. Azure Firewall configuration can enable selected traffic.                                           |
| **Centralized logging**                             | NSG logs for the virtual network.                                           | Aggregate NSG logs across all virtual networks.                             | Azure Firewall logs to Azure Monitor all accepted/denied traffic sent via a hub.                                                                                 |
| **Unintended open public endpoints**                | DevOps can accidentally open a public endpoint via incorrect NSG rules.     | DevOps can accidentally open a public endpoint via incorrect NSG rules.     | A spoke virtual network open port doesn't allow access. The return packet is dropped via stateful firewall (asymmetric routing).                                 |
| **Application level protection**                    | NSG provides network layer support only.                                    | NSG provides network layer support only.                                    | Azure Firewall supports FQDN filtering for HTTP/S and MSSQL for outbound traffic and across virtual networks.                                                    |

# Design outbound connectivity and routing
## Routing tables and Routes
- **System routes** - Defined for a specific location when created, can't be modified but can be overridden ![[Pasted image 20260421222410.png]]
- **User-defines routes (custom)** - The route the user created which can be used to override the default routes ![[Pasted image 20260421222506.png]]
- **Routes from other virtual networks** - When u create a virtual network peering between two virtual networks a route is added for each address range within the address space of each peered network
- **Border Gateway Protocol routes** - If your on-premises network gateway exchanges BGP routes with an Azure Virtual Network gateway, a route is added for each route propagated from the on-premises network gateway. These routes appear in the routing table as BGP routes.
- **Service endpoint routes** - The public IP addresses for certain services are added to the route table by Azure when you enable a service endpoint to the service. Service endpoints are enabled for individual subnets within a virtual network. When you enable a service endpoint, a route is only added to the route table for the subnet that belongs to this service. Azure manages the addresses in the route table automatically when the addresses change.
## Considerations
- System routes
	- Route traffic between virtual machines in the same virtual network or between peered virtual networks.
	- Support communication between virtual machines by using a virtual network-to-network VPN.
	- Enable site-to-site communication through Azure ExpressRoute or an Azure VPN gateway.
- User defined routes
	- Enable filtering of internet traffic by using Azure Firewall or forced tunneling.
	- Flow traffic between subnets through a Network Virtual Appliance (NVA).
	- Define routes to specify how packets should be routed in a virtual network.
	- Define routes that control network traffic and specify the next hop in the traffic flow.
- Overriding routes
	- Flow through NVA
	- Forced tunneling
# Design for on-premises connectivity to Azure Virtual Network
- For a hybrid-cloud network the on-premises corporate networks need to be connected to Azure
## Services
- **Azure VPN Gateway** - Provides a VPN between the premises and Azure
- **Azure ExpressRoute** - Uses a private dedicated connection through a non-Microsoft connectivity provider
- **Azure Virtual WAN and hub-spoke networks** - Having Azure as the hub with services branching off and the premises connects to the hub
# Choose an application delivery service
## Load Balancing
When selecting a load balancing service consider:
- Traffic type
- Global vs regional
- Availability
- Cost
- Features and limits
## Considerations when choosing load balancing
![[Pasted image 20260422085210.png]]
# Design for application delivery services
|Feature/Service|Azure Front Door|Application Gateway|Traffic Manager|Load Balancer|
|---|---|---|---|---|
|Type|Global CDN/ADN|Regional|Global|Regional/Global|
|Layer|Layer 7 (HTTP/HTTPS)|Layer 7 (HTTP/HTTPS)|DNS-based|Layer 4 (TCP/UDP)|
|Primary Use Case|Web traffic load balancing, application acceleration, global routing, and CDN content delivery|Web application firewall, TLS/SSL termination, and HTTP load balancing|DNS-based traffic routing for high availability and performance|Internal and external load balancing for non-HTTP(S) traffic|
|Key Features|Path-based routing, TLS/SSL offload, Web Application Firewall (WAF), URL-based routing, CDN/edge caching|Path-based routing, TLS/SSL offload, Web Application Firewall (WAF), URL-based routing|DNS-based routing, geographic routing, priority routing, weighted routing|High availability, low latency, zonal and zone-redundant endpoints|
|Scalability|High|High|High|High|
|Cost|Based on data processed and rules applied|Based on data processed, rules applied, and SKU|Based on DNS queries, health checks, and data points processed|Based on rules and data processed|
The different load balances can work together in your networking architecture
![[Pasted image 20260422085357.png]]
## Azure Front Door
- Lets you define, manage and monitor global routing for web traffic
- Global fail over for high availability
## Azure Traffic Manager
- DNS-based traffic load balancer that enable you to distribute traffic to servers across global Azure regions
- Increase application availability
- Improve application performance
- Combine hybrid applications
- Distribute traffic fro complex deployments
## Azure Load Balancer
- Provides high-performance, low-latency layer 4 load-balancing for all UDP/TCP protocols
- Mange inbound + outbound connections
- Configure public and internal load-balanced endpoints
- Manage service availability by mapping inbound connections to back-end pool destinations
## Azure Application Gateway
- Web traffic load balancer
- Application Delivery Controller (ADC) as a service, offering layer 7 load-balancing capabilities
- Path-based routing
- Multiple-site routing

# Design for application protection services
## Azure DDoS Protection
- Implement always-on traffic monitoring, adaptive tuning, and mitigation scale.
- Access multi-layered protection, including attack analytics, metrics, and alerting.
- Network protection with centralized management and Rapid Response support.
- IP protection for individual workloads or cost-sensitive architectures.

**Tiers**
- **DDoS Network Protection**: VNet-level protection plan covering multiple resources, includes DDoS Rapid Response support and cost protection guarantees
- **DDoS IP Protection**: Pay-per-protected-IP model, no protection plan required, suitable for individual workloads.
## Azure Private Link
- Enables you to access Azure PaaS services and Azure hosted customer-owned/partner services over a private endpoint in your virtual network
- Enable private connectivity to services on Azure.
- Integrate with on-premises and peered networks.
- Restrict traffic to the Microsoft network with no public internet access.
## Azure Firewall
- Implement centralized creation, enforcement, and logging of application and network connectivity policies.
- Apply connectivity policies across subscriptions and virtual networks.
- To restrict access to your virtual machine management ports, combine Azure Firewall rules with just in time (JIT) access.

**Tiers**
- **Basic**: Limited features, alert-only threat intelligence (not recommended for production).
- **Standard**: Full stateful firewall, FQDN filtering, threat intelligence, log analytics.
- **Premium**: Adds TLS inspection, IDPS with 67,000+ signatures, URL filtering, web categories, scales to 100 Gbps, PCI DSS compliance.
## Azure Web Application Firewall
- Protects your web applications from common web exploits and vulnerabilities
- React faster to security threats by centrally patching known vulnerabilities instead of securing individual web apps.
- Deploy Web Application Firewall with Application Gateway, Front Door, and Content Delivery Network.
## Azure Network Security Groups
- Filter network traffic to and from Azure resources in an Azure virtual network
- Use Access Control List (ACL) rules to control traffic
- Control how Azure routes traffic from subnets.
- Limit the users in an organization who can work with resources in virtual networks.
- Restrict traffic to an individual NIC by associating an NSG directly to a NIC.
- Combine NSGs with JIT access to restrict access to your virtual machine management ports.