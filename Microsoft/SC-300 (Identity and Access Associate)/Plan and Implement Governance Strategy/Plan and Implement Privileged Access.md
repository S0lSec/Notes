# Define a Privileged Access Strategy for Administrative Users
# Privileged Identity Management (PIM)
PIM is a service in Entra ID that enables you to manage, control and monitor access to important resources in your organisation.

PIM provides time-based and approval-based role activation to mitigate the risks of excessive, unnecessary or misused access permissions on resources you care about.

PIM Features:
- Provide just-in-time privileged access to Entra ID and Azure resources
- Assign time-bound access to resources using start and end dates
- Require approval to activate privileged roles
- Collect justification to understand why users activate
- Get notifications when privileged roles are activated
- Conduct access reviews to ensure users still need the roles
- Download audit history for internal or external audit
# Plan and Configure Privileged Access Groups
In PIM you can assign eligibility for  the membership or ownership of privileged access groups. 
You can assign Microsoft Entra built-in roles to cloud groups and use PIM to manage group memeber and ower eligibility and activation.
# Create and Manage Break-Glass Accounts
A break-glass account is a emergency access account only used in scenarios where normal administrative accounts can't be used.

It is recommended you maintain a goal of retricting emergency account use to only when necessary. (**Implement strict security controls**)
### Considerations
These accounts should be cloud-only that use the *.onmicrosoft.com* domain and aren't federated or synchronised from an on-prem environment.

Create two or more and do not use the same MFA method for both.
### Validate Break-Glass Accounts
When you train staff members to use emergency access accounts and validate the emergency access accounts, as a minimum, do the following steps at regular intervals:
1. Define which account to check
2. Ensure the accounts are documented and current
3. Ensure security officers who might need emergency accounts are trained on the process
4. Update the account credentials
5. Validate that the emergency access accounts can sign in and perform administrative tasks
6. Ensure that MFA or SSPR isn't registered to any individuals device or details

Account verification should be performed at least every 90 days, when a change in IT staff has beeen made or Entra subscriptions have changed.