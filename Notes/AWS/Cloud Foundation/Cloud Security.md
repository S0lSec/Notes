# Section 1: AWS Shared Responsibility Model
![](/Images/aws_shared_responsibility_model.png)
## AWS Responsibility: Security *of* the Cloud
- Physical security of data centers
- Hardware and software infrastructure
- Network infrastructure
- Virtualization infrastructure
![](/Images/security_of_the_cloud_AWS.png)
## Customer Responsibility: Security *in* the Cloud
- Patching and maintenance of operating systems (virtual machines, etc)
- Applications, using strong passwords, role-based access, etc
- Security group configuration
- OS or host-based firewalls
- Network configuration
- Account management
![](/Images/security_in_the_cloud_AWS.png)
## Service Characteristics and Security Responsibility
### Infrastructure as a Service (IaaS)
![](/Images/services_managed_by_customer_AWS.png)
**Managed by customer**
- Customer has more flexibility over configuring networking and storage settings
- Customer is responsible for managing more aspects of the security
- Customer configures the access controls
### Platform as a service (PaaS)
![](/Images/services_managed_by_AWS_AWS.png)
**Managed by AWS**
- Customer does not need to manage the underlying infrastructure
- AWS handles the operating system, database patching, firewall configuration, and disaster recovery
- Customer can focus on managing code or data
### Software as a service (SaaS)
**Managed by customer**
- Software is centrally hosted
- Licensed on a subscription model or pay-as-you-go basis.
- Services are typically accessed via web browser, mobile app, or application programming interface (API)
- Customers do not need to manage the infrastructure that supports the service
![](/Images/saas_examples_AWS.png)
# Section 2: AWS Identity and Access Management (IAM)
- Used to manage access to AWS resources
- Uses access rights to determine who can access what
	- **Who** can access
	- **Which** resource can they access
	- **How** can they access it
- IAM can be applied through/to users, groups, policies and roles
**IAM Policy Example**
![](/Images/IAM_policy_example_aws.png)
# Section 3: Securing a new AWS account
- **DO NOT USE ROOT ACCOUNT UNLESS NECESSARY**
- Actions that require root account:
	- Updating root user password
	- Changing AWS support plan
	- Restoring IAM users permissions
	- Change account settings
	
To stop using the account root user, take the following steps:
1. While you are logged into the account root user, create an IAM user for yourself with AWS Management Console access enabled (but do not attach any permissions to the user yet). Save the IAM user access keys if needed.
2. Next, create an IAM group, give it a name (such as FullAccess), and attach IAM policies to the group that grant full access to at least a few of the services you will use. Next, add the IAM user to the group.
3. Disable and remove your account root user access keys, if they exist.
4. Enable a password policy for all users. Copy the IAM users sign-in link from the IAM Dashboard page. Then, sign out as the account root user.
5. Browse to the IAM users sign-in link that you copied, and sign in to the account by using your new IAM user credentials.
6. Store your account root user credentials in a secure place.
