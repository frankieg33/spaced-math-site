# Privacybeleid — Rekenen elke dag

**Ingangsdatum:** 2026-05-21
**Laatst bijgewerkt:** 2026-06-10

Dit beleid beschrijft hoe de iOS-app Rekenen elke dag ("de App") met je gegevens omgaat. Het geldt vanaf v1.0, inclusief het v3-model voor CloudKit-delen met één gezin (dat het delen per profiel van v2.0 vervangt).

## Samenvatting in gewone taal

- We draaien geen servers. We verzamelen geen persoonlijke gegevens.
- Alles blijft op je apparaat, tenzij je **iCloud-synchronisatie** inschakelt; in dat geval bewaart Apple, niet wij, het in je privé-iCloud-account.
- De App gebruikt je microfoon alleen terwijl je in spraakmodus een opgave beantwoordt. De audio wordt verwerkt door Apple's spraakherkenning (op het apparaat, Siri-klasse) en meteen verwijderd; we bewaren, uploaden of analyseren het nooit.
- Er zijn geen trackers van derden, geen advertenties en geen analyse-SDK's.

## Wat de App op je apparaat bewaart

- **Profielen.** Naam, emoji, kleur en instellingen per profiel.
- **Status van gespreide herhaling.** Voor elke kaart (bijv. `7 + 8`): geplande volgende herhaaldatum, moeilijkheid, stabiliteit en aantal herhalingen.
- **Activiteit.** Een dagelijkse telling van voltooide herhalingen per profiel (gebruikt voor het reekslabel en het Statistieken-scherm).
- **Fouten.** Een wachtrij met opgaven die je onlangs fout beantwoordde, zodat de App ze opnieuw kan tonen.
- **Voorkeuren.** App-brede schakelaars, zoals of iCloud-synchronisatie is ingeschakeld.

Dit alles wordt geschreven naar de eigen, afgeschermde map Documenten van de App en naar `UserDefaults`. De App kan de gegevens van andere apps niet lezen, en andere apps kunnen de gegevens van de App niet lezen.

## Wat de App optioneel in iCloud bewaart

iCloud-synchronisatie staat **standaard uit**. Wanneer je die inschakelt (tandwielicoon → **Instellingen → Synchronisatie → Gebruik iCloud**), schrijft de App dezelfde hierboven beschreven gegevens naar je privé-iCloud via Apple's **CloudKit**-API. Dit is jouw iCloud, alleen toegankelijk voor jou op apparaten die met dezelfde Apple ID zijn ingelogd. Wij hebben er geen toegang toe.

- De exact gesynchroniseerde gegevens: profielen, kaartstatussen, activiteit, fouten en (optioneel) metadata van het gezin delen (een weergavenaam die je voor je gezin kiest).
- iCloud-synchronisatie omvat **niet** de inhoud van een spraakopname of enige analyse.
- Wanneer je met een andere Apple ID inlogt, detecteert de App de wijziging en zet de synchronisatie uit totdat je die uitdrukkelijk weer inschakelt, zodat gegevens niet stilletjes naar een ander account worden geüpload.
- Een profiel verwijderen via **Beheer profielen** verwijdert het profiel van het apparaat en (wanneer iCloud bereikbaar is op de oorspronkelijke Apple ID) ook uit je iCloud-kopie.

## Gezin delen

In v3 vindt het delen plaats op **gezins**niveau in plaats van per profiel. Open het tandwielicoon → **Instellingen → Gezin → Stel gezin in**, geef je gezin een naam en nodig gezinsleden uit via het standaard iOS-deelvenster (Berichten, Mail of AirDrop).

- Alle profielen op het apparaat van de eigenaar horen bij het gezin. Een gezinslid uitnodigen deelt ze allemaal tegelijk.
- De gegevens staan in de **iCloud van de gezinseigenaar**. Deelnemers bewaren geen aparte kopie in hun eigen iCloud; hun studieactiviteit wordt rechtstreeks naar de CloudKit van de eigenaar geschreven via Apple's zone-gebonden CKShare-rechtenmodel.
- Meedoen aan een gezin is **destructief op het apparaat dat meedoet**: de bestaande lokale profielen van de deelnemer worden vervangen door die van het gezin. Vóór het meedoen biedt de App een optie **Exporteer profielen naar bestand** zodat je een JSON-kopie van je huidige gegevens bewaart en later opnieuw importeert als je van gedachten verandert.
- Als de eigenaar het gezin ontbindt (Instellingen → Gezin → Ontbind) of uitlogt bij iCloud, verliezen de deelnemers bij hun volgende synchronisatie de live toegang. De lokale cache van gezinsprofielen wordt van henzelf (geen destructieve verwijdering bij het vertrek).
- Een deelnemer kan een gezin op elk moment verlaten (Instellingen → Gezin → Verlaten). Bij het verlaten houdt hij de gezinsprofielen op zijn apparaat als zijn eigen.
- De `CKShare`-limiet van Apple is 100 deelnemers per gedeeld item. De natuurlijke gezinsschaal is ~6.

## Exporteren / Importeren (JSON-reservekopie)

Bij **Instellingen → Reservekopie** kun je:

- **Exporteer profielen naar bestand**: een JSON-bestand met alle profielen op het huidige apparaat bewaren (ongeacht de gezinsstatus). Handig als handmatige reservekopie of vóór destructieve handelingen.
- **Importeer profielen uit bestand**: een eerdere export herstellen. De modus **Samenvoegen** voegt ontbrekende profielen toe en werkt bestaande bij als de geïmporteerde kopie nieuwer is. De modus **Vervangen** wist lokale profielen en installeert de geïmporteerde set; alleen beschikbaar als je niet in een gezin zit.

## Microfoon en spraakherkenning

Wanneer de spraakmodus is ingeschakeld, terwijl je een opgave beantwoordt, doet de App het volgende:

1. Legt live microfoonaudio vast met `AVAudioEngine`.
2. Streamt het naar `SFSpeechRecognizer` (Apple's framework). Op moderne iOS-apparaten draait de herkenning standaard op het apparaat; sommige configuraties kunnen Apple's spraakherkenningsservers gebruiken.
3. Leest de getranscribeerde cijfers en beoordeelt het antwoord.
4. Stopt de opname zodra een definitief antwoord is verkregen.

We bewaren geen audio, transcripties of afgeleid signaal. We versturen geen audio naar een andere partij dan Apple's `SFSpeechRecognizer`. De App vraagt `NSMicrophoneUsageDescription` en `NSSpeechRecognitionUsageDescription` bij het eerste gebruik; als een van beide rechten wordt geweigerd, wordt de spraakmodus automatisch uitgeschakeld en wordt het cijfertoetsenblok op het scherm gebruikt.

## Diagnostische logs

De App geeft ongestructureerde diagnostische gebeurtenissen door via Apple's standaard `OSLog`-framework (bijv. "studiesessie beëindigd, goed=12 fout=3"). Deze logs:

- Blijven op het apparaat.
- Zijn alleen voor jou zichtbaar, in Console.app terwijl het apparaat met een Mac is verbonden.
- Gebruiken Apple's `.private`-privacyclassificatie voor potentieel identificerende waarden (profiel-id, profielnaam), zodat die waarden in uitgeleverde builds worden afgeschermd.

We verzamelen, halen of verzenden geen `OSLog`-inhoud.

## Gegevens die we NIET verzamelen

- Je naam, e-mail of contactgegevens.
- Je locatie.
- Enige apparaat-identificator (IDFA, IDFV, advertentie-id).
- Crashrapporten verder dan wat Apple mogelijk via je iOS-instellingen verzamelt.
- Enige analyse of gedragstelemetrie.
- Betaal- of factureringsgegevens (aankopen worden volledig door Apple afgehandeld).

## Privacy van kinderen

Rekenen elke dag is ontworpen om veilig te zijn voor kinderen. Omdat de App geen persoonlijke gegevens verzamelt en geen derden contacteert, voldoet hij aan de definitie "geen persoonlijke gegevens" van de COPPA. We tonen geen advertenties, en er zijn geen accounts of sociale functies. Rekenen elke dag bevat één eenmalige in-app-aankoop (een ontgrendeling van de volledige app); omdat de app voor kinderen is ontworpen, wordt vóór elke aankoop een controle voor volwassenen getoond, zoals de regels van Apple's Kinderen-categorie vereisen. Alle betalingen en eventuele code-inwisselingen worden door Apple via de App Store afgehandeld. De App ziet of bewaart je betaalgegevens nooit.

## Jouw keuzes

- **Spraakmodus uitschakelen** op elk moment per profiel (Instellingen → Spraakmodus), of globaal door de microfoontoestemming te weigeren in de iOS-instellingen.
- **iCloud-synchronisatie uitschakelen** op elk moment (tandwielicoon → Instellingen → Synchronisatie → Gebruik iCloud → uit). Uitschakelen verwijdert geen iCloud-kopieën; verwijder elk profiel afzonderlijk als je ze wilt verwijderen.
- **Een gezin ontbinden of verlaten** (Instellingen → Gezin → Ontbind / Verlaten) om te stoppen met delen. Ontbinden trekt de toegang van deelnemers tot je gezin in; verlaten houdt de gezinsprofielen op je apparaat als je eigen.
- **Profielen naar een bestand exporteren** (Instellingen → Reservekopie → Exporteer) en lokaal bewaren: een handmatige reservekopie die iCloud nooit aanraakt.
- **De voortgang van een profiel resetten** zonder het profiel te verwijderen (profielinstellingen → Reset).
- **Een profiel verwijderen** (Beheer profielen → veeg of tik om te verwijderen): verwijdert ook de iCloud-kopie wanneer synchronisatie aanstaat. Herhaal per profiel om alles te verwijderen.

## Wijzigingen in dit beleid

Als we dit beleid wijzigen, is de nieuwe versie beschikbaar op dezelfde URL met een bijgewerkte datum **Laatst bijgewerkt**. Belangrijke wijzigingen worden ook vermeld in de release-opmerkingen van de App.

## Contact

Vragen over dit beleid of je gegevens? E-mail **spacedmath@gmail.com**.
