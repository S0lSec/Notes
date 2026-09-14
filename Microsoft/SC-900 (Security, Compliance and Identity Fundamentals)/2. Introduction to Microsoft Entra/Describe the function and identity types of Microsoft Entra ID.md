# Microsoft Entra
Entra family is organised around the access scenarios it secures.

| Category                                 | What it covers                                                                            |
| ---------------------------------------- | ----------------------------------------------------------------------------------------- |
| Establish Zero Trust access controls     | Foundational identity, authentication, and managed domain services                        |
| Secure access for employees              | Identity governance, identity protection, secure network access, and verified credentials |
| Secure access for customers and partners | External collaboration and customer identity and access management (CIAM)                 |
| Secure access in any cloud               | Identities for applications, services, and workloads                                      |
| Secure access for AI agents              | Identity, governance, and protection for nonhuman AI agent identities                     |
## Entra ID
Microsoft cloud-based identity and access management service
- Organisations can enable their employees, guests, device, workloads and agents to sign in and access resources.
- Provide a single identity system for their cloud and on-premises applications
- Protect user identities and credentials to meet an organisation access governance requirements
- Subscribers to Azure services, 365 or Dynamic 365 automatically have access to Entra ID
## Identity Types
**Human (user) identities**
- Internal user - Employees
- External users - Guests, partners, customers, etc

**Workload identities**
- Service principal - Uses Microsoft Entra ID for identity and access functions
- Managed identities - A service principal managed in Entra ID that elements the need for app developers to manage credentials

**Devices**
- Entra ID registered - Support for BYOD
- Entra ID joined - Device joined via an organisational account
- Hybrid joined - Devices are joined to your on-prem AD and Entra ID, requiring organisational account to sign in

**Agent identities**
- AI Agents
- Attended and autonomous scenarios

**Hybrid identities**
- Common user identity for authentication and authroisation to on-prem and cloud resources
- Hybrid identity is accomplished through:
	- Inter-directory provisioning
	- Synchronisation
- Entra ID Connect cloud sync