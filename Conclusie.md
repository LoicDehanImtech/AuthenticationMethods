
Wat is er nodig:
1. Praktisch voor implant login: 
	 Enkel identificatie en sessie op de server -> Kan groepen opvragen
2. CRA wetgeving
	 Optie bieden voor authenticatie (en Eventueel 2FA)
	 Security by design -> Geen duidelijk security problemen (Bv. wachtwoord in DB)
3. Nodig voor interactie met Azure AD (Of andere Identity Provider (ex. Keycloak))
	 1. Authenticatie -> CBA via Certificate Authority (Federated Authentication)
	 2. Of altijd authenticatie via de 3de partij en dan gewoon identificatie naar Windows AD (Als attribuut in JWT token)
		 -> Altijd internet connectie nodig

Restricties door constraints:
1. Binnen dezelfde windows login sessie blijven:
	 Biometrics built-in windows: Vast gebonden aan de actieve sessie. Niet mogelijk om te omzeilen vie impersonation/run-as/etc. 
	-> Indien biometrics moet het zelf geïmplementeerd worden
	-(Finger/Palm/Face/Voice/pin)
2. FabrieksOmstandigheden
	 -> Geen contact gebaseerde interactie (USB, fingerprint, Contact cards)
3. Oude windows installaties geen windows hello (Biometrics/pin)
4. Fabriek omstandigheden(Bv. Stof): geen fysieke scanners:
	- zorgen voor problemen bij herhaaldelijk gebruik van fysieke scanners. Bv. FIDO (USB) key, Contact cards, fingerprints

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
			 Bv. Pin opslagen in credential store en in de achtergrond doorgeven
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
4. Eigen biometric implementatie
5. 3de Partij bv. Azure AD -> Windows AD SID in JWT token om te linken



## Connectie met reader: (NFC/Smart Card/ biometric/etc.)
1. USB->IP converter
	 a. Stuur PC/SC commands naar card reader op IP/Port
	 b. Virtual Device software
		 + Eenvoudigere implementatie (Windows kan device zelf aanspreken)
		 - Eventueel consistentie? 24/7 ?
2. Whitelist op Thin client. Programma op beide kanten van de Remote desktop session om het device beschikbaar te maken op de server
3. kleine raspberry pi server die device beschikbaar stelt aan implant


- **Fallback Mechanisms:** What happens if the primary method fails (e.g., user forgets PIN, loses smart card/phone, biometric reader malfunctions)?
- -> Optie om toch wachtwoord/pin in te geven


Interactie me Microsoft Entra ID (Azure AD) of andere 3de partij (Federated Authentication)
- Windows AD registreren als Certificate Authority (CA).
- Authenticate User against Windows AD
- CBA van Windows AD naar 3de Partij
	- (Certificate, Challenge, Decrypt, receive token)



Iets als bankkaart:
	- Enkel identificatie nodig voor <50 euro
	- Authenticatie nodig voor >50 euro of na fraude detectie
			-> Risk Based authorisation
				- Na x tijd opnieuw authenticeren





Algemeen
 - Identificatie met Badge 
	 - Periodisch authenticatie met het wachtwoord
	 - In databank DB link van badge -> user
		 - Veld: Domain user of lokale user
- Voor wetgeving CRA - > SSO, uitloggen en inloggen met eigen
	- Of Gewoon Username/Password dialog 
		- En eventueel MFA geconfigureerd

Tabel user groepen met bit patronen
	-> Som van de bit patronen is het login bit patroon voor gupta
	

Automatisch uitloggen
	- Per groep/user/thin client?
	- Welke voorwaarden: Vaste tijdstippen / inactiviteit / etc.

-> Voorstel: Kaart fysiek op de scanner leggen, enkel ingelogd zolang de kaart daar ligt
-Fallback 

To check:
- Simpelweg: Bitpatroon doorgeven aan gupta kant
- Inlog procedure in gupta code zodat implant5 kan blijven werken zoals het is. En implant6 de nieuwe methode kan gebruiken
- Wachtwoord verlopen opvragen via UPN

To Test:
- Test of lokaal domein mogelijk is om groepen op te vragen
