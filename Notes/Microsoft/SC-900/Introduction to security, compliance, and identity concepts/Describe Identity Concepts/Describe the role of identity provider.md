# The role of the identity provider
- Identity provider creates, maintains and manages identity information and offers authentication, authorization and auditing services to applications and services.
- Applications delegate these responsibilities to the identity provider
# Why centralized authentication
Without a central identity provider, each application manages its own user accounts and enforced its own security policies. 

Which provides several challenges:
- Separate usernames and passwords
- Inconsistent security policies
- Administrative overhead
# Security Tokens and Claims
A security token is  a structured package of data that the identity provider issues after verifying a users identity. The application validates the token and uses the information inside it to grant access.

Tokens carry information in the form of claims (individual pieces of data about the authentication identity). Claims can include:
- The user's unique identifier
- Their display name and email address
- Their assigned roles or group memberships
- When the token was issued and when it expires
- What the token grants permission to do

## Two primary types of security tokens
- **ID token**: User has signed in (Authentication)
- **Access token**: User has permission (Authorization)
# Authentication Protocols
- OpenID Connect (OIDC)
- OAuth 2.0
- Security Assertion Markup Language (SAML)
# Single Sign-on
User signs in once and the identity provider issues tokens that the user presents to applications. The application validates the token against its trust relationship with the identity provider and grants access without requiring another sign-in