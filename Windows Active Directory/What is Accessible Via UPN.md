If you are an authenticated user within the same Windows Active Directory (AD) domain as the target user, and you know their User Principal Name (UPN - e.g., john.doe@yourcompany.com), you can typically access a significant amount of information about them by default. (In contrast to [[What is not accessible via UPN]])
Active Directory is designed to be a directory service, and one of its core functions is to make information about resources (including users) available to other authenticated members of the domain.
Here's a breakdown of the information you can usually access by default as a standard domain user:
### **Commonly Accessible Information (Default Read Permissions):**
Basic Identity:
	Full Name (Display Name)
	First Name
	Last Name
	Initials
	SAM Account Name (the older DOMAIN\username format)
	User Principal Name (UPN - which you already know)
	SID (Security Identifier)
Contact Information:
	Email Address
	Work Phone Number(s) (Telephone Number, Mobile, Fax, IP Phone)
	Office Location
	Street Address, City, State/Province, Postal Code, Country/Region (if populated)
Organizational Information:
	Job Title
	Department
	Company
	Manager (often shown as the manager's user object, which you could then query)
	Direct Reports (sometimes visible, depends on AD configuration/tool)
	Group Membership:
	You can usually see which groups the user is a member of (memberOf attribute).
	Account Information (Limited):
	Description field
	When the account was created (whenCreated attribute)
	Sometimes lastLogonTimestamp (this is replicated infrequently and isn't a precise "last logon time", but gives an indication). Note: The true lastLogon is stored only on the specific Domain Controller that authenticated the logon and isn't easily queried remotely without specific permissions/tools.
	Whether the account is Enabled or Disabled (usually readable).
# How You Might Access This Information:
PowerShell: This is the most powerful and common method for standard users. The Get-ADUser cmdlet is key. Make sure you have the Active Directory module installed (usually requires RSAT) or run from a machine where it's available. Import-Module ActiveDirectory

# Get default properties
`Get-ADUser -Identity "john.doe@yourcompany.com"
# Get all typically readable properties
`Get-ADUser -Identity "john.doe@yourcompany.com" -Properties *
# Get specific properties like Manager and MemberOf
`Get-ADUser -Identity "john.doe@yourcompany.com" -Properties DisplayName, Department, Title, Manager, MemberOf

**Outlook / Global Address List (GAL)**: Applications like Microsoft Outlook query AD to populate the address book. You can often right-click a user and view their properties, which shows a subset of the AD information.
Command Prompt (Legacy):
- `net user john.doe /domain` (provides very basic information)
- `dsquery user -upn john.doe@yourcompany.com | dsget user -display -email -dept -title -memberof` (more detailed, uses older DS tools)
- Third-Party Tools: Various **LDAP browsers or AD querying** tools exist.


### Permissions are key, but the default AD setup is relatively open for read access among domain members.