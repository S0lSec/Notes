# Entilement Management
Governance is the process of overseeeing and managing a system.
Identity lifecycle management is the creation to deletion of accounts.
![[Pasted image 20260818183151.png]]

Entitlement management is an identity governance feature that allow organisations to manage the identity and access lifecycle at scale. This works via automating access request workflows, access assignments, reviews and expiration.
# Define Access Packages
An access package is a list of resources. A policy is included controlling access.

When to use access packages:
- Time-limited access
- Manager approval or delegated role/identity
- Manage access without IT involvement
- Cross-organisation collaboration
# Define Catalogs
A catalog is a container of resources and access packages.
It is used to group related resources together.
# Manage Terms of Use
- Terms of use are stored as a PDF.
- A PDF can contain EULA.
- Can enforce complaince
# Manage the Lifecycle of External Users in Entra ID
You can select what happens when an external user, who was invided to your directory through an access package request being approved, no longer has any access package assignments.

This can happen if the user relinquishes all their access package assignments, or their last access package assignment expires. By default, when an external user no longer has any access packages assignments, they're blocked from signing into your directory. After 30 days, their guest user account is removed from your directory.
# Configure and Manage Connected Organisations
A connected organisation is another org that you have a relationship with.

For users in a connected org to have access to your resources you will need a representation of that orgs users. You can use **entitlement management** to bring them into your directory as needed.