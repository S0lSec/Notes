# Create, Configure and manage Identities
## Users
- User account contains all information needed to authenticate the user during the sign-on process
- use the **Identity - All users** dashboard in the admin center to work with user objects
- Three kinds of users:
	- Cloud identities
	- Directory-synchronised identities
	- External users
## Groups
- **Security Groups**
	- Common
	- Manage access to shared resources for a group
	- Can be nested groups
- **Microsoft 365 Groups**
	- Access shared mailbox calendar, SharePoint and more
	- Give access to external people
	- Unable to nest within groups
- **Dynamic Groups**
	- Special type of security group
	- Membership dynamically generated via membership rule
## Devices
- **Registered Device**
	- Supports BYOD
	- Registered devices sign in using local account
	- Also attached to Entra ID account granting access to org resources
	- Control using Mobile Device Management tools like Intune
- **Joined Device**
	- Intended for cloud-first or cloud-only organisations
	- Organisation owned
	- Joined only Entra ID
	- Org account required to login
	- Conditional Access policies can be applied to the device identity
- **Hybrid Joined Device**
	- Use if:
		- You have Win32 apps deployed to these devices
		- You want to continue to use GPO to manage the device
		- You wan to use existing image solutions to deploy devices
# Licenses
Used to give users or groups access to services.
## Group-based Licensing
- Can assign one or more product licenses to a group
- Entra ID assigns to all member of the group
- New group members are automatically assigned the appropriate licenses
- Licenses can be assigned to any security group
# Custom Security Attributes
- Business-specific attributes that you can define and assign to Entra Id objects
# Provisioning with SCIM
**SCIM** - System for Cross-Domain Identity Management
![[Pasted image 20260804131931.png]]
