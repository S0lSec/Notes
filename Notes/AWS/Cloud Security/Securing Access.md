# Shared Responsibility Model
![[Pasted image 20260429103728.png]]
- Customer is responsible for security in cloud
- AWS is responsible for security of the cloud
## IAM Fundamentals
**(Identity and Access Management)**
- Securely shares and controls individual and group access to your AWS resources
- Integrates with many other AWS services
- Supports federated identity management
- Supports granular permissions
- Supports multi-factor authentication
- Provides identity information for assurance

**IAM provides authentication and authorization**
- Who is requesting access?
- What can they do?
## Overview
**User**
A person/application that can authenticate with an AWS account

**Group**
Collection of IAM users who are granted identical authorization

**Role**
Identity used to grant a temporary set of permissions to make AWS service requests

**IAM Policy**
Document that defines which resources can be accessed and the level of access to each resource
## Terminology
- **IAM entity:** Users and roles
- **IAM identity:** Used to identify and group
- **IAM resource:** Resources stored in IAM
- **Principal:** Person/application that uses the AWS account root user
## Requests
Requests are made any time a principal attempts to use the AWS Manage Console, API or AWS CLI.
## Service endpoints
- To connect to an AWS service use the URL of the entry point (aka the endpoint)
- The AWS software development kits (SDKs) and AWS CLI use the default endpoint for each service
- You can specify alternate endpoints for API requests based on configuration requirements
# Authenticating with IAM
## IAM Roles
- Provides temporary security credentials
- Not uniquely associated with one person
- A person/application/AWS service can assume a role
- Often used for delegation
- The AWS Security Token Service (STS) issues temporary security credentials
## IAM Credentials for Authentication
- Username + Password (console access)
- Access key ID + secret access key (programmatic/API access)
# Authorizing with IAM
## Principle of Least Privilege
- Grant minimum permissions that are needed
- Grant addition access as needed
## Managed and Inline IAM Policies
**Managed**
- Standalone, identity-based policies
- Can be attached to multiple users, groups and roles
- **Features:**
	- Reusability
	- Central change management
	- Versioning and rollback
	- Permissions management that can be delegated to others
	- Provides the use of permissions boundaries
**Inline**
- Embedded in a principle entity
- Can use the same policy for multiple entities but those entities do not share the policy. They all have their own copy of the policy
## Evaluation Logic for IAM Policies
![[Pasted image 20260429110346.png]]
# Additional Authentication and Access Management Services
## Identity Federation
- A system of trust between two parties to authenticate users and convey information that is needed to authorized resource access
	- Identity provides are responsible for user authentication
	- Service providers are responsible for resource access
- Two AWS services are available to provide federation to AWS account and applications
	- AWS Single Sign-On (AWS SSO)
	- AWS Identity and Access Management (IAM)
## AWS SSO
- Create or connect identities once and manage access centrally across your AWS accounts
- Provides a unified administration experience
- Users are provided a user portal to access all their assigned AWS accounts or cloud applications
- You can flexibly configure access to run parallel to or replace AWS account access management by using IAM
## AWS Directory Service
- For AD, also called AWS Managed Microsoft AD
- Facilitates directory-aware workloads and AWS resources to use managed AD in the AWS Cloud
- Provides the ability to extend your existing AD to AWS by using your existing on-premises user credentials to access cloud resources
- Supports AD SSO to AWS applications by using a single set of credentials
## Amazon Cognito
- Integrates user sign-up, sign-in and access control with web and mobile applications
- Provides a secure identity store that can scale to millions of users with Amazon Cognito user pool
- Offers user sign-in through enterprise identity providers and social identity providers
- Provides the ability to create unique identities for your users and federate them with identity providers through Amazon Cognito identity pools
## AWS Organizations
- Account management service that you can use to consolidate multiple AWS accounts into a centrally managed organization
- Includes account creation and management as well as consolidated billing capabilities
- Provides for hierarchical grouping of accounts 
- Supports centralized policy control over AWS services and API actions using service control policies (SCPs)
- Integrates with IAM and other services