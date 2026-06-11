# Polityka prywatności — Mata Dzienna

**Data wejścia w życie:** 2026-05-21
**Ostatnia aktualizacja:** 2026-06-10

Ta polityka opisuje, jak aplikacja na iOS Mata Dzienna („Aplikacja") obchodzi się z Twoimi informacjami. Obowiązuje od v1.0 wzwyż, w tym model udostępniania CloudKit dla jednej rodziny z v3 (który zastępuje udostępnianie według profili z v2.0).

## Podsumowanie prostymi słowami

- Nie prowadzimy żadnych serwerów. Nie zbieramy żadnych informacji osobowych.
- Wszystko pozostaje na Twoim urządzeniu, chyba że włączysz **synchronizację iCloud**; w takim przypadku to Apple, a nie my, przechowuje dane na Twoim prywatnym koncie iCloud.
- Aplikacja używa mikrofonu tylko, gdy odpowiadasz na zadanie w trybie głosowym. Dźwięk jest przetwarzany przez rozpoznawanie mowy Apple (na urządzeniu, klasy Siri) i natychmiast odrzucany; nigdy go nie przechowujemy, nie przesyłamy ani nie analizujemy.
- Nie ma żadnych zewnętrznych trackerów, reklam ani SDK analitycznych.

## Co Aplikacja przechowuje na Twoim urządzeniu

- **Profile.** Nazwa, emoji, kolor i ustawienia profilu.
- **Stan powtórek w odstępach.** Dla każdej karty (np. `7 + 8`): zaplanowana data następnej powtórki, trudność, stabilność i liczba powtórek.
- **Aktywność.** Dzienne zliczenie ukończonych powtórek na profil (używane do plakietki serii i ekranu statystyk).
- **Błędy.** Kolejka zadań, na które ostatnio odpowiedziałeś błędnie, aby Aplikacja mogła pokazać je ponownie.
- **Preferencje.** Przełączniki całej Aplikacji, np. czy synchronizacja iCloud jest włączona.

Wszystko to jest zapisywane we własnym, odizolowanym folderze Dokumenty Aplikacji oraz w `UserDefaults`. Aplikacja nie może czytać danych innych aplikacji, a inne aplikacje nie mogą czytać danych Aplikacji.

## Co Aplikacja opcjonalnie przechowuje w iCloud

Synchronizacja iCloud jest **domyślnie wyłączona**. Gdy ją włączysz (ikona koła zębatego → **Ustawienia → Synchronizacja → Używaj iCloud**), Aplikacja zapisuje te same dane opisane powyżej w Twoim prywatnym iCloud przez API **CloudKit** Apple. To Twój iCloud, dostępny tylko dla Ciebie na urządzeniach zalogowanych tym samym Apple ID. Nie mamy do niego dostępu.

- Dokładnie synchronizowane dane: profile, stany kart, aktywność, błędy oraz (opcjonalnie) metadane udostępniania rodziny (nazwa wyświetlana, którą wybierzesz dla swojej rodziny).
- Synchronizacja iCloud **nie** obejmuje treści żadnego nagrania głosowego ani żadnej analityki.
- Gdy zalogujesz się innym Apple ID, Aplikacja wykrywa zmianę i wyłącza synchronizację, dopóki nie włączysz jej ponownie, aby dane nie zostały po cichu przesłane na inne konto.
- Usunięcie profilu w **Zarządzaj profilami** usuwa profil z urządzenia oraz (gdy iCloud jest osiągalny na pierwotnym Apple ID) z Twojej kopii iCloud.

## Udostępnianie rodziny

W v3 udostępnianie odbywa się na poziomie **rodziny**, a nie według profilu. Otwórz ikonę koła zębatego → **Ustawienia → Rodzina → Skonfiguruj rodzinę**, nadaj rodzinie nazwę i zaproś bliskich przez standardowy arkusz udostępniania iOS (Wiadomości, Mail lub AirDrop).

- Wszystkie profile na urządzeniu właściciela należą do rodziny. Zaproszenie jednego członka rodziny udostępnia je wszystkie naraz.
- Dane znajdują się w **iCloud właściciela rodziny**. Uczestnicy nie przechowują osobnej kopii we własnym iCloud; ich aktywność nauki jest zapisywana bezpośrednio w CloudKit właściciela przez ograniczony do strefy model uprawnień CKShare Apple.
- Dołączenie do rodziny jest **nieodwracalne na dołączającym urządzeniu**: istniejące lokalne profile uczestnika są zastępowane profilami rodziny. Przed dołączeniem Aplikacja oferuje opcję **Eksportuj profile do pliku**, abyś zapisał kopię JSON bieżących danych i mógł ją później ponownie zaimportować, jeśli zmienisz zdanie.
- Jeśli właściciel rozwiąże rodzinę (Ustawienia → Rodzina → Rozwiąż) lub wyloguje się z iCloud, uczestnicy tracą dostęp na żywo przy następnej synchronizacji. Lokalna pamięć podręczna profili rodziny staje się ich własna (bez nieodwracalnego usuwania przy wyjściu).
- Uczestnik może opuścić rodzinę w dowolnej chwili (Ustawienia → Rodzina → Opuść). Wychodząc, zachowuje profile rodziny na swoim urządzeniu jako własne.
- Limit `CKShare` Apple to 100 uczestników na udostępniony element. Naturalna skala rodziny to ~6.

## Eksport / Import (kopia zapasowa JSON)

W **Ustawienia → Kopia zapasowa** możesz:

- **Eksportuj profile do pliku** — zapisać plik JSON zawierający wszystkie profile bieżącego urządzenia (niezależnie od stanu rodziny). Przydatne jako ręczna kopia zapasowa lub przed nieodwracalnymi operacjami.
- **Importuj profile z pliku** — przywrócić poprzedni eksport. Tryb **Scal** dodaje brakujące profile i aktualizuje istniejące, jeśli zaimportowana kopia jest nowsza. Tryb **Zastąp** kasuje lokalne profile i instaluje zaimportowany zestaw; dostępny tylko, gdy nie jesteś w rodzinie.

## Mikrofon i rozpoznawanie mowy

Gdy tryb głosowy jest włączony, podczas odpowiadania na zadanie Aplikacja:

1. Przechwytuje dźwięk mikrofonu na żywo za pomocą `AVAudioEngine`.
2. Przesyła go do `SFSpeechRecognizer` (framework Apple). Na nowoczesnych urządzeniach iOS rozpoznawanie domyślnie działa na urządzeniu; niektóre konfiguracje mogą używać serwerów rozpoznawania mowy Apple.
3. Odczytuje przepisane cyfry i ocenia odpowiedź.
4. Zatrzymuje przechwytywanie, gdy tylko uzyskano ostateczną odpowiedź.

Nie zachowujemy dźwięku, transkrypcji ani żadnego sygnału pochodnego. Nie przesyłamy dźwięku do żadnej strony poza `SFSpeechRecognizer` Apple. Aplikacja prosi o `NSMicrophoneUsageDescription` i `NSSpeechRecognitionUsageDescription` przy pierwszym użyciu; jeśli którekolwiek z uprawnień zostanie odrzucone, tryb głosowy jest automatycznie wyłączany i używana jest ekranowa klawiatura numeryczna.

## Dzienniki diagnostyczne

Aplikacja wysyła nieustrukturyzowane zdarzenia diagnostyczne przez standardowy framework `OSLog` Apple (np. „sesja nauki zakończona, poprawne=12 błędne=3"). Te dzienniki:

- Pozostają na urządzeniu.
- Są widoczne tylko dla Ciebie, w Console.app, gdy urządzenie jest podłączone do Maca.
- Używają klasyfikacji prywatności Apple `.private` dla wszelkich potencjalnie identyfikujących wartości (id profilu, nazwa profilu), więc w wydanych kompilacjach te wartości są ukryte.

Nie zbieramy, nie pobieramy ani nie przesyłamy treści `OSLog`.

## Dane, których NIE zbieramy

- Twojego imienia, e-maila ani danych kontaktowych.
- Twojej lokalizacji.
- Żadnego identyfikatora urządzenia (IDFA, IDFV, id reklamowy).
- Raportów o awariach poza tym, co Apple może zbierać przez Twoje ustawienia iOS.
- Żadnej analityki ani telemetrii zachowań.
- Informacji o płatności lub rozliczeniach (zakupy są w całości obsługiwane przez Apple).

## Prywatność dzieci

Mata Dzienna jest zaprojektowana tak, aby była bezpieczna dla dzieci. Ponieważ Aplikacja nie zbiera informacji osobowych i nie kontaktuje się z osobami trzecimi, spełnia definicję „brak informacji osobowych" z COPPA. Nie wyświetlamy reklam i nie ma kont ani funkcji społecznościowych. Mata Dzienna zawiera jeden jednorazowy zakup w aplikacji (odblokowanie pełnej aplikacji); ponieważ aplikacja jest przeznaczona dla dzieci, przed każdym zakupem wyświetlana jest weryfikacja dla dorosłych, zgodnie z wymaganiami reguł kategorii Dzieci Apple. Wszystkie płatności i realizacje kodów są obsługiwane przez Apple za pośrednictwem App Store. Aplikacja nigdy nie widzi ani nie przechowuje Twoich danych płatniczych.

## Twoje wybory

- **Wyłączyć tryb głosowy** w dowolnej chwili dla profilu (Ustawienia → Tryb głosowy) lub globalnie, odmawiając uprawnienia mikrofonu w ustawieniach iOS.
- **Wyłączyć synchronizację iCloud** w dowolnej chwili (ikona koła zębatego → Ustawienia → Synchronizacja → Używaj iCloud → wył.). Wyłączenie nie usuwa kopii w iCloud; usuń każdy profil osobno, jeśli chcesz je usunąć.
- **Rozwiązać lub opuścić rodzinę** (Ustawienia → Rodzina → Rozwiąż / Opuść), aby przestać udostępniać. Rozwiązanie odbiera uczestnikom dostęp do Twojej rodziny; opuszczenie zachowuje profile rodziny na Twoim urządzeniu jako własne.
- **Eksportować profile do pliku** (Ustawienia → Kopia zapasowa → Eksportuj) i trzymać go lokalnie — ręczna kopia zapasowa, która nigdy nie dotyka iCloud.
- **Zresetować postęp profilu** bez usuwania profilu (Ustawienia profilu → Resetuj).
- **Usunąć profil** (Zarządzaj profilami → przesuń lub dotknij, aby usunąć) — przy włączonej synchronizacji usuwa to też kopię w iCloud. Powtórz dla każdego profilu, aby usunąć wszystko.

## Zmiany tej polityki

Jeśli zmienimy tę politykę, nowa wersja będzie dostępna pod tym samym adresem URL ze zaktualizowaną datą **Ostatnia aktualizacja**. O istotnych zmianach poinformujemy też w informacjach o wydaniu Aplikacji.

## Kontakt

Pytania o tę politykę lub Twoje dane? E-mail **spacedmath@gmail.com**.
