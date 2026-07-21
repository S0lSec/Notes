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