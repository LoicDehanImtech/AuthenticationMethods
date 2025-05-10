[[Biometrics in Windows]]
**-> Should be able to retrieve SID** ?
- https://learn.microsoft.com/en-us/windows/win32/api/winbio/nf-winbio-winbioidentify 
	-> Which can then be used to pull the groups of active directory
	- https://aistudio.google.com/prompts/1qgElsVbumGKwLOh-zG1fKsnUw9W4Xqbs
	- https://aistudio.google.com/prompts/1zPsflCaCmDIOsMB0oKh5lVlxtGa8RbRO

## Fingerprint / palm scan
Not possible due to [[Practical Limitations]] regarding dust and labor environment

**Combines card + fingerprint: https://cpl.thalesgroup.com/access-management/safenet-idprime-fido-biometric-smart-card**

Nadelen:
-  Fingerprint login. Gebeurt via window hello, wordt lokaal op device opgeslagen. 
	->  Fingerprint zou op elk device dat een operator gebruikt moeten worden geregistreerd.
- Fingerprint login. Consistentie? Vaak op gsm problemen met scannen van vinger -> Handschoenen, vereist propere handen
- Fingerprint login. Scanner via ethernet?
## Facial recognition / Iris scan

## Voice recognition
Same principle as Facial recognition but less consistent. And more difficult with background noise.
