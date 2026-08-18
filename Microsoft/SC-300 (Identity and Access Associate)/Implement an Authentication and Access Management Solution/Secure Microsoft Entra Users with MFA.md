# Configure and Deploy Self-Service Password reset
Self-service password reset:
- Allows user to reset their own password
- Doesn't require admin/IT intervention
- Requires users to be enrolled first
- Requires an assigned licence
## SSR Licensing Options

| **Feature**                                                                                                                                                                          | **Microsoft Entra ID Free** | **Microsoft 365 Business Standard** | **Microsoft 365 Business Premium** | **Microsoft Entra ID Premium<br>P1 or P2** |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------- | ----------------------------------- | ---------------------------------- | ------------------------------------------ |
| **Cloud-only user password change**<br>When a user in Microsoft Entra ID knows their password and wants to change it                                                                 | ✅                           | ✅                                   | ✅                                  | ✅                                          |
| **Cloud-only user password reset**<br>When a user in Microsoft Entra ID has forgotten their password                                                                                 |                             | ✅                                   | ✅                                  | ✅                                          |
| **Hybrid user password change or reset with on-premises writeback**<br>When a user in Microsoft Entra ID is synchronized from an on-premises directory using Microsoft Entra Connect |                             |                                     | ✅                                  | ✅                                          |
# Entra MFA
Can set up a Conditional Access Policy that requires a user/group to have MFA required for access to a specific resource.
## Considerations
**Cloud Only Setup** - Nothing additional required to setup
**Hybrid Identity** - Entra Connect must be deployed and synchronised/federated with your on-prem AD DS
**Need on-prem legacy apps** - Entra Application Proxy must be deployed
**Use Entra MFA with a RADIUS Authentication** - Network Policy Server (NPS) must be set up and configured