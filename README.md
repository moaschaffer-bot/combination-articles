# Kombinationsartikel — BackOffice-prototyp

Klickbar wireframe-prototyp för konfigurationsflödet av kombinationsartiklar i OpenPOS BackOffice.

## Vad prototypen visar

Flödet för att skapa en ny kombinationsartikel i BackOffice:

1. Fyll i namn, kassekategori och kvittovisning
2. Lägg till delar (t.ex. Förrätt / Varmrätt / Dessert)
3. Välj artiklar per del med sök och varugrupp-filter
4. Sätt ett defaultvärde per del
5. Spara kombinationsartikeln

## Filer

| Fil | Beskrivning |
|---|---|
| `index.html` | Komplett prototyp — all HTML, CSS och JS i en fil |
| `CONTEXT.md` | Fullständig projektbakgrund, designbeslut och terminologi |
| `README.md` | Den här filen |

## Köra lokalt

Öppna `index.html` direkt i webbläsaren — inga beroenden eller byggsteg krävs.

## GitHub Pages

Prototypen är live på: `https://[ditt-användarnamn].github.io/kombination-proto`

## Designspråk

Prototypen följer OpenPOS BackOffice visuella identitet:
- Primärfärg: `#5B4FCF` (lila)
- Bakgrund: `#F0EFF5`
- Typografi: system-UI sans-serif
- Komponenter: sidebar, topbar, cards, modala dialoger — samma mönster som befintlig BackOffice

## Status

**Under utveckling** — detta är en designprototyp, inte produktionskod.

Vad som återstår att designa:
- Prissättning per artikel i kombinationen
- Drag-and-drop för omsortering av delar  
- Kassavyn (steppern som servitören möter)
- Felhantering och validering

## Kontext

Se `CONTEXT.md` för fullständig bakgrund om projektet, use caset (Stadsteatern), momshantering, serveringslogik och öppna frågor.
