# Security Groups
![[Pasted image 20260513103337.png]]
- Have rules that control inbound and outbound instance traffic
- Default security groups deny all inbound traffic and allow all outbound traffic
# Network ACLs
![[Pasted image 20260513103517.png]]
- Has separate inbound/outbound rules
- Stateless
- Each VPC automatically comes with a modifiable default network ACL
- By default all inbound & outbound IPv4 traffic is allowed
- Can create custom network ACL and associate with a subnet
# Compare Security Groups and Network ACLs

| **Attribute**       | **Security Groups**                                                | **Network ACLs**                                                               |
| ------------------- | ------------------------------------------------------------------ | ------------------------------------------------------------------------------ |
| **Scope**           | Instance or interface level                                        | Subnet level                                                                   |
| **Supported Rules** | Allow rules only                                                   | Allows and deny rules                                                          |
| **State**           | Stateful                                                           | Statelss                                                                       |
| **Order of Rules**  | All rules are evaluated before a decision is made to allow traffic | Rules are evaluated in number order before a decision is made to allow traffic |
# VPC Security Features
![[Pasted image 20260513103840.png]]
# Load Balancers
## ELB
- Distributes incoming application traffic
- Supports high availability
- Performs health checks on instances
- Provides the following:
	- ALB
	- NLB
	- CLB
## Data protection in ELB
![[Pasted image 20260513104006.png]]
**Single point of contact**
A load balancer serves as the single point of contact for clients
## Load Balancers in Action
![[Pasted image 20260513104110.png]]
# Best Practices to Protect Your Network
- Control traffic at all layers
- Inspect and filter your traffic at the application level
- Automate network protection
- Limit exposure
# Protecting your Compute Resources
## Amazon Inspector
- Run automated security assessments on EC2 instances and applications
- Identify application security issues
- Enforce security standards and best practices
- Generate assessment reports
### Security Benefits
- Automate tasks to help you respond to security issues
- Regularly monitor your resources
- Benefit from AWS security expertise
- Integrate security into DevOps
## AWS Systems Manager
- Amazon Inspector uses AWS Systems Manager Agent (SSM Agent) to collect the software inventory and configurations from your EC2 instances
- The collected application inventory and configurations are used to assess workloads for vulnerabilities