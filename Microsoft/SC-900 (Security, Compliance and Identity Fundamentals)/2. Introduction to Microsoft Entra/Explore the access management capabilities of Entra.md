# Conditional Access
Conditional Access (CA) policies are if-then statements

**Assignments determine which signals to use**
- Users, groups, workload identities, roles
- Cloud apps or actions
- Sign-in and user risk detection
- Device or device platform
- IP location

**Access controls determine how a policy is enforced**
- Block access
- Grant access
- Session control

**Protecting AI services**
- Conditional access policies can protect AI services from misuse and unathorised access
# Entra Global Secure Access
GSA is Microsoft's Security Service Edge (SSE) solution uses Zero Trust network, identity and endpoint access controls to secure access.

It combines Entra Internet Access, Entra Internet Access for Microsoft Services and Entra Private Access with Defender for Cloud Apps.

Gives control over network traffic at the end-user computing de

- **Entra Internet Access** provides an identity-centric Secure Web Gateway (SWG) solution for SaaS applications and other internet traffic
- **Entra Internet Access for Microsoft Services** enhances Entra ID capabilities with direct connectivity to supported Microsoft services, improving security, performance and resilience
- **Entra Private Access** provides your uses secure access to your private, corporate resources
- **GSA helps secure AI workloads** by ensuring that traffic to and from these services pass through the same identity-aware security controls applied to other enterprise traffic
![[Pasted image 20260807141114.png]]
# Entra roles and role-based access control (RBAC)
Roles control permissions to manage Entra resources.

**Types:**
•Built-in roles.
•Custom roles.
•Categories of Microsoft Entra roles:
	- Microsoft Entra specific
	- Service-specific
	- Cross service
- Only grant the access users need
![[Pasted image 20260807141213.png]]