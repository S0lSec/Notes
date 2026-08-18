# Amazon Elastic Block Store (EBS)
- Provide persistent block storage volumes for use with EC2 instances
- Each volume is automatically replicated within its AZ
- Block storage you can change one block of data.
	- Object storage the entire file must be updated
- Can create individual storage volumes and attach them to an EC2 instance
- Automatically replicated within its AZ
- Can be backed up automatically to S3
## EBS Volume Types
![[Pasted image 20260530114154.png]]
## EBS Volume Use Cases
![[Pasted image 20260530114216.png]]
## EBS Features
- Snapshots
- Encryption
- Elasticity
## EBS Pricing
**Volumes**
- EBS volumes persist independently from the instance
- All volume types are charged by the amount that is provisioned per month
**IOPS**
- **General Purpose SSD**: Charged by the amount that you provision in GB per month
- **Magnetic**: Charged by the number of requests to the volume
- **Provisioned IOPS SSD**: Charged by the amount that you provision in IOPS
**Snapshots**
- Added cost of EBS snapshots to S3 is per GB month of data stored
**Data transfer**
- Inbound data transfer is free
- Outbound data transfer across Regions incurs charges
# Amazon Simple Storage Service (S3)
- Data is stored as objects in buckets
- Virtually unlimited storage
	- Single object is limited to 5 TB
- Designed for 11 9s of durability
- Granular access to buckets and objects

- Redundantly stored in the Region
- Designed for seamless scaling
- Access the data anywhere
## S3 Storage Classes
**Highest availability and most frequent access**
- Standard
- Intelligent-Tiering
- Standard-Infrequent Access
- One Zone-Infrequent Access
- Glacier
- Glacier Deep Archive
**Lowest availability and infrequent access**
## Pricing
- Pay only for what you use
- Do not pay for:
	- Transfers IN to S3
	- Transfer OUT from S3 to Cloudfront or EC2 in the same region
# Amazon Elastic File System (EFS)
- Good for big data and analytics, media processing workflows, content management and home directories
- Petabyte-scale, low-latency file system
- Shared storage
- Elastic capacity
- Supports NFS version 4.0 & 4.1
- Compatible with all Linux-based AMIs for Amazon EC2
## EFS Architecture
![[Pasted image 20260530115206.png]]
## EFS Implementation
1. Create EC2 resources and launch your instance
2. Create your EFS
3. Create your mount targets in the appropriate subnets
4. Connect your instance to the mount targets
5. Verify the resources and protection of your AWS account