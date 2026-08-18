# Plan your line-of-business Application Registration Strategy
- Add applications to Entra ID to leverage one or more of the services it provides
## Application objects and service principles
**Application objects** - Define and describe the application to Entra ID, enabling it to know how to issue tokens based on its settings. (Will only exist in their tenant)
**Service principles** - Govern an application connecting Entra ID. Can be considered the instance of the application in your tenant.
## Permission to add applications to Entra Instance
By default all users in your directory have rights to register application objects they are developing, and they have discretion over which applications they share or give access to their organisations data through consent.
# Application Permissions
Application that integrate with Microsoft identity platform follow an authorization model that gives users and administrators control over how data can be accessed.
### Types:
**Delegated permissions** - Used by apps that have a signed-in user present (Either user/admin consent)
**Application permissions** - Used by apps that run without a signed-in user present (Admin consent)