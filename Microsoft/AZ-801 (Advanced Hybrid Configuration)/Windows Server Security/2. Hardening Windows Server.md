# OSConfig

| **Capability**                        | **Description**                                                            |
| ------------------------------------- | -------------------------------------------------------------------------- |
| Scenario based security configuration | Applies and enforces security baselines like Secured-core, CIS, and STIGs  |
| Drift control                         | Detects drift from desired state and remediates automatically              |
| Reporting and auditing                | Generates reports on compliance and configuration status                   |
| Cross-platform support                | Works on Windows Server, Azure Arc, and Linux Edge devices                 |
| Integration                           | Compatible with PowerShell, Azure Policy, Windows Admin Center, and GitOps |
# Windows Local Administrator Password Solution (LAPS)
Automatically managed and rotates the password of the built-in local admin account on domain-joined windows computers, securely storing those randomised passwords inside your AD.

Provides organisations with a central local administrator passwords repository for domain-member machines.

**Features**:
- Backup passwords in AD/Entra ID
- Encrypt passwords in AD
- Local admin passwords are unique on each computer that Windows LAPS manages
## How Windows LAPS works:
1. Windows LAPS determines if the password of the local Administrator account has expired
2. If the password hasn't expired, Windows LAPS does nothing
3. If the password has expired, Windows LAPS performs that following steps:
	1. Changes the Local admin password to a new, random value based on the configuration parameters for local Admin passwords
	2. Transmits this new password and the new password-expiration data to AD DS or Entra ID
	3. AD DS stores these properties in a special, confidential attribute associated with the computer account of the computer that has had its local Admin account password updated
## Configure and manage passwords using Windows LAPS
1. Move computers targeted for LAPS to a specific OU
2. using the `Set-LapsADComputerSelfPermission` cmdlet to assign the computer account the ability to update their computer's local Admin account password when it expires

Policies that you can configure after you have installed the templates:
- Enable local admin password management
- Password settings
# Configure Privileged Access Workstations (PAW)
PAW is a heavily hardened, dedicated physical or virtual computer used exclusively by admins to manage high-level infrastructure like DC, prevent credential theft.

**When configuring a PAW you should:**
- Ensure that only authorised users can sign into the PAW
- •Enable Microsoft Defender Credential Guard
- Enable BitLocker Drive Encryption
- Use Microsoft Defender Device Guard policies to restrict app execution to only trusted apps
- Block PAWs from accessing the internet.
- Install all the tools your administrative tasks require
- Limit physical access to the PAWs

**After you have configured your PAWs, perform the following configuration tasks:**
- Block RDP, Windows PowerShell, and management console connections to your servers that come from any computer that isn’t a PAW
- Implement IPsec Connection specific rules so that traffic between servers and PAWs is authenticated and encrypted to help protect against replay attacks
- Configure sign-in restrictions for administrative accounts so that those accounts can only sign in to a PAW

**Combining a daily-user workstation and a PAW:**
- Combine these computers by hosting the daily-use in a VM and the PAW as the host. NOT THE OTHER WAY ROUND
# Secure Domain Controllers
**Take the following precautions to help secure your organisations domain controllers:**
- Ensure domain controllers are running the most recent version of the Windows Server and have current security updates
- Deploy domain controllers using the Server Core installation option
- Keep physically deployed domain controllers in dedicated, secure racks separate from other servers
- Run virtualized domain controllers either on separate virtualization hosts or as a shielded VM on a guarded fabric
- Deploy domain controllers on hardware that includes a TPM and configure all volumes with BitLocker
- Use Microsoft Defender Device Guard to control the execution of scripts and executables on the domain controller
- Limit RDP connections by configuring RDP through Group Policy assigned to the Domain Controllers’ OU
- Configure the perimeter firewall to block outbound connections to the internet from domain controllers
- Review Center for Internet Security (CIS) benchmark for Windows Server for security guidance specific to domain controllers
# Analyse Security Configuration with Security Compliance Toolkit
- Microsoft SCT is a set of tools provided by Microsoft that you can use to download and implement security configuration baselines.
- Can use SCT to compare your current GPOS to the recommended GPO security baselines
# Secure SMB Traffic
- User SMB 3.1.1
**Configure SMB encryption:**
- On a per-share basis or for an entire file server
- Using Windows Admin Center
- Using Windows PowerShell:
	- `Set-SmbShare –Name <sharename> -EncryptData $true`
	- `Set-SmbServerConfiguration –EncryptData $true`
	- `New-SmbShare –Name <sharename> -Path <pathname> –EncryptData $true`
	- `Set-SmbServerConfiguration –RejectUnencryptedAccess $false`