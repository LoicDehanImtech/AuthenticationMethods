
Biometrics built-in windows: Vast gebonden aan de actieve sessie. Niet mogelijk om te omzeilen vie impersonation/run-as/etc. 
-> Indien biometrics moet het zelf geïmplementeerd worden
-(Finger/Palm/Face/Voice/pin)
## Categorie 1: Identificatie met optionele Authenticatie
Windows Credential store
	- Eenmalig username + wachtwoord registreren op server
	-> Applicatie kan deze hergebruiken na identificatie
Identificatie via:
	1. RFID smart card (simpele tekst aflezen van kaart)
		1. Lage security -> probleem wetgeving
	2. PKI smart card -> username, optional CBA
		1. Moeilijk om pin te vermijden
	3. NFC smart phone connection
		- Niet iedereen heeft een Smartphone (>2015)
	4. **QR-Code + Smart Phone**
	5. Eigen Biometrics app
		- Complexe implementatie
	6. Simple Menu select username
		- Extreem lage security (CRA wetgeving)
		- Combinatie met iets als **push notification** 

## Categorie 2: Altijd Authenticatie
1. PKI smart card
2. NFC smart phone -> Unlock voor authenticatie
3. **QR-Code + Smart Phone**




## Connectie met reader: (NFC/Smart Card/ biometric/etc.)
1. USB->IP converter
	 a. Stuur PC/SC commands naar card reader
	 b. Virtual Device software
		 + Eenvoudigere implementatie (Windows kan device zelf aanspreken)
		 - Eventueel consistentie? 24/7 ?
2. Whitelist op Thin client. Programma op beide kanten van de Remote desktop session om het device beschikbaar te maken op de server
3. kleine raspberry pi server die device beschikbaar stelt aan implant
4.


Physieke scanners:
	- Fabrieks omstandigheden (Bv. Stof) zorgen voor problemen bij herhaaldelijk gebruik van physieke scanners. Bv. FIDO (USB) key, Contact cards, fingerprints



- **Fallback Mechanisms:** What happens if the primary method fails (e.g., user forgets PIN, loses smart card/phone, biometric reader malfunctions)?
- -> Optie om toch wachtwoord in te geven