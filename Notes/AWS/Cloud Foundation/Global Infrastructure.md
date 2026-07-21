# Section 1: AWS Global Infrastructure
The AWS global infrastructure is designed and built to deliver a flexible, reliable, salable and secure cloud computing environment with high-quality global network performance
## Regions
- A geographical area
- Data replication across regions is controlled by you
- Communication between regions uses AWS backbone network infrastructure
- Each region provides full redundancy and connectivity to the network
- Typically consists of two or more **availability zones**

Select a region by determining:
1. Data governance
2. Legal requirements
3. Latency
4. Services available within the region
5. Costs
## Availability Zones
- Each region has multiple availability zones
- Availability zones are fully isolated partition of the AWS infrastructure
- Consist of discrete data centers
- Designed for fault isolation
- Interconnected with other availability zones by using high-speed private networking
- Recommended to replicate data + resources across availability zones for resiliency
## Data Centers
- Designed for security
- Where the data resides and data processing occurs
- Each data center has redundant power, networking, connectivity and is housed in a separate facility
## Points of Presence 
- AWS provides global network of Points of Presence locations
- Consists of edge locations and a much smaller number of Regional edge caches
- Used with Amazon CloudFront
	- A global content delivery network that delivers content to the end users with reduced latency
- Regional edge caches used for content with infrequent access
![](/Images/points_of_presence.png)
## Infrastructure Features
- Dynamic adaption of capacity
- Adapts to accommodate growth
- Continues operating properly in the presence of failure
- Built-in redundancy of components
- High level of operational performance
- Minimized downtime
- No human intervention
# Section 2: AWS Services and Service Category
## Foundational Services
- Compute
- Networking
- Storage
## Storage Services
- Amazon Simple Storage Service (S3)
- Amazon Elastic Block Store (EBS)
- Amazon Elastic File System (EFS)
- Amazon Simple Storage Service Glacier
## Compute Services
- Amazon EC2
- Amazon EC2 Auto Scalling
- Amazon Elastic Container Service (ECS)
- Amazon EC2 Container Registry
- AWS Elastic Beanstalk
- AWS Lambda
- Amazon Elastic Kubernetes Service (EKS)
- AWS Fargate
## Database Services
- Amazon Relational Database Service
- Amazon Aurora
- Amazon Redshift
- Amazon DynamoDB
## Networking/Content Delivery Services
- Amazon VPC
- Elastic Load Balancing
- Amazon CloudFront
- AWS Transit Gateway
- Amazon Route 53
- AWS Direct Connect
- AWS VPN
## Security, Identity and Compliance Services
- AWS Identity and Access Management (IAM)
- AWS Organizations
- Amazon Cognito
- AWS Aritfact
- AWS Key Management Service
- AWS Shield
## Cost Management Services
- AWS Cost and Usage Report
- AWS Budgets
- AWS Cost Explorer
## Management and Governance Services
- AWS Management Console
- AWS Config
- Amazon CloudWatch
- AWS Auto Scaling
- AWS Command Line Interface
- AWS Trusted Advisor
- AWS Well-Architected Tools
- AWS  CloudTrail