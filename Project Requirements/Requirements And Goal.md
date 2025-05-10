We are looking to change our application login system from simple username+password (stored in database) to something simple and secure.

Requirements:
1. Operators should not have to enter a password
2. Thin clients do not have usb ports. Only data transfer to external devices can be done via ethernet
3. CRA ruling requires us to setup for the future with security in mind. Therefore we want to use the windows active directory
4. For the sake of Remote desktop the windows login session may not change. We simply want to validate a user  against the active directory in order to log in.

## A.Essentieel voor Functionaliteit:
### 1 Een manier van identificatie

Windows AD:
- sAMAccountName: Uniek binnen een domein (<20 char) DOMAIN\username
- UPN: SamAccountName@yourdomain.com
### 2.Manier om groepen op te vragen uit Active Directory (Vermoedelijk Windows, eventueel Azure)

Microsoft Entra ID (was vroeger Azure AD)
	-> Requires internet connection

Windows Active Directory

Google Cloud Identity: Provides identity and access management services within the Google Cloud ecosystem

Okta: A leading independent identity management platform offering single sign-on (SSO), multi-factor authentication (MFA), and lifecycle management.

AWS Identity and Access Management (IAM) & AWS Single Sign-On (SSO): If your infrastructure heavily relies on Amazon Web Services, their IAM and SSO services offer robust identity management.

Keycloak: An open-source Identity and Access Management solution that supports various authentication protocols (like SAML, OAuth 2.0, OpenID Connect) and can be self-hosted or managed.

## B. Essentieel voor Wetgeven CRA:
1. Klant de optie bieden voor security.
2. Product ontworpen met security in gedachten