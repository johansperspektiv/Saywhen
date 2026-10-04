# Saywhen

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

## PWA-identitet
- Appnamn: `Saywhen`
- Manifest-ID: `/Saywhen/`
- Start URL: `/Saywhen/`
- Scope: `/Saywhen/`
- Cache: `saywhen-v2`
- Gamla PWA-cachar rensas automatiskt när den nya service workern aktiveras.

## Microsoft-konfiguration (behövs en gång)
1. Skapa en appregistrering i Microsoft Entra admin center.
2. Välj kontotyper som ska kunna logga in. För både jobb/skola och privata Microsoft-konton: välj motsvarande multitenant + personal Microsoft accounts-alternativ.
3. Lägg till en **Single-page application (SPA)** redirect URI som exakt matchar den publicerade appen: `https://johansperspektiv.github.io/Saywhen/`
4. Lägg till delegerade Microsoft Graph-behörigheter: `User.Read` och `Calendars.ReadWrite`.
5. Kopiera **Application (client) ID**.
6. Öppna appens Inställningar och klistra in Client ID.

## Publicering på GitHub Pages
Lägg filerna i roten av repot `Saywhen` så att `index.html` ligger direkt där. Publicerad adress:

`https://johansperspektiv.github.io/Saywhen/`

Efter uppladdning, öppna sidan i Chrome på Android. Om telefonen fortfarande visar den gamla PWA-identiteten, rensa webbplatsdata för `johansperspektiv.github.io` en gång och öppna sidan igen.

## Lokal test
Eftersom manifestet är anpassat för GitHub Pages-sökvägen `/Saywhen/` är enklaste lokala testet att servera från en överordnad mapp där projektmappen heter `Saywhen`.

Exempel från `/mnt/data` eller motsvarande överordnad mapp:

```bash
python -m http.server 8080
```

Öppna sedan `http://localhost:8080/Saywhen/`.

## Säkerhetsmodell
Appen har ingen funktion som ändrar eller raderar tidigare kalenderposter. Den enda DELETE-operationen är Ångra på det event-ID som returnerades direkt efter att appen själv skapade posten.
