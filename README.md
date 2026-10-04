# Snabbkalender

Minimal svensk röstapp för Outlook-kalendern.

## Funktioner
- En stor mikrofonknapp.
- Svensk röstigenkänning i webbläsaren.
- Förstår bl.a. "idag", "imorgon", veckodagar, "nästa torsdag", "14 oktober", "14/10", klockslag och enkel varaktighet.
- Kontrollerar Outlook-kalendern efter överlappande aktiviteter innan skapande.
- Vid krock skapas ingenting förrän användaren väljer "Lägg till ändå".
- Grön bekräftelse efter skapande.
- Ångra raderar endast den kalenderpost som appen precis skapade.
- Automatisk Outlook-påminnelse: 10 dagar före om aktiviteten ligger minst 10 dagar fram, 3 dagar före om minst 3 dagar fram, 1 dag före om minst 1 dag fram, annars 1 timme före.

## Microsoft-konfiguration (behövs en gång)
1. Skapa en appregistrering i Microsoft Entra admin center.
2. Välj kontotyper som ska kunna logga in. För både jobb/skola och privata Microsoft-konton: välj motsvarande multitenant + personal Microsoft accounts-alternativ.
3. Lägg till en **Single-page application (SPA)** redirect URI som exakt matchar adressen där appen körs, t.ex. `http://localhost:8080/` vid lokal test.
4. Lägg till delegerade Microsoft Graph-behörigheter: `User.Read` och `Calendars.ReadWrite`.
5. Kopiera **Application (client) ID**.
6. Öppna appens Inställningar och klistra in Client ID.

## Lokal test
Kör från denna mapp, exempelvis:

```bash
python -m http.server 8080
```

Öppna sedan `http://localhost:8080/` i Chrome. Filen bör inte öppnas direkt med `file://`, eftersom Microsoft-inloggning och PWA-funktioner behöver en webb-origin.

## Mobil
När appen ligger på HTTPS kan den öppnas i Chrome på Android och installeras som PWA via "Lägg till på startskärmen"/"Installera app".

## Säkerhetsmodell
Appen har ingen funktion som ändrar eller raderar tidigare kalenderposter. Den enda DELETE-operationen är Ångra på det event-ID som returnerades direkt efter att appen själv skapade posten.
