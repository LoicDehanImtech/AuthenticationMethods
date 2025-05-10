## Smart card requirements (Active Directory)

-Niet eender welke kaart met een chip of NFC signaal
	-> PKI-based Smart Cards

1. Secure Storage of Private Key: The smart card must have a secure chip capable of generating and securely storing a private cryptographic key on-board. This private key should never leave the card.

2. Support for X.509 Digital Certificates: The card must be able to securely store an X.509 digital certificate. This certificate contains the corresponding public key and identity information about the cardholder.

3. On-Card Cryptographic Operations: The smart card must be able to perform cryptographic operations (like digitally signing data or decrypting data) using the private key stored on the card without exposing the private key itself. This is fundamental to the security model. When logging into AD, the card uses its private key to sign the authentication request

4. PIN Protection: The card must support PIN verification. The private key should only be accessible for cryptographic operations after the user successfully enters their PIN to unlock the card. Ideally, the PIN verification happens securely on the card's chip.

5. Compatibility with a Cryptographic Service Provider (CSP) or Key Storage Provider (KSP):

6. ISO 7816 (contact) or ISO 14443 (CBA based) (contactless) compliant smart cards capable of securely storing a private key and performing on-card signing, 

7. protected by a PIN. Most importantly, these cards must be provisioned with an X.509 certificate issued by a trusted CA, 

8. containing the Smart Card Logon EKU, the user's UPN in the SAN, accessible revocation information, and linked to the private key stored securely on the card.

Cards:
- Beide Contact en contactless: Crescendo PIV / C2300 Cards

