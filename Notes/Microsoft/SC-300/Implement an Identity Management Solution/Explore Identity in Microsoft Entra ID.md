# Explain the Identity Landscape
|1) Zero Trust|
|---|
|![](https://learn.microsoft.com/en-us/training/wwl-azure/explore-identity-azure-active-directory/media/icon-verify-explicitly.png) Verify Explicitly  ![Decoration. Icon of a simple circuit showing that you should only grant the least level of access needed.](https://learn.microsoft.com/en-us/training/wwl-azure/explore-identity-azure-active-directory/media/icon-least-privilege.png)Use Least Privilege  ![Decoration. Icon of two arrows with points together showing a point where a breach potentially occurred.](https://learn.microsoft.com/en-us/training/wwl-azure/explore-identity-azure-active-directory/media/icon-assume-breach.png)Assume Breach|
1. Always think with **Zero Trust** in mind. Don't give access to data and applications because the user had access previously.

|2) Identity|3) Actions|
|---|---|
|Business to Business (B2B)|Authenticate - Prove - AuthN|
|Business to Consumer (B2C)|Authorize - Get - AuthZ|
|Verifiable Credentials|Administer - Configure|
|(Decentralize Providers)|Audit - Report|
2. Provide verified accounts for user & applications.
3. You have specific actions identity provides and to keep the systems running. Users and applications can authenticate and authorize to gain access to systems.

| 4) Usage                     | 5) Maintain                |
| ---------------------------- | -------------------------- |
| Access applications and data | Protect - Detect - Respond |
| Secure - Cryptography        |                            |
| Dollars - Licenses           |                            |
4. You get many actions that can be performed once your credentials are verified. Use applications and data while taking advantage of other identity based services.
5. Always keep your system up to date.
# Zero Trust with Identity
## Guidance for Architecture Design
|Verify Explicitly|Use least privilege access|Assume breach|
|---|---|---|
|Always validate all available data points including:|To help secure both data and productivity, limit user access using:|Minimize blast radius for breaches and prevent lateral movement by:|
|User identity and location|Just-in-time (JIT)|Segmenting access by network, user, devices, and app awareness|
|Device health|Just-enough-access (JEA)|Encrypting all sessions end to end|
|Service or workload context|Risk-based adaptive policies|Use analytics for threat detection, posture visibility and improving defenses|
|Data classification|Data protection against out of band vectors||
|Anomalies|||
## Deploy Zero Trust Solutions
A Zero Trust approach should extend throughout the entire digital estate and serve as an integrated security philosophy and end-to-end strategy.

You need to implement Zero Trust controls and technologies across six foundational elements.
![[Pasted image 20260804122956.png]]
## Zero Trust Architecture
![[Pasted image 20260804123426.png]]
- Security policy governs everything
- Identity is used to verify identity and access
# Identity as a Control Plane
A control plane is a long-established networking concept. It is the component responsible for determining how traffic flows through a network.

A control plane is a tool or service that directs access to resources based on specific criteria.
# Why we have Identity
Identity gives the ability to:
- prove they are who they say they are - **Authentication**
- get permission to do something - **Authorization**
- report what was done - **Auditing**
- IT manage and self administer an identity - **Administration**

|Authentication|Authorization|Administration|Auditing|
|---|---|---|---|
|![](https://learn.microsoft.com/en-us/training/wwl-azure/explore-identity-azure-active-directory/media/icon-authentication.png)|![](https://learn.microsoft.com/en-us/training/wwl-azure/explore-identity-azure-active-directory/media/icon-authorization.png)|![](https://learn.microsoft.com/en-us/training/wwl-azure/explore-identity-azure-active-directory/media/icon-administration.png)|![](https://learn.microsoft.com/en-us/training/wwl-azure/explore-identity-azure-active-directory/media/icon-audit.png)|
|User sign on experience|User sign on experience|Single view management|Track who does what, when, where and how|
|Trusted source(s)|Can a user access the resource|Application of business rules|Focused alerting|
|Federative protocols|What can they do when they access it?|Automated requests, approvals, and access assignment|In-depth collated reporting|
|Level of assurance||Entitlement management|Governance & compliance|
## What is an Identity Provider (IdP)
An identity provider is a system that creates, manages and stores digital identities.
- Google
- Microsoft Entra ID
- GitHub
## Common Identity Protocols
- OpenID provider
- SAML identity provider
# Identity Administration
Identity administration is how identity objects are managed over the lifetime of the identity's existence.
![[Pasted image 20260804124757.png]]
## Identity Administration Provides
- A system that is highly configurable around business processes
- The agility to scale resources according to demand
- Cost savings through the distribution and automation of management
- Flexibility around synchronization, proliferation and change control
## Identity Management Automation
|PowerShell|CLI (command line interface)|
|---|---|
|Cross-platform PowerShell runs on Windows, macOS, Linux|Cross-platform command-line interface, installable on Windows, macOS, Linux|
|Requires Windows PowerShell or PowerShell|Runs in Windows PowerShell, Command prompt, or Bash and other Unix shells|

|Scripting Language|Action|Command|
|---|---|---|
|Azure CLI|Create user|`az ad user create --display-name "New User" --password "Password" --user-principal-name NewUser@contoso.com`|
|Microsoft Graph|Create user|`New-MgUser -DisplayName "New User" -PasswordProfile Password -UserPrincipalName "NewUser@contoso.com" -AccountEnabled $true -MailNickName "Newuser“`|
# Contrast Decentralised Identity with Central Identity Systems
**Centralised Identity Management** or **Central Identity System** is a single identity tool where credentials are stored and managed, to provide authentication capabilities.
## Decentralised Identity
- Helps people, organisations and things interact with each other transparently and securely in an identity trust fabric
- People control their own digital identity and credentials
# Microsoft Entra Business to Business
- Work with external organisations without having to maintain multiple identities
## Microsoft Entra External Identities
- External users can "bring their own identities"
- The external user's identity provider manages their identity
- You manage their access

The following capabilities make up External Identities:

| Type of B2B            | Usage                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **B2B collaboration**  | Collaborate with external users by letting them use their preferred identity to sign in to your Microsoft applications or other enterprise applications (SaaS apps, custom-developed apps, etc.). B2B collaboration users are represented in your directory, typically as guest users.                                                                                                                                                       |
| **B2B direct connect** | Establish a mutual, two-way trust with another Microsoft Entra organization for seamless collaboration. B2B direct connect currently supports Teams shared channels, enabling external users to access your resources from within their home instances of Teams. B2B direct connect users aren't represented in your directory, but they're visible from within the Teams shared channel and can be monitored in Teams admin center reports. |
