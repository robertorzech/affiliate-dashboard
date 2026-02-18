# Affiliate Dashboard: Partnerize, Zeropark & Awin

Unified dashboard do monitorowania prowizji i przychodów z trzech głównych platform affiliate: Partnerize, Zeropark i Awin — z powiadomieniami push i email.

## Funkcje
- 📊 **Partnerize**: Widok prowizji wg statusów (Pending, Approved, Rejected, Paid, itp.)
- 💰 **Zeropark**: Przychód wczoraj i w bieżącym miesiącu
- 🏆 **Awin**: Prowizje wczoraj, w miesiącu + breakdown według statusu i advertiserów
- 🔔 Powiadomienia push w przeglądarce/telefonie (dla Partnerize)
- 📧 Powiadomienia email przez EmailJS (dla Partnerize)
- 🔄 Auto-odświeżanie (co 1/5/15/30 min)
- 📱 Działa jako PWA (dodaj do ekranu głównego iPhone)
- 💾 Zapamiętuje klucze API i ustawienia (localStorage)

## Wdrożenie na GitHub Pages

1. Stwórz nowe repozytorium na GitHub (np. `affiliate-dashboard`)
2. Wgraj oba pliki: `index.html` i `manifest.json`
3. Wejdź w Settings → Pages → Source: `main` branch
4. Aplikacja dostępna pod: `https://robertorzech.github.io/affiliate-dashboard/`

## Konfiguracja przy pierwszym uruchomieniu

### Partnerize API
- Zaloguj się na Partnerize
- Przejdź do: **Account → API Keys**
- Skopiuj swój **User API Key**

### Zeropark API
- Skontaktuj się z **Zeropark Publisher Team**
- Otrzymasz:
  - **API Token**
  - **Domainer ID**

### Awin API
- Zaloguj się na Awin
- Przejdź do: **https://ui.awin.com/awin-api**
- Wpisz hasło i kliknij **"Show my API token"**
- Skopiuj **OAuth2 Bearer Token**
- Twój **Publisher ID** widoczny jest w UI Awin po zalogowaniu (u góry z lewej)

### Powiadomienia email (opcjonalne) – EmailJS
1. Zarejestruj się bezpłatnie na [emailjs.com](https://emailjs.com)
2. Dodaj **Email Service** (np. Gmail) → zapisz `Service ID`
3. Stwórz **Email Template** z polami:
   - `{{to_email}}` – adresat
   - `{{subject}}` – temat
   - `{{message}}` – treść zmian
   - `{{changes_html}}` – zmiany w HTML
4. Skopiuj `Template ID` i `Public Key` z zakładki Account

## Zakładki

### Partnerize
- Przegląd prowizji według statusów
- Wykrywanie zmian statusów
- Powiadomienia push i email
- Log zmian

### Zeropark
- Przychód wczoraj (Revenue, Sold Visits, Avg CPM)
- Przychód w bieżącym miesiącu (suma)
- Tabela z dziennymi statystykami:
  - Requested Visits
  - Accepted Visits
  - Sold Visits
  - Revenue
  - Average CPM

### Awin
- Prowizje wczoraj
- Prowizje w bieżącym miesiącu
- Pending prowizje
- Approved prowizje
- Breakdown według statusu (pending, approved, declined, etc.)
- Top 10 Advertisers (według prowizji)

## Powiadomienia na iPhone
1. Otwórz aplikację w Safari
2. Kliknij przycisk **Udostępnij** (ikona z strzałką w górę)
3. Wybierz **"Dodaj do ekranu głównego"**
4. Aplikacja działa jak natywna apka — zezwól na powiadomienia

## Uwagi techniczne
- Wszystkie API wymagają proxy CORS dla żądań przeglądarkowych
- Aplikacja używa `corsproxy.io` jako publicznego proxy
- Dla produkcji zalecane własne proxy lub backend
- Dane API i log zmian przechowywane lokalnie w przeglądarce
- Awin używa OAuth2 Bearer Token (max 20 zapytań/minutę)
- Możesz używać tylko jednego API lub wszystkich trzech jednocześnie
