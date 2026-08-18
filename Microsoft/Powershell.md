(Will fix later)
Install AD DS server role
Install-WindowsFeature –Name AD-Domain-Services –ComputerName SEA-SVR1

Verify AD DS role is installed
Get-WindowsFeature –ComputerName SEA-SVR1

Run command on different server
(make sure server is added in all servers has ad ds)

Invoke-Command -ComputerName SEA-SVR1

Create an OU
New-ADOrganizationalUnit -Name "Seattle" -Path "DC=contoso,DC=com" -ProtectedFromAccidentalDeletion $true -Server SEA-DC1.contoso.com

Create user account
New-ADUser -Name Ty -DisplayName 'Ty Carlson' -GivenName Ty -Surname Carlson -Path 'OU=Seattle,DC=contoso,DC=com'

Set user password
Set-ADAccountPassword Ty

Enable account
Enable-ADAccount Ty

Create domain global group
New-ADGroup SeattleBranchUsers -Path 'OU=Seattle,DC=contoso,DC=com' -GroupScope Global -GroupCategory Security

Add user to group
Add-ADGroupMember -Identity SeattleBranchUsers -Members Ty

Check users in group
Add-ADGroupMember -Identity SeattleBranchUsers -Members Ty

Add user to local administrators group
Add-LocalGroupMember -Group 'Administrators' -Member 'CONTOSO\Ty'

# Networking
## Display Routing Table
`netstat -r`
## Display Active Connections
`netstat -abno`
# Bulk adding users
1. Install Mircosoft.Graph powershell module
	 `Install-Module Microsoft.Graph -Scope CurrentUser -Verbose`
2. Confirm installation
	 `Get-InstalledModule Microsoft.Graph`
3. Login to Microsoft Graph API
	 `Connect-MgGraph -Scopes "User.ReadWrite.All"`
4. Verify you are connected
	`Get-MgUser`
5. Assign common temp password to all new users 
```
$PWProfile = @{
    Password = "<Enter a complex password you will>";
    ForceChangePasswordNextSignIn = $false
}
```
6. Create new user
```
New-MgUser `
    -DisplayName "New PW User" `
    -GivenName "New" -Surname "User" `
    -MailNickname "newuser" `
    -UsageLocation "US" `
    -UserPrincipalName "newuser@<labtenantname.com>" `
    -PasswordProfile $PWProfile -AccountEnabled `
    -Department "Research" -JobTitle "Trainer"
```
# Bulk Invite Users
1. Install Mircosoft.Graph powershell module
	 `Install-Module Microsoft.Graph -Scope CurrentUser -Verbose`
2. Confirm installation
	 `Get-InstalledModule Microsoft.Graph`
3. Login to Microsoft Graph API
	 `Connect-MgGraph -Scopes "User.ReadWrite.All"`
4. Set the values for the email and redirect for the External user
```
Import-Module Microsoft.Graph.Identity.SignIns

$params = @{
    invitedUserEmailAddress = "admin@fabrikam.com"
    inviteRedirectUrl = "https://myapp.contoso.com"
}
```
5. Send the MgInvitation command to invite the External user
	`New-MgInvitation -BodyParameter $params`