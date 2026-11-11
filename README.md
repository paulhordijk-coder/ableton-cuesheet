# Timeline AbletonCueSheet

**Timeline AbletonCueSheet** is een professionele Ableton Live extensie gebouwd met de `@ableton-extensions/sdk`, ontworpen om direct vanuit je Ableton Live arrangement kant-en-klare cue sheets (`.cue` / `.txt`) te genereren voor mixtapes, podcasts en livesets.

---

## 📸 Interface Preview

![Timeline AbletonCueSheet Interface](screenshot.png)

---

## 🤖 AI Project Samenvatting & Oorsprong

Dit project is ontwikkeld door **Antigravity** (Google DeepMind) in samenwerking met de gebruiker.

### Wat Timeline AbletonCueSheet oplost:
Voorheen moesten DJ's en producers handmatig door hun arrangement navigeren om per overgang de precieze tijdcode (minuten, seconden, frames) op te schrijven voor een tracklist of CUE-bestand.

**Timeline AbletonCueSheet**:
1. Wordt direct geopend via het Ableton Live contextmenu op clips of tracks (**"Timeline AbletonCueSheet..."**).
2. Analyseert automatisch alle audio- en MIDI-clips uit het actieve arrangement.
3. Filtert met slimme drempelwaarden korte risers, sweeps, fills en percussie-samples weg.
4. Voegt aaneengesloten clips op hetzelfde spoor automatisch samen.
5. Biedt een overzichtelijke pop-up dialoog waarin alle tracks direct geïnspecteerd en bewerkt kunnen worden.
6. Genereert de volledige CUE sheet met één klik op het bureaublad of kopieert deze direct naar het klembord.

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

## 🏗️ Architectuur & Dataflow (Voor Developers & AI Agents)

De extensie werkt als een hybride Node.js / Webview applicatie via de `@ableton-extensions/sdk`:

```
┌────────────────────────────────────────────────────────────────────────┐
│ Ableton Live 12 (Arrangement View)                                     │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ 1. context.application.song
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ src/ableton-cuesheet/extension.ts (Node.js Extension Host runtime)     │
│ - Verzamelt song.tempo en alle song.tracks.arrangementClips            │
│ - Berekent bestandsnamen via AudioClip.filePath                        │
│ - Injecteert JSON data inline via <script>const projectData = ...      │
│ - Roept context.ui.showModalDialog(dataUrl, 680, 720) aan              │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ 2. Data URL Modal Dialog
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ src/ableton-cuesheet/ui/interface.html (Webview UI)                    │
│ - Vormgegeven met @timeline-studio/design-system                       │
│ - Filtert samples/risers op drempelwaarde                              │
│ - Voegt aaneengesloten clips op hetzelfde spoor samen                  │
│ - Zet beats om naar MM:SS:FF timecodes op basis van projecttempo       │
│ - Retourneert JSON via window.close(JSON.stringify(result))            │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ 3. Promise resolve in extension.ts
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ extension.ts -> Schrijft bestand direct naar Desktop van de gebruiker  │
└────────────────────────────────────────────────────────────────────────┘
```

### Belangrijke bestanden in deze repository:
- `manifest.json`: Definieert de extensienaam (`ableton-cuesheet`), entry point (`dist/extension.js`), en API-versie.
- `build.ts`: Esbuild script. Let op: `interface.html` wordt via de esbuild `text` loader als een inline string gebundeld in `dist/extension.js`.
- `vendor/`: Bevat de lokale `.tgz` archieven (`ableton-extensions-sdk` en `ableton-extensions-cli`). Hierdoor werkt `npm install` direct zonder afhankelijk te zijn van externe/gesloten Ableton NPM accounts.
- `screenshot.png`: Exact gerenderde weergave (680×720) van de modale dialoog.

---

## 🚀 Installatie & Ontwikkeling

### Vereisten
- Node.js (versie 24.14.1 of hoger)
- Ableton Live 12+ (vereist voor live testen met `npm start`, **niet** vereist om de `.ablx` te bouwen!)

### Installatie
```sh
npm install
```

### Het `.ablx` Installatiepakket Bouwen
Om het definitieve `.ablx` pakket voor Ableton Live te genereren:
```sh
npm run package
```
Dit voert automatisch `tsc --noEmit`, de productiebundel via `build.ts`, en `extensions-cli package` uit. Het resultaat is `ableton-cuesheet-1.0.0.ablx` in de hoofdmap.

### Hoe installeer je het `.ablx` bestand in Ableton Live?
- **Methode 1**: Dubbelklik op het gegenereerde `ableton-cuesheet-1.0.0.ablx` bestand. Ableton Live 12 opent en installeert de extensie automatisch.
- **Methode 2**: Sleep het bestand direct in het geopende Ableton Live venster.
- Na installatie verschijnt **"Timeline AbletonCueSheet..."** direct in het contextmenu wanneer je met de rechtermuisknop op een audioclip, MIDI-clip of track klikt.

### Lokale Ontwikkeling & Testen
1. Kopieer `.env.example` naar `.env`:
   ```sh
   cp .env.example .env
   ```
2. Zorg dat `EXTENSION_HOST_PATH` in `.env` verwijst naar je lokale `Ableton Live 12 Suite.exe`.
3. Start de dev-server:
   ```sh
   npm start
   ```

### Overzicht van npm scripts
- `npm run build`: Bouwt de productiebundel naar `dist/extension.js`.
- `npm run build:dev`: Bouwt de ontwikkelversie inclusief source maps.
- `npm run package`: Bouwt de productiebundel en genereert het `.ablx` pakket.
- `npm start`: Compileert en start de extensie direct in Live's Extension Host.

---

## 📄 Licentie
MIT &bull; Ontwikkeld voor de muzikale community.
