# Administer Authentication Methods
| **Bad**: Password | **Good**: Password and... | **Better**: Password and...                         | **Best**: Passwordless                                             |
| ----------------- | ------------------------- | --------------------------------------------------- | ------------------------------------------------------------------ |
| 123456<br>qwerty  | SMB<br>Voice              | Authenticator<br>Software Tokens<br>Hardware Tokens | Autenticator<br>Window Hello<br>FIDO2 security key<br>Certificates |
## FIDO2
- Unphishable specification-based passwordless authentication method
- Allows users and orgs to leverage the specification to sign in to their resources without a username or password
### Implementation
1. Allow Self-service setup
2. Enforce attestation
3. Enforce key restrictions
## OATH Tokens
**OATH** - Open Authentication
**TOTP** - Time-based One Time Password
Software or hardware implementations available in Entra ID
# Implement Authentication Solutions based on Windows Hello for Business
![[Pasted image 20260810183608.png]]
(Note: Azure Active Directory is now Microsoft Entra ID)

- Credentials are based on certificate or asymmetrical key pairs
- Credentials can be bound to the device, and the token that is obtained using the credential is also bound to the device
- Identity providers validate user identity and maps the Windows Hello public key to a user account
