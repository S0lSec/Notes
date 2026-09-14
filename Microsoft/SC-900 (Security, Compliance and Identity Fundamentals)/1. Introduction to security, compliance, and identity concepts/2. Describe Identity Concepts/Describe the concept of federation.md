Federation enable access to services across organisational or domain boundaries by establishing trust relationships between separate identity providers.
# How federation works
1. Organisation identity system vouches for you
2. Partners system accepts that voucher
![[Pasted image 20260731152632.png]]
Organization A configures its identity provider to _trust_ Organization B's identity provider. When a user from Organization B tries to access a resource in Organization A, Organization A's identity provider accepts the authentication that Organization B already performed and grants access based on that trust.
# Federation in Practice
## Business-to-business (B2B) collaboration
Two companies partner on a project, federation lets employees from one company access shared resources.
## Social and consumer identity providers
Consumer application lets users sign in with their Google, Microsoft or GitHub account.
## Enterprise application integration with on-premises identity
Organisations with on-prem AD DS can use federation to extend on-premises authentication to cloud services.
