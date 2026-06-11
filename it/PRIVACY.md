---
title: "Mate ogni giorno"
description: "Esercizi di matematica con ripetizione dilazionata per iPhone e iPad"
---

# Informativa sulla privacy — Mate ogni giorno

**Data di entrata in vigore:** 2026-05-21
**Ultimo aggiornamento:** 2026-06-10

Questa informativa descrive come l'app iOS Mate ogni giorno ("l'App") tratta le tue informazioni. Si applica dalla v1.0 in poi, incluso il modello di condivisione CloudKit a famiglia singola della v3 (che sostituisce la condivisione per profilo della v2.0).

## Riepilogo in parole semplici

- Non gestiamo alcun server. Non raccogliamo alcuna informazione personale.
- Tutto rimane sul tuo dispositivo a meno che tu non attivi la **sincronizzazione iCloud**, nel qual caso è Apple, non noi, a memorizzarlo nel tuo account iCloud privato.
- L'App usa il microfono solo mentre rispondi a un problema in modalità voce. L'audio è elaborato dal riconoscimento vocale di Apple (sul dispositivo, di classe Siri) e scartato immediatamente; non lo memorizziamo, carichiamo o analizziamo mai.
- Non ci sono tracker di terze parti, né pubblicità, né SDK di analisi.

## Cosa memorizza l'App sul tuo dispositivo

- **Profili.** Nome, emoji, colore e impostazioni per profilo.
- **Stato di ripetizione dilazionata.** Per ogni carta (es. `7 + 8`): data del prossimo ripasso, difficoltà, stabilità e numero di ripassi.
- **Attività.** Un conteggio giornaliero dei ripassi completati per profilo (usato per l'etichetta della serie e la schermata Statistiche).
- **Errori.** Una coda di problemi che hai risposto male di recente, così l'App può riproporli.
- **Preferenze.** Interruttori a livello di App, come l'attivazione o meno della sincronizzazione iCloud.

Tutto questo viene scritto nella cartella Documenti isolata della stessa App e in `UserDefaults`. L'App non può leggere i dati di altre app, e altre app non possono leggere i dati dell'App.

## Cosa memorizza facoltativamente l'App in iCloud

La sincronizzazione iCloud è **disattivata per impostazione predefinita**. Quando la attivi (icona dell'ingranaggio → **Impostazioni → Sincronizzazione → Usa iCloud**), l'App scrive gli stessi dati descritti sopra nel tuo iCloud privato tramite l'API **CloudKit** di Apple. È il tuo iCloud, accessibile solo a te sui dispositivi con accesso effettuato con lo stesso ID Apple. Noi non vi abbiamo accesso.

- I dati esattamente sincronizzati: profili, stati delle carte, attività, errori e (facoltativamente) i metadati della condivisione della famiglia (un nome a tua scelta per la tua famiglia).
- La sincronizzazione iCloud **non** include il contenuto di alcuna registrazione vocale né alcuna analisi.
- Quando accedi con un ID Apple diverso, l'App rileva il cambiamento e disattiva la sincronizzazione finché non la riattivi esplicitamente, così i dati non vengono caricati in silenzio su un altro account.
- Eliminare un profilo da **Gestisci profili** rimuove il profilo dal dispositivo e (quando iCloud è raggiungibile sull'ID Apple originario) anche dalla tua copia iCloud.

## Condivisione della famiglia

Nella v3, la condivisione avviene a livello di **famiglia** anziché per profilo. Apri l'icona dell'ingranaggio → **Impostazioni → Famiglia → Configura famiglia**, dai un nome alla tua famiglia e invita i familiari tramite il foglio di condivisione standard di iOS (Messaggi, Mail o AirDrop).

- Tutti i profili sul dispositivo del proprietario appartengono alla famiglia. Invitare un familiare li condivide tutti in una volta.
- I dati risiedono nell'**iCloud del proprietario della famiglia**. I partecipanti non memorizzano una copia separata nel proprio iCloud; la loro attività di studio viene scritta direttamente nel CloudKit del proprietario tramite il modello di autorizzazioni CKShare con ambito di zona di Apple.
- Unirsi a una famiglia è **distruttivo sul dispositivo che si unisce**: i profili locali esistenti del partecipante vengono sostituiti con quelli della famiglia. Prima di unirsi, l'App offre l'opzione **Esporta i profili in un file** per salvare una copia JSON dei dati attuali e reimportarla più tardi in caso di ripensamento.
- Se il proprietario scioglie la famiglia (Impostazioni → Famiglia → Sciogli) o esce da iCloud, i partecipanti perdono l'accesso in tempo reale al loro prossimo aggiornamento. La cache locale dei profili della famiglia diventa la loro (nessuna cancellazione distruttiva all'uscita).
- Un partecipante può lasciare una famiglia in qualsiasi momento (Impostazioni → Famiglia → Esci). Uscendo, mantiene i profili della famiglia sul proprio dispositivo come propri.
- Il limite `CKShare` di Apple è di 100 partecipanti per elemento condiviso. La scala naturale di una famiglia è di circa 6.

## Esporta / Importa (backup JSON)

In **Impostazioni → Backup** puoi:

- **Esporta i profili in un file**: salvare un file JSON contenente tutti i profili del dispositivo attuale (qualsiasi stato della famiglia). Utile come backup manuale o prima di operazioni distruttive.
- **Importa i profili da un file**: ripristinare un'esportazione precedente. La modalità **Unisci** aggiunge i profili mancanti e aggiorna quelli esistenti se la copia importata è più recente. La modalità **Sostituisci** cancella i profili locali e installa l'insieme importato; disponibile solo quando non sei in una famiglia.

## Microfono e riconoscimento vocale

Quando la modalità voce è attiva, mentre rispondi a un problema l'App:

1. Cattura l'audio dal microfono dal vivo con `AVAudioEngine`.
2. Lo trasmette a `SFSpeechRecognizer` (il framework di Apple). Sui dispositivi iOS moderni il riconoscimento viene eseguito sul dispositivo per impostazione predefinita; alcune configurazioni possono usare i server di riconoscimento vocale di Apple.
3. Legge le cifre trascritte e valuta la risposta.
4. Interrompe la cattura non appena si ottiene una risposta finale.

Non conserviamo audio, trascrizioni o alcun segnale derivato. Non trasmettiamo audio ad alcuna parte diversa dal `SFSpeechRecognizer` di Apple. L'App richiede `NSMicrophoneUsageDescription` e `NSSpeechRecognitionUsageDescription` al primo utilizzo; se una delle autorizzazioni viene negata, la modalità voce viene disattivata automaticamente e si usa il tastierino numerico sullo schermo.

## Registri diagnostici

L'App emette eventi diagnostici non strutturati tramite il framework standard `OSLog` di Apple (es. "sessione di studio terminata, corrette=12 sbagliate=3"). Questi registri:

- Restano sul dispositivo.
- Sono visibili solo a te, in Console.app mentre il dispositivo è collegato a un Mac.
- Usano la classificazione di privacy `.private` di Apple per qualsiasi valore potenzialmente identificativo (id profilo, nome profilo), così quei valori sono oscurati nelle versioni pubblicate.

Non raccogliamo, recuperiamo né trasmettiamo il contenuto di `OSLog`.

## Dati che NON raccogliamo

- Il tuo nome, e-mail o recapiti.
- La tua posizione.
- Qualsiasi identificatore del dispositivo (IDFA, IDFV, id pubblicitario).
- Rapporti sugli arresti anomali oltre a quanto Apple può raccogliere tramite le tue impostazioni iOS.
- Qualsiasi analisi o telemetria comportamentale.
- Informazioni di pagamento o fatturazione (gli acquisti sono gestiti interamente da Apple).

## Privacy dei minori

Mate ogni giorno è progettata per essere sicura per i bambini. Poiché l'App non raccoglie informazioni personali e non contatta terze parti, rispetta la definizione "nessuna informazione personale" della COPPA. Non mostriamo pubblicità e non ci sono account né funzioni social. Mate ogni giorno include un singolo acquisto in-app (uno sblocco dell'app completa); poiché l'app è progettata per i bambini, prima di ogni acquisto viene mostrata una verifica per adulti, come richiesto dalle regole della categoria Bambini di Apple. Tutti i pagamenti ed eventuali riscatti di codici sono gestiti da Apple tramite l'App Store. L'App non vede né memorizza mai i tuoi dati di pagamento.

## Le tue scelte

- **Disattivare la modalità voce** in qualsiasi momento per profilo (Impostazioni → Modalità voce) o globalmente negando l'autorizzazione del microfono nelle Impostazioni di iOS.
- **Disattivare la sincronizzazione iCloud** in qualsiasi momento (icona dell'ingranaggio → Impostazioni → Sincronizzazione → Usa iCloud → disattiva). Disattivarla non elimina le copie iCloud; elimina ogni profilo singolarmente se vuoi rimuoverle.
- **Sciogliere o lasciare una famiglia** (Impostazioni → Famiglia → Sciogli / Esci) per smettere di condividere. Sciogliere revoca l'accesso dei partecipanti alla tua famiglia; uscire mantiene i profili della famiglia sul tuo dispositivo come propri.
- **Esportare i profili in un file** (Impostazioni → Backup → Esporta) e conservarlo localmente: un backup manuale che non tocca mai iCloud.
- **Reimpostare i progressi di un profilo** senza eliminare il profilo (Impostazioni del profilo → Reimposta).
- **Eliminare un profilo** (Gestisci profili → scorri o tocca per eliminare): rimuove anche la copia iCloud quando la sincronizzazione è attiva. Ripeti per profilo per rimuovere tutto.

## Modifiche a questa informativa

Se modifichiamo questa informativa, la nuova versione sarà disponibile allo stesso URL con una data di **Ultimo aggiornamento** aggiornata. Le modifiche sostanziali saranno indicate anche nelle note di versione dell'App.

## Contatto

Domande su questa informativa o sui tuoi dati? E-mail **spacedmath@gmail.com**.
