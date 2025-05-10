NFC
?
?
Contactless key cards
## CBA [[Certificate Based Authentication]]

SMART CARDS ALSO ARE BASED ON CBA

-> Zelfde CBA gebruikt om in te loggen bij Windows AD en om JWT te verkrijgen van Azure
-> Kan overal inloggen op dezelfde manier

-> Private key voor encryption/decryption zit beveiligd door windows  'user account isolation’ principe. Een weg daarom heen vinden breekt de integriteit van de authenticatie

contain smart card chips with proper security capabilities. They use standards like ISO 14443.

## Key Logging 
Automated password entry through name/password stored in card
- In the background of the login dialog await specific key combination followed by name/password 
- Authenticate against Windows AD
## Simpel mapping
- UPN/SID stored on card
- Poll groups from AD: [[What is Accessible Via UPN]]