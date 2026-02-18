# Affiliate Dashboard: Partnerize Payment Summary + Zeropark + Awin

Dashboard monitorujący **statusy płatności** z Partnerize oraz przychody z Zeropark i Awin.

## 🎯 Co monitoruje Partnerize?

Dashboard używa endpointu **Payment Summary**, który pokazuje **statusy płatności** (nie pojedyncze konwersje):

### Statusy płatności:
1. **PENDING** 💛 - Prowizje oczekujące na zatwierdzenie
2. **APPROVED** 💚 - Prowizje zatwierdzone przez reklamodawcę
3. **CONFIRMED** 💙 - Kwota potwierdzona, dostępna po opłaceniu faktury
4. **AVAILABLE** ✅ - Kwota dostępna do wypłaty TERAZ
5. **PAID** 🔵 - Już wypłacone

### Powiadomienia:
- 🔔 **Push notification** w przeglądarce gdy kwota się zmieni
- 📧 **Email** gdy kwota się zmieni
- 📝 **Log** wszystkich zmian w zakładce

---

## ⚙️ Konfiguracja

### Partnerize API (3 klucze)
1. Zaloguj się na Partnerize
2. Kliknij logo → **Account Settings**
3. Znajdź:
   - **Application Key** (User Application Key)
   - **User API Key** (User API Key)
   - **Publisher ID** (widoczny na górze strony)

### Zeropark API (1 klucz)
1. Zaloguj się na panel Zeropark
2. **Dashboard → My Account → Security**
3. Kliknij **"Create new API access token"**
4. Skopiuj **API Token**

### Awin API (2 klucze)
1. Zaloguj się na Awin
2. Przejdź do: **https://ui.awin.com/awin-api**
3. Wpisz hasło i kliknij **"Show my API token"**
4. Skopiuj **OAuth2 Bearer Token**
5. **Publisher ID** widoczny jest w Awin UI (u góry z lewej)

### Powiadomienia Email (opcjonalne)
1. Zarejestruj się na [emailjs.com](https://emailjs.com)
2. Dodaj **Email Service** (Gmail/Outlook)
3. Stwórz **Email Template**:
   ```
   Subject: Partnerize Status Change
   
   Changes detected:
   {{changes_html}}
   ```
4. Skopiuj: **Service ID**, **Template ID**, **Public Key**

---

## 🚀 Deployment na GitHub Pages

1. Utwórz repo: `affiliate-dashboard`
2. Wgraj plik: `partnerize-final.html` jako `index.html`
3. Settings → Pages → Source: `main` branch
4. Gotowe! Dashboard pod: `https://[username].github.io/affiliate-dashboard/`

---

## 📊 Jak działa wykrywanie zmian?

1. Dashboard pobiera payment summary co N minut (ustawiasz auto-refresh)
2. Porównuje kwoty dla każdego statusu+waluta
3. Jeśli kwota się zmienia → wysyła powiadomienie
4. Zmiana logowana w zakładce "Log powiadomień"

### Przykład powiadomienia:
```
Partnerize – zmiana prowizji
pending (GBP): £100.00 → £150.00
approved (GBP): £50.00 → £75.00
```

---

## 📱 Instalacja jako PWA (iPhone)

1. Otwórz w Safari
2. Kliknij przycisk **Udostępnij** (strzałka w górę)
3. **"Dodaj do ekranu głównego"**
4. Aplikacja działa jak natywna + powiadomienia push

---

## 🔧 Uwagi techniczne

- **Payment Summary** - bez parametrów daty, zawsze pokazuje aktualny stan
- **CORS Proxy** - używany `corsproxy.io` (dla produkcji zalecane własne proxy)
- **Auto-refresh** - ustawiane 1/5/15/30 min
- **Rate limits**: 
  - Partnerize: nie określone w dokumentacji
  - Zeropark: nie określone
  - Awin: 20 zapytań/minutę

---

## ❓ FAQ

**Q: Dlaczego kolumna "Count" pokazuje 0?**  
A: Payment Summary endpoint zwraca tylko sumy kwot, nie liczbę pojedynczych konwersji.

**Q: Dlaczego widzę tylko 5 statusów zamiast wszystkich konwersji?**  
A: To są **statusy płatności** (agregaty), nie pojedyncze konwersje. Jeśli chcesz widzieć pojedyncze konwersje, mogę dodać drugi endpoint.

**Q: Jak często sprawdzać zmiany?**  
A: Zalecane 15-30 min. Zmiany statusów płatności nie następują co minutę.

**Q: Czy mogę monitorować konkretną kampanię?**  
A: Payment Summary pokazuje wszystkie kampanie razem. Dla pojedynczych kampanii użyj conversion endpoint (inny).

---

## 📞 Wsparcie

Jeśli masz pytania lub problemy:
1. Sprawdź **Console** w przeglądarce (F12)
2. Upewnij się że wszystkie 3 klucze API są poprawne
3. Sprawdź czy base URL w Console to `api.partnerize.com` lub `api.performancehorizon.com`
