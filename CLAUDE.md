# Financiële APK

## Over dit project

Een Nederlandstalige single-page webapp die gebruikers in 3 minuten inzicht geeft in hun financiële gezondheid. De tool is bedoeld als leadgeneratie-instrument: vertrouwen opbouwen door persoonlijk inzicht te geven, een "gap" zichtbaar maken, en leiden naar een adviesgesprek.

**Live URL:** https://southparc.github.io/financiele-apk/
**Repository:** https://github.com/southparc/financiele-apk

## Mappenstructuur

```
financiele-apk/
├── index.html              # De volledige applicatie (HTML + CSS + JS in één bestand)
├── .github/
│   └── workflows/
│       └── deploy.yml      # GitHub Pages deployment (automatisch bij push naar main)
└── CLAUDE.md
```

Alles zit in één `index.html` — geen build tools, geen frameworks, geen afhankelijkheden.

## Applicatiestructuur

De app heeft 5 fases:

### 1. Vragenformulier (8 stappen)
Stap-voor-stap met optieknoppen (geen formuliervelden). Alles werkt met ranges, geen exacte bedragen:

1. **Leeftijd** — 4 ranges (25-34, 35-44, 45-54, 55-65)
2. **Gezinssituatie** — alleenstaand / samenwonend / gezin / alleenstaand met kinderen
3. **Bruto jaarinkomen** — 5 ranges (< €35k tot > €120k)
4. **Woning** — koop of huur
5. **Hypotheek/huur** — dynamisch: toont hypotheekranges bij koop, huurranges bij huur
6. **Spaargeld & beleggingen** — 5 ranges (< €10k tot > €200k)
7. **Pensioenopbouw** — ja / beperkt / nee / onbekend
8. **Financieel doel** — eerder stoppen / huis kopen / zekerheid / vermogen opbouwen / inzicht

### 2. Laadscherm
Geanimeerde stappen (cashflow, pensioen, buffer, risico's, rapport) met checkmarks. Duurt ~3,2 seconden.

### 3. Dashboard
- **Scoresring** — 0-100, geanimeerd, kleur groen/oranje/rood
- **4 indicatoren** — inkomen vs. uitgaven, buffer, pensioen, vermogensgroei
- **Vergelijkingsbalk** — "U scoort beter dan X% van vergelijkbare huishoudens"
- **Persoonlijke inzichten** — gekleurde kaarten (groen/oranje/rood) met specifieke bedragen en situatiebeschrijvingen
- **3 concrete acties** — genummerd, geprioriteerd
- **Scenario's** — "wat als" knoppen (4 dagen werken, beleggen, eerder stoppen, extra lenen/huis kopen)

### 4. CTA
Rustige gradient-banner met "Plan een vrijblijvend gesprek" knop.

### 5. Disclaimer
Korte tekst dat het een indicatie is, geen financieel advies.

## Rekenmodel (JavaScript)

Het rekenmodel draait volledig client-side en bevat modules voor:

- **Netto inkomen** — vereenvoudigd NL belastingmodel (3 schijven)
- **Uitgaven** — basisbedrag × gezinsfactor + woonlasten
- **Buffer** — vermogen / maandelijkse uitgaven
- **Pensioen** — percentage van huidig inkomen op basis van opbouwstatus
- **Vermogensontwikkeling** — spaarpotentieel + 4% groei
- **Box 3** — vrijstellingsgrens + 2% heffing
- **Risico's** — nabestaanden (hypotheek + gezin) en arbeidsongeschiktheid
- **Huis kopen** — maximale hypotheek (4,25× inkomen), kosten koper (5%), maandlastvergelijking
- **Scoring** — samengestelde score (0-100) op basis van alle modules

## Ontwerpkeuzes

### Kleuren (CSS variabelen)
- **Primair blauw:** `#3b82f6` (knoppen, voortgang, accenten)
- **Donkerblauw:** `#1e40af` (CTA gradient)
- **Groen:** `#22c55e` (positieve indicatoren)
- **Oranje:** `#f59e0b` (waarschuwingen)
- **Rood:** `#ef4444` (negatieve indicatoren)
- **Achtergrond:** `#f9fafb` (lichtgrijs)
- **Kaarten:** `#ffffff` met subtiele schaduwen
- Elke statuskeur heeft een bijbehorende lichte achtergrondkleur voor insight-kaarten

### Typografie
- Systeemfonts: `-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif`
- Geen externe fonts geladen (snelheid)

### Layout
- Max-width: `640px` — mobiel-first, gecentreerd
- Border-radius: `12px` op kaarten
- Geen "Excel vibe" — rustig, veel witruimte, visueel clean
- Stap-voor-stap navigatie met voortgangsbalk (geen lang formulier)

### UX-principes
- Alles in ranges, geen exacte bedragen
- Geen vaktaal
- Resultaat voelt persoonlijk (specifieke bedragen, niet generiek)
- CTA is subtiel, niet agressief
- Scenario-knoppen maken het "verslavend" — gebruikers willen doorrekenen

## Deployment

GitHub Actions workflow (`.github/workflows/deploy.yml`) deployt automatisch naar GitHub Pages bij elke push naar `main`. Gebruikt `actions/deploy-pages@v4`.

## Taal

Alles is Nederlandstalig — interface, berekeningen, inzichten, acties, disclaimer.
