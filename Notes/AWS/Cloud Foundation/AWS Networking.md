# Amazon VPC
- Enables you to provision a logically isolated section of the AWS Cloud where you can launch resources
- Gives you control over your virtual networking resources
- Enables you to customize network configuration for your VPC
- Enables you to use multiple layers of security

## VPCs and Subnets
**VPCs**
- Logically isolated from other VPCs
- Dedicated to your AWS account
- Belong to a single AWS Region and can span multiple Availability Zones

**Subnets**
- Range of IP addresses that divide a VPC
- Belong to a single Availability Zone
- Classified as public or private

## IP Addressing
- When creating a VPC you assign it to an IPv4 CIDR block
- Cannot change address range after creation
- Largest IPv4 CIDR block is /16
- Smallest IPv4 CIDR block is /28
- IPv6 is support with a different block size limit
- CIDR blocks of subnets cannot overlap

## Reserved IP Addresses
On a /24 network with an IP of 192.168.0.0
192.168.0.0 - Network address
192.168.0.1 - Internal communication
192.168.0.2 - DNS resolution
192.168.0.3 - Future use
192.168.0.255 - Broadcast address

## Public IP Address Types
**Public IPv4 Address**
- Manually assigned through an Elastic IP address
- Automatically assigned through the auto-assign public IP address settings at the subnet level

**Elastic IP address**
- Associated with an AWS account
- Can be allocated and remapped anytime
- Additional costs might apply

## Elastic Network Interface
- A virtual network interface that you can:
	- Attach to an instance
	- Detach from the instance and attach to another instance to redirect traffic
- Its attributes follow when it is reattached to a new instance
- Each instance in your VPC has a default network interface that is assigned a private IPv4 address from the IPv4 address range of your VPC

## Route Tables and Routes
- Route table contains a set of rules that you can configure to direct network traffic from your subnet
- Each route specifies a destination and a target
- By default every route table contains a local route for communication within the VPC
- Each subnet must be associated with a route table

# VPC Networking
## Internet Gateway
- Allows instances inside of a VPC to access the internet when a **public IP** address is allocated and a **route table** with a route to access the internet gateway.
![](/Images/internet_gateway_aws.png)
## Network Address Translation (NAT) Gateway
![](NAT_gateway_aws.png)
- NAT gateways enable instances in private subnets to connect to the internet
- NAT gateway is in public subnet
## VPC Sharing
![](/Images/VPC_sharing_aws.png)
- Enables users to share subnets with other AWS accounts in the same organization.
## VPC Peering
![](/Images/VPC_peering_aws.png)
## AWS Site-to-Site VPN
![](/Images/aws_site_to_site_aws.png)
By default, instances that you launch into a VPC cannot communicate with a remote network. To connect your VPC to your remote network (that is, create a virtual private network or VPN connection), you:
1. Create a new virtual gateway device (called a virtual private network (VPN) gateway) and attach it to your VPC.
2. Define the configuration of the VPN device or the customer gateway. The customer gateway is not a device but an AWS resource that provides information to AWS about your VPN device.
3. Create a custom route table to point corporate data center-bound traffic to the VPN gateway. You also must update security group rules. (You will learn about security groups in the next section.)
4. Establish an AWS Site-to-Site VPN (Site-to-Site VPN) connection to link the two stems
together.
5. Configure routing to pass traffic through the connection.
## AWS Direct Connect
![](/Images/aws_direct_connect.png)
- Establish a dedicated private network connection between your network and one of the DX locations.
## VPC Endpoints
![](/Images/vpc_endpoints_aws.png)
# VPC Security
**Security Groups**
- Basically firewalls
**Access Control Lists**
- Has separate inbound and outbound rules
- Stateless
# Amazon Route 53
- DNS web service
- pretty much it lol