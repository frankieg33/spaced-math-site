---
title: "Daglig Matte"
description: "Matteövningar med spridd repetition för iPhone och iPad"
---

# Integritetspolicy — Daglig Matte

**Ikraftträdandedatum:** 2026-05-21
**Senast uppdaterad:** 2026-06-10

Denna policy beskriver hur iOS-appen Daglig Matte ("Appen") hanterar dina uppgifter. Den gäller från v1.0 och framåt, inklusive v3:s modell för CloudKit-delning med en familj (som ersätter v2.0:s delning per profil).

## Sammanfattning på vanlig svenska

- Vi driver inga servrar. Vi samlar inte in någon personlig information.
- Allt stannar på din enhet om du inte slår på **iCloud-synkronisering**, då Apple, inte vi, lagrar det i ditt privata iCloud-konto.
- Appen använder din mikrofon endast medan du svarar på en uppgift i röstläge. Ljudet bearbetas av Apples taligenkänning (på enheten, Siri-klass) och kasseras omedelbart; vi lagrar, laddar aldrig upp eller analyserar det.
- Det finns inga tredjepartsspårare, ingen reklam och inga analys-SDK:er.

## Vad Appen lagrar på din enhet

- **Profiler.** Namn, emoji, färg och inställningar per profil.
- **Status för spridd repetition.** För varje kort (t.ex. `7 + 8`): schemalagt nästa repetitionsdatum, svårighet, stabilitet och antal repetitioner.
- **Aktivitet.** En daglig räkning av slutförda repetitioner per profil (används för svit-etiketten och Statistik-skärmen).
- **Fel.** En kö med uppgifter du nyligen svarat fel på, så att Appen kan visa dem igen.
- **Inställningar.** App-omfattande reglage, t.ex. om iCloud-synkronisering är på.

Allt detta skrivs till Appens egen, isolerade Dokument-mapp och till `UserDefaults`. Appen kan inte läsa andra appars data, och andra appar kan inte läsa Appens data.

## Vad Appen valfritt lagrar i iCloud

iCloud-synkronisering är **avstängd som standard**. När du slår på den (kugghjulsikonen → **Inställningar → Synkronisering → Använd iCloud**) skriver Appen samma data som beskrivs ovan till ditt privata iCloud via Apples **CloudKit**-API. Detta är ditt iCloud, åtkomligt endast för dig på enheter inloggade med samma Apple-ID. Vi har ingen åtkomst till det.

- De exakta data som synkroniseras: profiler, korttillstånd, aktivitet, fel och (valfritt) metadata för familjedelning (ett visningsnamn du väljer för din familj).
- iCloud-synkronisering omfattar **inte** innehållet i någon röstinspelning eller någon analys.
- När du loggar in med ett annat Apple-ID upptäcker Appen ändringen och stänger av synkroniseringen tills du uttryckligen slår på den igen, så att data inte tyst laddas upp till ett annat konto.
- Att radera en profil från **Hantera profiler** tar bort profilen från enheten och (när iCloud är åtkomligt på det ursprungliga Apple-ID:t) även från din iCloud-kopia.

## Familjedelning

I v3 sker delning på **familje**nivå i stället för per profil. Öppna kugghjulsikonen → **Inställningar → Familj → Skapa familj**, namnge din familj och bjud in familjemedlemmar via det vanliga iOS-delningsbladet (Meddelanden, Mail eller AirDrop).

- Alla profiler på ägarens enhet hör till familjen. Att bjuda in en familjemedlem delar dem alla på en gång.
- Data finns i **familjeägarens iCloud**. Deltagare lagrar ingen separat kopia i sitt eget iCloud; deras studieaktivitet skrivs direkt till ägarens CloudKit via Apples zonbegränsade CKShare-behörighetsmodell.
- Att gå med i en familj är **destruktivt på enheten som går med**: deltagarens befintliga lokala profiler ersätts med familjens. Innan du går med erbjuder Appen alternativet **Exportera profiler till fil** så att du kan spara en JSON-kopia av dina nuvarande data och importera dem igen senare om du ångrar dig.
- Om ägaren upplöser familjen (Inställningar → Familj → Upplös) eller loggar ut från iCloud förlorar deltagarna live-åtkomst vid sin nästa synkronisering. Den lokala cachen med familjeprofiler blir deras egen (ingen destruktiv radering på vägen ut).
- En deltagare kan lämna en familj när som helst (Inställningar → Familj → Lämna). Vid utträde behåller hen familjens profiler på sin enhet som sina egna.
- Apples `CKShare`-gräns är 100 deltagare per delat objekt. Den naturliga familjeskalan är ~6.

## Exportera / Importera (JSON-säkerhetskopia)

Under **Inställningar → Säkerhetskopia** kan du:

- **Exportera profiler till fil**: spara en JSON-fil med alla profiler på den aktuella enheten (oavsett familjestatus). Bra som manuell säkerhetskopia eller före destruktiva åtgärder.
- **Importera profiler från fil**: återställa en tidigare export. Läget **Sammanfoga** lägger till saknade profiler och uppdaterar befintliga om den importerade kopian är nyare. Läget **Ersätt** raderar lokala profiler och installerar den importerade uppsättningen; tillgängligt endast när du inte är i en familj.

## Mikrofon och taligenkänning

När röstläget är på, medan du svarar på en uppgift, gör Appen följande:

1. Fångar live-mikrofonljud med `AVAudioEngine`.
2. Strömmar det till `SFSpeechRecognizer` (Apples ramverk). På moderna iOS-enheter körs igenkänningen på enheten som standard; vissa konfigurationer kan använda Apples taligenkänningsservrar.
3. Läser de transkriberade siffrorna och bedömer svaret.
4. Stoppar inspelningen så snart ett slutgiltigt svar erhållits.

Vi behåller inget ljud, inga transkriptioner och ingen härledd signal. Vi överför inte ljud till någon annan part än Apples `SFSpeechRecognizer`. Appen begär `NSMicrophoneUsageDescription` och `NSSpeechRecognitionUsageDescription` vid första användningen; om någon av behörigheterna nekas stängs röstläget av automatiskt och sifferknappsatsen på skärmen används.

## Diagnostikloggar

Appen skickar ostrukturerade diagnostikhändelser via Apples standardramverk `OSLog` (t.ex. "studiepass avslutat, rätt=12 fel=3"). Dessa loggar:

- Stannar på enheten.
- Är endast synliga för dig, i Console.app medan enheten är ansluten till en Mac.
- Använder Apples `.private`-integritetsklassificering för potentiellt identifierande värden (profil-id, profilnamn), så att de värdena döljs i levererade versioner.

Vi samlar inte in, hämtar eller överför `OSLog`-innehåll.

## Data vi INTE samlar in

- Ditt namn, din e-post eller kontaktuppgifter.
- Din plats.
- Någon enhetsidentifierare (IDFA, IDFV, annons-id).
- Kraschrapporter utöver vad Apple kan samla in via dina iOS-inställningar.
- Någon analys eller beteendetelemetri.
- Betalnings- eller faktureringsuppgifter (köp hanteras helt av Apple).

## Barns integritet

Daglig Matte är utformad för att vara säker för barn. Eftersom Appen inte samlar in personlig information och inte kontaktar tredje part uppfyller den COPPA:s definition "ingen personlig information". Vi visar ingen reklam, och det finns inga konton eller sociala funktioner. Daglig Matte innehåller ett enda engångsköp i appen (en upplåsning av hela appen); eftersom appen är utformad för barn visas en vuxenkontroll före varje köp, enligt reglerna för Apples Barn-kategori. Alla betalningar och eventuella inlösen av koder hanteras av Apple via App Store. Appen ser eller lagrar aldrig dina betaluppgifter.

## Dina val

- **Stänga av röstläget** när som helst per profil (Inställningar → Röstläge), eller globalt genom att neka mikrofonbehörigheten i iOS-inställningarna.
- **Stänga av iCloud-synkronisering** när som helst (kugghjulsikonen → Inställningar → Synkronisering → Använd iCloud → av). Att stänga av raderar inte iCloud-kopior; radera varje profil för sig om du vill ta bort dem.
- **Upplösa eller lämna en familj** (Inställningar → Familj → Upplös / Lämna) för att sluta dela. Att upplösa återkallar deltagarnas åtkomst till din familj; att lämna behåller familjens profiler på din enhet som dina egna.
- **Exportera profiler till en fil** (Inställningar → Säkerhetskopia → Exportera) och behålla den lokalt: en manuell säkerhetskopia som aldrig rör iCloud.
- **Återställa en profils utveckling** utan att radera profilen (profilens inställningar → Återställ).
- **Radera en profil** (Hantera profiler → svep eller tryck för att radera): tar även bort iCloud-kopian när synkronisering är på. Upprepa per profil för att ta bort allt.

## Ändringar i denna policy

Om vi ändrar denna policy blir den nya versionen tillgänglig på samma URL med ett uppdaterat datum för **Senast uppdaterad**. Väsentliga ändringar anges även i Appens versionsinformation.

## Kontakt

Frågor om denna policy eller dina data? E-post **spacedmath@gmail.com**.
