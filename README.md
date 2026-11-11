# AbletonCueSheet

**AbletonCueSheet** is een professionele Ableton Live extensie gebouwd met de `@ableton-extensions/sdk`, ontworpen om direct vanuit je Ableton Live arrangement kant-en-klare cue sheets (`.cue` / `.txt`) te genereren voor mixtapes, podcasts en livesets.

De interface volgt de rustige, zakelijke huisstijl van het [Timeline Studio Design System](https://github.com/paulhordijk-coder/design-system).

---

## 🤖 AI Project Samenvatting & Oorsprong

Dit project is ontwikkeld door **Antigravity** (Google DeepMind) in samenwerking met de gebruiker.

### Wat AbletonCueSheet oplost:
Voorheen moesten DJ's en producers handmatig door hun arrangement navigeren om per overgang de precieze tijdcode (minuten, seconden, frames) op te schrijven voor een tracklist of CUE-bestand.

**AbletonCueSheet**:
1. Wordt direct geopend via het Ableton Live contextmenu op clips of tracks (**"AbletonCueSheet..."**).
2. Analyseert automatisch alle audio- en MIDI-clips uit het actieve arrangement.
3. Filtert met slimme drempelwaarden korte risers, sweeps, fills en percussie-samples weg.
4. Voegt aaneengesloten clips op hetzelfde spoor automatisch samen.
5. Biedt een overzichtelijke pop-up dialoog conform de Timeline Studio huisstijl (lichte achtergronden, minimale kleurafleiding, clean typografie en haarscherpe bedieningselementen).
6. Genereert de volledige CUE sheet met één klik op het bureaublad of kopieert deze direct naar het klembord.

---

## 🎨 Huisstijl & Design Tokens

De gebruikersinterface van **AbletonCueSheet** implementeert het officiële [Timeline Studio Design System](https://github.com/paulhordijk-coder/design-system):

- **Achtergronden**: Rustige en zakelijke lichte achtergrond (`--timeline-bg-base: #f8fafc;`) met helderwitte paneelvlakken (`--timeline-bg-surface: #ffffff;`).
- **Accentkleur**: Timeline Cobalt Blue (`--timeline-primary-500: #2563eb;`) voor actieve elementen, tabs en primaire actieknoppen.
- **Typografie**: Inter voor interface-elementen, Plus Jakarta Sans voor titels, en JetBrains Mono met `tabular-nums` voor stabiele SMPTE timecodes.
- **Header**: Uniforme Timeline Studio applicatiebalk inclusief officieel logo-mark, merknaam (`AbletonCueSheet`), versie-indicatie (`v1.0.0`) en realtime Live verbindingsstatus.

---

## 🎛️ Opties & Functionaliteit

### Scherm 1: Instellingen
1. **Mixtape Audio Bestandsnaam**: De naam van de geëxporteerde audio-mix (bijv. `mixtape.wav`) die in het cue sheet wordt gekoppeld via de `FILE`-instructie.
2. **Uitvoer Cue Sheet Bestandsnaam**: Het tekstbestand dat op het bureaublad wordt opgeslagen (standaard gesynchroniseerd met de audio-naam).
3. **Track Filter Drempelwaarde**: Clips korter dan deze waarde (bijv. `1:30` of `90` seconden) worden automatisch gefilterd zodat overgangseffecten geen overbodige tracks aanmaken.
4. **Overgangspositie (Cue Index Point)**:
   - *Start van overgang / overlap*: De tracktijd triggert direct wanneer het inkomende nummer begint te spelen.
   - *Einde van overgang / overlap*: De tracktijd triggert zodra het uitgaande nummer volledig is afgelopen.
5. **Aaneengesloten clips samenvoegen**: Voegt aansluitende clips op hetzelfde spoor samen tot één logisch muzieksegment voordat de tijdsdrempel wordt getoetst.

### Scherm 2: Track Overzicht
- **Interactieve Track-tabel**: Directe voorvertoning met bewerkbare songtitels en artiestnamen.
- **Live CUE Code Voorvertoning**: Realtime weergave van de gestructureerde CUE syntax.
- **Kopieer naar Klembord**: Kopieert de inhoud direct naar het klembord met toast-bevestiging.
- **Opslaan op Bureaublad**: Exporteert het `.txt` cue sheet bestand direct naar het bureaublad.

---

## 🚀 Installatie & Ontwikkeling

### Vereisten
- Ableton Live 12+ (met Extension Host ondersteuning)
- Node.js (versie 24.14.1 of hoger)

### Installatie
```sh
npm install
```

### Scripts
- `npm run build`: Bouwt de productiebundel naar `dist/extension.js`.
- `npm run build:dev`: Bouwt de ontwikkelversie inclusief source maps.
- `npm start`: Compileert in dev-modus en start de Ableton Extension Host.
- `npm run package`: Bouwt de extensie en verpakt deze in een `.ablx` bestand (`ableton-cuesheet-1.0.0.ablx`).

---

## 📄 Licentie
MIT &bull; Ontwikkeld voor de muzikale community.
