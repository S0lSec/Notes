# Implement and Configure Consent Settings
- A user/admin must grant permissions to an app before it can access company data.
- Users can allow apps access to specific information, like a mailbox, but not access to organisation servers.
- Users may not think through ramifications of granting access.
# Integrate On-Premises Apps via Entra Application Proxy
![[Pasted image 20260818122416.png]]
### What is a Application Proxy
- An application proxy is a feature that allows users to access on-prem applications.
- Proxy service runs in the cloud and has an App Proxy connector running on-prem.
- Securely passes sign-on tokens from Entra ID to the application.
### Value of an Application Proxy
- Protocol translation to/from modern authentication
- use seamless SSO to remove user action to log in multiple times
- Allows apps to stay on-prem, but still be securely available to the user
# Implement Application User Provisioning
Application provisioning refers to automatically creating user identities and roles in SaaS cloud applications that need to access.
# SCIM Provisioning
![[Pasted image 20260818123711.png]]
SCIM or System for Cross-Domain Identity Management is used to enable automatic provisioning of users and groups between your applications and Entra ID.

SCIM specifications provides a common user schema for provisioning.
# Monitor and Audit access/sign-on to Entra Integrated Enterprise Apps
- Usage and insight reports
- Audit logs
- Enterprise applications audit logs
- 