# Jira – czas pracy (oświadczenie KUP)

Aplikacja na Windows, która liczy czas pracy nad ticketami z Jiry na podstawie historii zmian
statusu, odejmuje spotkania z kalendarza Outlook i tworzy miesięczne oświadczenie o 50% kosztów
uzyskania przychodu (PDF).

## Pobierz

**[Pobierz instalator – JiraCzasPracy-setup.exe](https://github.com/pzukowicz/oswiadczenie-KUP-releases/releases/latest/download/JiraCzasPracy-setup.exe)**
(zawsze najnowsza wersja)

Wszystkie wersje i lista zmian: [Releases](https://github.com/pzukowicz/oswiadczenie-KUP-releases/releases).
Przy każdej wersji jest też `SHA256SUMS.txt` z sumą kontrolną instalatora.

## Instalacja

1. Uruchom pobrany `JiraCzasPracy-setup.exe`. Uprawnienia administratora nie są potrzebne:
   aplikacja instaluje się tylko dla Twojego konta Windows (`%LOCALAPPDATA%\Programs\JiraCzasPracy`).
2. Instalator nie jest podpisany cyfrowo, więc Windows może pokazać okno „System Windows ochronił
   ten komputer”. Kliknij wtedy **Więcej informacji → Uruchom mimo to**. Na laptopach zarządzanych
   przez firmę polityka bezpieczeństwa może zablokować niepodpisane programy. O dopuszczenie trzeba
   wtedy zapytać IT.
3. Aplikację uruchomisz z menu Start: **Jira – czas pracy**.

Wymagania: Windows 10 lub 11 (potrzebny .NET Framework 4.8 jest już w systemie). Oświadczenie
w PDF zapisuje zainstalowany Microsoft Word; bez Worda aplikacja zapisze plik .docx.

## Aktualizacja

Gdy jest nowsza wersja, aplikacja pokaże w pasku stanu „Dostępna nowa wersja X – zaktualizuj”.
Kliknij i potwierdź – aplikacja pobierze nową wersję (i sprawdzi jej sumę kontrolną), zamknie się,
zainstaluje ją i uruchomi się ponownie. Ustawienia i historia oświadczeń zostają.

Gdyby pobranie się nie udało (np. blokada w firmie), zamiast tego pojawi się link „pobierz”: pobierz
nowy instalator i uruchom go – zainstaluje się na starą wersję. Zainstalowaną wersję widać
w zakładce **Konfiguracja**, po prawej stronie. Link obok prowadzi do listy wersji.

## Pierwsze uruchomienie

1. Utwórz API token Jiry: <https://id.atlassian.com/manage-profile/security/api-tokens>, przycisk
   **Create API token**. Tokeny wygasają (maksymalnie po roku). Gdy pojawi się błąd 401, utwórz
   nowy.
2. W zakładce **Konfiguracja** wpisz adres Jiry, swój e-mail Atlassian i token, a potem kliknij
   **Połącz**.
3. Uzupełnij **Dane pracownika**: imię i nazwisko, PESEL / ID pracownika, stanowisko i przełożonego.
4. Jeśli chcesz odejmować spotkania, wklej link ICS kalendarza Outlook (instrukcja jest w aplikacji,
   w sekcji „Kalendarz Outlook”). Dopóki brakuje czegoś potrzebnego do oświadczenia, aplikacja
   startuje na zakładce Konfiguracja i pisze, co uzupełnić.
5. W zakładce **Oświadczenie** wybierz miesiąc i przejdź przez trzy kroki: urlop i dni wolne →
   tickety z Jiry (zaznacz te do oświadczenia) → spotkania i folder zapisu → **Generuj
   oświadczenie**.

## Twoje dane

Ustawienia zostają na Twoim komputerze, w `%APPDATA%\JiraCzasPracy\settings.json`: adres Jiry,
e-mail, dane pracownika i przełożonego, urlopy, zaznaczenia spotkań. API token, PESEL / ID
pracownika i link do kalendarza są zaszyfrowane (Windows DPAPI – odczyta je tylko Twoje konto
Windows). Kopie wygenerowanych oświadczeń (zakładka Historia) leżą w
`%APPDATA%\JiraCzasPracy\Oświadczenia`. Aplikacja tylko czyta dane z Jiry i wysyła token wyłącznie
pod wpisany adres Jiry. Przy starcie sprawdza na GitHubie, czy jest nowsza wersja, i pobiera ją
stamtąd – bez wysyłania żadnych Twoich danych.

Przy odinstalowaniu (Ustawienia Windows → Aplikacje) aplikacja zapyta, czy usunąć też ustawienia.
