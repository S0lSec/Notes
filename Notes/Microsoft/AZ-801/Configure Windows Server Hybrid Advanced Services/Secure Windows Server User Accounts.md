# Configure User Accounts Rights
- User rights apply to the overall systems
- Permissions apply to objects
- Use principal of least privilege

**Use the following to help manage user rights:**
- User rights assignment policy, such as:
	- Take ownership of files or other objects
	- Load and unload device drivers
- Account security options, including:
	- Logon hours
	- Logon workstations
	- Account is sensitive and cannot be delegated
# Configure Security Options
Security policy settings are rules that are configured on a computer or multiple devices for protecting resources on a device or network.

- The Security Setting extension of the Local Group Policy Editor snap-in allows you to define security configurations as part of a GPO
- GPOs are linked to AD containers and they enable you to manage security settings for multiple devices from any device joined to the domain
# Configure Password Policies
- Control how users authenticate with Win Server
- Default password policies are set using GPOs linked to the domain
- Microsoft Entra Password Protection for AD DS gives another level of control and security
- You can implement fine-grained password policies using Ad Administrative Center and assign them to a suer or a global security group
# Protect User Accounts
## When a user is a member of the Protected Users group:
- User credentials are not cached locally
- Credential delegation (CredSSP) will not cache user credentials
- Windows Digest will not cache user credentials
- NTLM will not cache user credentials
- Kerberos will not create DES or RC4 keys, or cache credentials or long-term keys
- The user can no longer sign-in offline
- NTLM authentication is not allowed
- DES and RC4 encryption in Kerberos preauthentication cannot be used
- Credentials cannot be delegated using constrained delegation
- Cannot be delegated using unconstrained delegation
- Ticket-granting tickets (TGTs) cannot renew past the initial lifetime
## Protected Users group prerequisites:
- The protected user group is a universal group and replicated across all domain controllers
- The user must sign in to a device running Win 8.1 or Win Server 2012 R2 or newer
- Domain controller protection requires that domains must be running at a Win Server 2012 R2 or high domain functional level

(Notes: Lower functional levels still support protection on client devices)
## Authentication Policies
### Authentication Policies
- Enable you to configure:
	- TGT lifetime
	- Access-control conditions for a user, service or computer account
- For user accounts you can:
	- Configure the users TGT lifetime
	- Restrict devices the user can sign into
	- Define criteria that the devices must meet
### Authentication Policy Silos
- Enable you to assign authentication policies to user, computer and service account
- Work with the Protected Users group to add configurable restrictions to the groups existing non-configurable restrictions
- Ensure that the accounts belong to only a single authentication policy silo
# Describe Microsoft Defender Credential Guard
- Protects user credentials from compromise by isolating credentials within a protected, virtualised container, separate from the rest of the OS
- The virtualised containers OS runs parallel with but independent from the host OS

**Does not support:**
- Unconstrained Kerberos delegation
- NTLMv1 or MS-CHAPv2
- Digest authentication
- CredSSP delegation
- Kerberos DES encryption
- Use on DC
- Protections for the AD DS database or SAM
# Block NTLM Authentication
**NT LAN Manager**

The NTLM authentication protocol:
- Is less secure than the Kerberos authentication protocol
- Should be blocked in favor of using Kerberos

Prior to blocking NTLM you must ensure that existing applications are no longer using the protocol.

You can audit NTLM traffic by configuration the following Group Policy settings:
- Network security: Restrict NTLM: Outgoing NTLM Traffic to remote servers
- Network security: Restrict NTLM: Audit Incoming NTLM traffic
- Network security: Restrict NTLM: Audit NTLM authentication in the domain

After you have determined that you can block NTLM in your org you must configure the **Restrict NTLM: NTLM authentication in this domain** policy.

The configuration options are:
- Deny for domain accounts to domain servers
- Deny for domain accounts
- Deny for domain servers
- Deny all

(Navigate to: Computer Configuration\Windows Settings\Security Settings\Local Policies\Security Options)
# Locate Problematic Accounts
Check your AD DS environment for accounts that:
- Haven't signed in for a period of time
- Have passwords with no expiration data
# Implement Exploit Protection
1. Configure exploit protection settings in Windows Security app
2. Export the settings to an XML configuration file
3. Use GP or Microsoft Intune to apply the same settings to multiple devices in your org
# Configure and manage Windows Defender Application Control
- Designed to protect devices against malware and other untrusted software
- Prevents malicious code from running by ensuring that only approved code, that you know, can be run
# Implement Microsoft Defender for Endpoint
![[Pasted image 20260810141816.png]]
- Maximize available security capabilities and better protect your enterprise from cyber threats
- Onboarding your device enables you to identify and stop threats quickly , prioritize risks and evolve your defenses across OS and net devices
# Microsoft Defender SmartScreen
Determines whether a site is potentially malicious by:
- Analysing visited webpages and looking for indication of suspicious behavior. If it is determined suspicious, to shows a warning page
- Checking visited sites against a dynamic list of reported phishing sites and malicious software sites.