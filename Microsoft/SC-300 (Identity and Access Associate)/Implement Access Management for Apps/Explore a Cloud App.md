# What is a App
An app is a application running self contained in the cloud. They function with resources that a part of their code configuration.

If an app needs access to Azure resources they need to have an identity they can use to connect to those resources. (This is done with managed identity)
# Access app from other tenants
![[Pasted image 20260818115109.png]]
You cannot use managed identity across tenants that need access to the same app/resource. You must register the application to create a service principle.

- Service principles are used:
	- Each tenant registers the app (creates a service principle)
	- Required a key or certificate for authentication
# Register an App in Entra ID
1. **Do the app registration (parent)** - This is global and has permissions
2. **App role** - Used to pass role specific information into your app for a developer to use
3. **Enterprise app** - Tenant specific data
(Note: When using PowerShell, you create an app registration first then the enterprise app if you need it)
## Global
- Unique application ID
- Redirect URI
- Branding
- API permissions
- Role definitions
## Tenant-specific service principle
- Reference to application + unique object ID
- User/group assignments
- Role assignments
- Visibility in portals
# Single tenant vs Multitenant apps
single tenant app means the app is only available to users and resources within that tenant. Multitenant apps can access user and resources from multiple tenants.