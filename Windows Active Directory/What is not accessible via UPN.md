### What You Typically CANNOT Access (Without Specific Permissions):
- Password / Password Hashes: Absolutely not accessible.
- Sensitive Attributes: Administrators can configure specific Access Control Lists (ACLs) on certain attributes (like unixHomeDirectory, custom attributes containing sensitive data like salary or SSN if used improperly) to restrict read access.
- Detailed Logon Information: Precise last logon times across all DCs, logon workstation history (unless auditing is configured and you have rights to view logs).
- Password Policies Applied: Details of Fine-Grained Password Policies applying directly to the user might require higher privilege.
- BitLocker Recovery Keys: Stored elsewhere or with specific ACLs.
- Remote Desktop Settings: Specific user-level RDP settings might be restricted.