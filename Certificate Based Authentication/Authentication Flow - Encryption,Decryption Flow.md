
## Encryption/Decryption Flow

### 1. Authentication Initiation:
- User inserts smart card into reader
- System requests authentication
### 2. Certificate Presentation:
- The public certificate is read from the card
- System verifies certificate validity with the CA
### 3. Challenge-Response:
- System generates a random challenge
- Challenge is encrypted with user's public key
- Encrypted challenge sent to smart card

### 4. Decryption on Card:
- Smart card uses internal private key to decrypt challenge
- Critical point: Decryption happens ON THE CARD itself, not on the computer
- This "on-card computation" is the key security feature
### 5. Response:
- Decrypted challenge (or derived signature) is returned
- System verifies the response matches the original challenge
### 6. Session Establishment:
- Upon successful verification, authentication completes
- Kerberos ticket or session token issued
