A standardized electronic document that **binds a public key to an identity** (like a person, organization, server hostname, email address, etc.).

It **contains** the public key, but also includes other crucial information:
- **Subject:** The identity being certified (e.g., Name, Email, Hostname).
- **Issuer:** The trusted third party (Certificate Authority - CA) that verified the subject's identity and issued the certificate.
- **Validity Period:** A start and end date during which the certificate is considered valid.
- **Serial Number:** A unique identifier for the certificate from the issuer.
- **Key Usage:** Information about what the key pair is intended for (e.g., signing, encryption, authentication).
- **Issuer's Digital Signature:** The CA signs the entire certificate with its own private key. This allows others to verify that the certificate is authentic and hasn't been tampered with, provided they trust the CA.

**In essence:** A public key is just the key data. A certificate is a signed container that holds the public key and attests to the identity associated with it. You use the certificate to get someone's trusted public key.