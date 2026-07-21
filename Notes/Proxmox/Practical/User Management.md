# Create a Linux PAM User Account
1. Go to server shell
2. `adduser backupadmin`
3. Supply new users information
# Connecting Linux PAM User to Proxmox VE
1. Go to Datacenter > Permissions > Users
2. Click Add
3. Supply Details
4. Ensure that Realm is *Linux Pam standard authentication Realm*
5. Click Add
# User Permissions and Roles
## Create Role
1. Go to Datacenter > Permissions > Roles
2. Click Create to create role
3. Add name and privileges
## Create Paths
1. Go to Datacenter > Permissions
2. Click Add > User Permission/Group Permission
3. Add details
