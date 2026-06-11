# Datenschutzrichtlinie — Mathe Täglich

**Datum des Inkrafttretens:** 2026-05-21
**Zuletzt aktualisiert:** 2026-06-10

Diese Richtlinie beschreibt, wie die iOS-App Mathe Täglich ("die App") mit Ihren Informationen umgeht. Sie gilt ab v1.0, einschließlich des v3-Modells für die Einzelhaushalt-CloudKit-Freigabe (das die profilbezogene Freigabe von v2.0 ersetzt).

## Zusammenfassung in einfachen Worten

- Wir betreiben keine Server. Wir erheben keine personenbezogenen Daten.
- Alles bleibt auf Ihrem Gerät, es sei denn, Sie aktivieren die **iCloud-Synchronisierung**. In diesem Fall speichert Apple — nicht wir — die Daten in Ihrem privaten iCloud-Konto.
- Die App verwendet Ihr Mikrofon nur, während Sie im Sprachmodus eine Aufgabe beantworten. Das Audio wird von Apples geräteinterner Spracherkennung (Siri-Klasse) verarbeitet und sofort verworfen; wir speichern, übertragen oder analysieren es niemals.
- Es gibt keine Tracker von Drittanbietern, keine Werbung und keine Analyse-SDKs.

## Was die App auf Ihrem Gerät speichert

- **Profile.** Name, Emoji, Farbe und profilbezogene Einstellungen.
- **Status des verteilten Wiederholens.** Für jede Karte (z. B. `7 + 8`): geplantes nächstes Wiederholungsdatum, Schwierigkeit, Stabilität und Anzahl der Wiederholungen.
- **Aktivität.** Eine tägliche Zählung der abgeschlossenen Wiederholungen pro Profil (verwendet für den Serien-Chip und den Statistik-Bildschirm).
- **Fehler.** Eine Warteschlange mit Aufgaben, die Sie kürzlich falsch beantwortet haben, damit die App sie erneut anzeigen kann.
- **Einstellungen.** App-weite Schalter, etwa ob die iCloud-Synchronisierung aktiviert ist.

All dies wird in den eigenen, abgeschotteten Dokumentenordner der App und in `UserDefaults` geschrieben. Die App kann die Daten anderer Apps nicht lesen, und andere Apps können die Daten der App nicht lesen.

## Was die App optional in iCloud speichert

Die iCloud-Synchronisierung ist **standardmäßig deaktiviert**. Wenn Sie sie aktivieren (Zahnradsymbol → **Einstellungen → Synchronisierung → iCloud verwenden**), schreibt die App dieselben oben beschriebenen Daten über Apples **CloudKit**-API in Ihre private iCloud. Das ist Ihre iCloud, die nur für Sie auf Geräten zugänglich ist, die bei derselben Apple-ID angemeldet sind. Wir haben keinen Zugriff darauf.

- Die genau synchronisierten Daten: Profile, Kartenstatus, Aktivität, Fehler und (optional) Metadaten der Haushaltsfreigabe (ein von Ihnen gewählter Anzeigename für Ihren Haushalt).
- Die iCloud-Synchronisierung umfasst **nicht** den Inhalt einer Sprachaufnahme oder irgendeine Analyse.
- Wenn Sie sich bei einer anderen Apple-ID anmelden, erkennt die App die Änderung und schaltet die Synchronisierung aus, bis Sie sie ausdrücklich wieder einschalten, damit keine Daten stillschweigend in ein anderes Konto hochgeladen werden.
- Das Löschen eines Profils unter **Profile verwalten** entfernt das Profil vom Gerät und (wenn iCloud unter der ursprünglichen Apple-ID erreichbar ist) auch aus Ihrer iCloud-Kopie.

## Haushaltsfreigabe

In v3 erfolgt die Freigabe auf **Haushaltsebene** statt pro Profil. Öffnen Sie das Zahnradsymbol → **Einstellungen → Haushalt → Haushalt einrichten**, benennen Sie Ihren Haushalt und laden Sie Familienmitglieder über das standardmäßige iOS-Teilen-Menü ein (Nachrichten, Mail oder AirDrop).

- Alle Profile auf dem Gerät des Eigentümers gehören zum Haushalt. Das Einladen eines Familienmitglieds gibt sie alle auf einmal frei.
- Die Daten liegen in der **iCloud des Haushaltseigentümers**. Teilnehmer speichern keine separate Kopie in ihrer eigenen iCloud; ihre Lernaktivität schreibt direkt in die CloudKit des Eigentümers über Apples zonenbezogenes CKShare-Berechtigungsmodell.
- Der Beitritt zu einem Haushalt ist **auf dem beitretenden Gerät unwiderruflich**: Die vorhandenen lokalen Profile des Teilnehmers werden durch die Profile des Haushalts ersetzt. Vor dem Beitritt bietet die App eine Option **Profile in Datei exportieren**, damit Sie eine JSON-Kopie Ihrer aktuellen Daten speichern und später erneut importieren können, falls Sie es sich anders überlegen.
- Wenn der Eigentümer den Haushalt auflöst (Einstellungen → Haushalt → Auflösen) oder sich von iCloud abmeldet, verlieren die Teilnehmer bei ihrer nächsten Synchronisierung den Live-Zugriff. Der lokale Cache der Haushaltsprofile wird zu ihrem eigenen (keine unwiderrufliche Löschung beim Verlassen).
- Ein Teilnehmer kann einen Haushalt jederzeit verlassen (Einstellungen → Haushalt → Verlassen). Beim Verlassen bleiben die Profile des Haushalts als eigene auf dem Gerät des Teilnehmers.
- Apples `CKShare`-Obergrenze liegt bei 100 Teilnehmern pro Freigabe. Die natürliche Haushaltsgröße liegt bei etwa 6.

## Exportieren / Importieren (JSON-Sicherung)

Unter **Einstellungen → Sicherung** können Sie:

- **Profile in Datei exportieren** — eine JSON-Datei mit jedem Profil auf dem aktuellen Gerät speichern (unabhängig vom Haushaltsstatus). Nützlich als manuelle Sicherung oder vor unwiderruflichen Aktionen.
- **Profile aus Datei importieren** — einen früheren Export wiederherstellen. Der **Zusammenführen**-Modus fügt fehlende Profile hinzu und aktualisiert vorhandene, wenn die importierte Kopie neuer ist. Der **Ersetzen**-Modus löscht lokale Profile und installiert den importierten Satz; nur verfügbar, wenn Sie sich nicht in einem Haushalt befinden.

## Mikrofon & Spracherkennung

Wenn der Sprachmodus aktiviert ist, während Sie eine Aufgabe beantworten, geht die App so vor:

1. Erfasst Live-Mikrofon-Audio mit `AVAudioEngine`.
2. Streamt es an `SFSpeechRecognizer` (Apples Framework). Auf modernen iOS-Geräten läuft die Erkennung standardmäßig auf dem Gerät; einige Konfigurationen können Apples Spracherkennungsserver verwenden.
3. Liest die transkribierten Ziffern und bewertet die Antwort.
4. Stoppt die Erfassung, sobald eine endgültige Antwort vorliegt.

Wir behalten kein Audio, keine Transkripte und kein abgeleitetes Signal. Wir übertragen kein Audio an Dritte außer an Apples `SFSpeechRecognizer`. Die App fordert `NSMicrophoneUsageDescription` und `NSSpeechRecognitionUsageDescription` bei der ersten Verwendung an; wird eine der beiden Berechtigungen verweigert, wird der Sprachmodus automatisch deaktiviert und die Tastatur auf dem Bildschirm verwendet.

## Diagnoseprotokolle

Die App gibt unstrukturierte Diagnoseereignisse über Apples standardmäßiges `OSLog`-Framework aus (z. B. "Lernsitzung beendet, richtig=12 falsch=3"). Diese Protokolle:

- Bleiben auf dem Gerät.
- Sind nur für Sie sichtbar, in der App "Console" (Konsole), während das Gerät mit einem Mac verbunden ist.
- Verwenden Apples `.private`-Datenschutzklassifizierung für potenziell personenbezogene Werte (Profil-ID, Profilname), sodass diese Werte in ausgelieferten Builds geschwärzt werden.

Wir erfassen, rufen oder übertragen keine `OSLog`-Inhalte.

## Daten, die wir NICHT erheben

- Ihren Namen, Ihre E-Mail oder Kontaktdaten.
- Ihren Standort.
- Jegliche Gerätekennung (IDFA, IDFV, Werbe-ID).
- Absturzberichte über das hinaus, was Apple möglicherweise über Ihre iOS-Einstellungen erfasst.
- Jegliche Analyse- oder Verhaltenstelemetrie.
- Zahlungs- oder Abrechnungsinformationen (Käufe werden vollständig von Apple abgewickelt).

## Datenschutz von Kindern

Mathe Täglich ist so gestaltet, dass es für Kinder sicher ist. Da die App keine personenbezogenen Daten erhebt und keine Dritten kontaktiert, erfüllt sie die Definition "keine personenbezogenen Daten" von COPPA. Wir zeigen keine Werbung an, und es gibt keine Konten oder sozialen Funktionen. Mathe Täglich enthält einen einzigen einmaligen In-App-Kauf (eine Freischaltung für die Vollversion); da die App für Kinder gestaltet ist, wird vor jedem Kauf eine Erwachsenenschranke angezeigt, wie es Apples Regeln für die Kinderkategorie verlangen. Alle Zahlungen und etwaige Code-Einlösungen werden von Apple über den App Store abgewickelt. Die App sieht oder speichert Ihre Zahlungsdaten niemals.

## Ihre Wahlmöglichkeiten

- **Sprachmodus deaktivieren** — jederzeit pro Profil (Einstellungen → Sprachmodus) oder global durch Verweigern der Mikrofonberechtigung in den iOS-Einstellungen.
- **iCloud-Synchronisierung deaktivieren** — jederzeit (Zahnradsymbol → Einstellungen → Synchronisierung → iCloud verwenden → aus). Das Deaktivieren löscht keine iCloud-Kopien; löschen Sie jedes Profil einzeln, wenn Sie sie entfernen möchten.
- **Einen Haushalt auflösen oder verlassen** (Einstellungen → Haushalt → Auflösen / Verlassen), um die Freigabe zu beenden. Das Auflösen widerruft den Zugriff der Teilnehmer auf Ihren Haushalt; beim Verlassen bleiben die Profile des Haushalts als Ihre eigenen auf Ihrem Gerät.
- **Profile in eine Datei exportieren** (Einstellungen → Sicherung → Exportieren) und lokal aufbewahren — eine manuelle Sicherung, die niemals iCloud berührt.
- **Den Fortschritt eines Profils zurücksetzen**, ohne das Profil zu löschen (profilbezogene Einstellungen → Zurücksetzen).
- **Ein Profil löschen** (Profile verwalten → wischen oder zum Löschen tippen) — entfernt auch die iCloud-Kopie, wenn die Synchronisierung aktiviert ist. Wiederholen Sie dies pro Profil, um alles zu entfernen.

## Änderungen dieser Richtlinie

Wenn wir diese Richtlinie ändern, ist die neue Version unter derselben URL mit einem aktualisierten Datum **Zuletzt aktualisiert** verfügbar. Wesentliche Änderungen werden auch in den Versionshinweisen der App vermerkt.

## Kontakt

Fragen zu dieser Richtlinie oder zu Ihren Daten? E-Mail **spacedmath@gmail.com**.
