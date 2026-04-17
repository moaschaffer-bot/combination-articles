# Kontext — Kombinationsartiklar (P2)

## Om projektet
Detta är ett designprojekt för **OpenPOS BackOffice** — ett kassasystem riktat mot restauranger, hotell och liknande verksamheter. Produkten heter **OPEN Two** (app) och **BackOffice** (webbaserat admingränssnitt).

Projektet handlar om att designa och prototypa flödet för att skapa och konfigurera **kombinationsartiklar** i BackOffice — ett nytt feature-koncept som ännu inte är byggt.

---

## Projektstruktur (interna prioriteringar)

| Projekt | Prioritet | Status |
|---|---|---|
| P1 – Avancerade serveringar | PRIO 1 | Pågående |
| P2 – Kombinationsartiklar | PRIO 2 | Tidig fas / design |

**P2 är beroende av P1** — kombinationsartiklar förutsätter att avancerade serveringar är implementerat, eftersom serveringar skapas automatiskt när en kombination läggs till i varukorgen.

---

## Use case (Stadsteatern)

Primär kund som efterfrågat funktionen. Deras behov:

- En **kassaknapp per kombination** (t.ex. "Stora menyn", "Lilla menyn")
- Knappen triggar en **stepper** i kassan med obligatoriska, förkonfigurerade steg
- Varje steg = en del av menyn (Förrätt / Varmrätt / Dessert)
- Varje steg har ett **defaultvärde** men kan bytas av servitören
- När steppern är klar läggs kombinationen i varukorgen

### Köksflöde
- Serveringar skapas **automatiskt** när kombinationen läggs till i varukorgen — en servering per steg
- Om en servering av samma typ redan är öppen läggs artiklarna till i den befintliga (inte en ny)
- Köket ser **aldrig** "Stora menyn" — bara de valda komponenterna, routade via bongkategorier till rätt station
- Logiken: servering = tidsdimension (när), bongkategori = rumsdimension (vart)

### Kvitto
- Styrbart via BackOffice-inställning på företagsnivå
- Alternativ 1: Totalpris — "Stora menyn · 230 kr"
- Alternativ 2: Per del — "Förrätt: Laxtataki · 80 kr, Varmrätt: ..."

---

## Momshantering

Varje ingående artikel behåller sin egen momssats. Priset per artikel sätts om manuellt i kombinationen. Momsen beräknas proportionellt:

**Exempel:** Pizza (12% moms) = 150 kr, Vin (25% moms) = 80 kr → totalt 230 kr
- Moms pizza: (150/230) × 0,12
- Moms vin: (80/230) × 0,25

---

## Serveringslogik (koppling till P1)

Serveringar i BackOffice konfigureras som egna objekt med namn och prioritet:
- Förrätt (1), Varmrätt (2), Dessert (3)
- Artiklar kopplas till serveringar i BackOffice
- Serveringar och bongkategorier är **separata dimensioner** — de ska inte slås ihop

Beteende vid automatisk skapande:
- Om servering av samma typ finns öppen → lägg till i den
- Om inte → skapa ny

---

## BackOffice-flöde (designat i prototypen)

Konfigurationsflödet för en kombinationsartikel i BackOffice:

1. **Grunduppgifter** — Namn, kassekategori, kvittovisning
2. **Delar** — Lägg till delar (steg i steppern), ge dem namn, välj artiklar per del, sätt defaultvärde
3. **Artikelväljaren** — Sök + varugrupp-filter, bulk-val, "Sätt som standard" per artikel
4. **Spara** — Kombinationen blir tillgänglig som kassaknapp

### UX-beslut i designen
- Delar är expanderbara/ihopfällbara — öppen del visar artikelväljaren, stängd visar pills
- Drag handle för omsortering (ej implementerat i prototypen ännu)
- "Lägg till del" → inline namnfält (ingen modal) → direkt till artikelväljaren
- Toast-bekräftelse när en del sparas
- Artikelväljaren: sök-först + varugrupp som filter (skalbart från 30 till 400+ artiklar)

---

## Terminologi (använd konsekvent)

| Term | Förklaring |
|---|---|
| Kombinationsartikel | Det nya konceptet — en artikel som består av valbara delar |
| Del | Ett steg i kombinationen (t.ex. Förrätt, Varmrätt) |
| Servering | Tidsgrupperingen i köksflödet — kopplas till artiklar, inte delar |
| Bongkategori | Styr vart en bong skickas (printer/station) |
| Stepper | UI-mönstret i kassan där servitören väljer per steg |
| Standard | Defaultvärdet för ett steg i steppern |
| BackOffice | Webbgränssnittet för adminkonfiguration |

---

## UX Copy-principer (från intern skill)

- Svenska: du-form, bisatser, imperativ på knappar, meningsfallet
- Knappar: verb + objekt — "Välj artiklar", "Spara kombinationsartikel", "Lägg till del"
- Fältrubriker: substantiv — "Kvittovisning", "Namn", "Kassekategori"
- Toasts: specifika — "Förrätt sparad – 3 artiklar valda"
- Hjälptexter: korta, utan jargong — "Visas i kassan och på köksbon gen"

---

## Öppna frågor / blockerare

- Lageravdrag är designat men ej byggt — stort arbete, ej i scope för P2 MVP
- Receptflödet (drinkar/ingredienser) är en separat variant av konceptet — ej prioriterat nu
- Drag-and-drop för omsortering av delar är ej implementerat i prototypen
- Kombinationspriset per artikel sätts manuellt — BackOffice-flödet för detta är ej designat än (steg 4 i flödet ovan)

---

## Relaterade projekt att känna till

**P1 – Avancerade serveringar** (Sjömagasinet-möte 16/4):
- Serveringar skapas automatiskt när artiklar läggs i varukorgen
- Fire-knapp (låst/fri?) — öppen fråga
- BackOffice-inställning för serverings-konfiguration
- Blockerare: printer category vs egna kategorier
