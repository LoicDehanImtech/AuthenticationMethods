**Certificaat om naar de Azure domain controller te linken hoe wordt dit unlocked / gelinkt aan windows active directory.**
## Info 
[[Certificate Based Authentication]]

[[Certificate Authority]]

- Authenticate against Windows AD
- Request Certificate
- Follow through [[Certificate Based Authentication]] flow
- Receive and parse [[JSON Web Token (JWT)]]


"""https://learn.microsoft.com/en-us/entra/identity/authentication/concept-certificate-based-authentication-smartcard
Microsoft Entra users can authenticate using X.509 certificates on their smart cards directly against Microsoft Entra ID at Windows sign-in. There's no special configuration needed on the Windows client to accept the smart card authentication.
"""


## Method:
 **Certificate-Based Authentication (CBA) with Azure AD (En de andere Okta, Google, keycloak etc.)

1. Setup Link Windows AD -> Azure AD
2. Setup windows Internal CA (Publicly Trusted Certificate Authorities)
3. Setup Sync Windows AD en Azure AD zodat gebruikers overeenkomen (En log errors)

Trust: Certificates issued by your internal CA are not inherently trusted by external entities (like websites on the internet). However, for your internal applications authenticating against your Azure AD tenant, this is not usually a concern as you are explicitly establishing the trust within your Azure AD configuration.

using System.Security.Cryptography.X509Certificates; 

[Overview of Microsoft Entra certificate-based authentication - Microsoft Entra ID | Microsoft Learn](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-certificate-based-authentication)