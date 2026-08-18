(https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-61r2.pdf)
# Identifying an Incident
## Incident Recognition and Response
- Is a set of information, security policies and procedures that you can use to identify, contain and eliminate attacks
- Enables an organisation to quickly detect and halt attacks
- Help minimize damage and prevent future attacks
## Recognizing Incidents
- **Not all events are incidents in need of immediate remedy**
- Examples:
	- Logging in from a remote location
	- Failing hard drive that is still fully operational
	- Employee trying to access resources that they shouldn't access
## Phase 1: Discovery and Recognition
- Incident identification, logging and categorization
- Incident notification and escalation
- Investigation and diagnosis
## Phase 2: Resolution and Recovery
- Forensic isolation
- Stage a fix
- Deploy the fix
- Incident closure
# AWS Services that support Phase 1
| **Service**         | **Description**                                                      |
| ------------------- | -------------------------------------------------------------------- |
| AWS Trusted Advisor | Inspects your environment and makes recommendations                  |
| Amazon CloudWatch   | Displays metrics about every AWS service you use                     |
| Amazon Inspector    | Vulnerability management service                                     |
| Amazon GuardDuty    | Continuous security monitoring                                       |
| AWS Shield          | Automatically protects network from DDOS                             |
| AWS Config          | Monitoring and assessment service for resources \| Change Management |
![[Pasted image 20260527083443.png]]
# AWS Services that support Phase 2
| **Service**         | **Description**                                                                         |
| ------------------- | --------------------------------------------------------------------------------------- |
| AWS Systems Manager | Helps keep your environment operational                                                 |
| AWS CloudFormation  | Provides the ability to create a template that describes all the AWS resources you want |
**Event-Driven Responses**

| **Service**                        | **Description**                                                              |
| ---------------------------------- | ---------------------------------------------------------------------------- |
| Amazon Simple Notification Service | Sends notification from the cloud based on events                            |
| AWS Step Functions                 | Used to distribute applications and automate IT and business processes       |
| AWS Lambda                         | Event-driven compute service that provides the ability to run code on demand |
![[Pasted image 20260527083427.png]]![[Pasted image 20260527083458.png]]
1. The instance is removed from its Auto Scaling group, and a snapshot is created of any attached Amazon Elastic Block Store (Amazon EBS) volumes.
2. The instance is isolated by removing all its previously associated security groups. Then, a new forensics security group is assigned to the instance with no inbound or outbound permissions.
3. A CloudFormation template is used to create a new environment, including a new VPC that contains a forensics instance with prebuilt tools attached to a copy of any volumes from the snapshots.
4. A basic forensics investigation is performed on the attached volumes.
5. A report is then generated with the results from the investigation and sent to the team through an SNS topic.
# Best Practices for Incident Handling
- Identify key personnel, external resources and tools
- Automate containment capabilities
- Develop incident response plans
- Pre-provision access and tools
- Run incident response game days