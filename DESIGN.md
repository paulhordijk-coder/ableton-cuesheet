# Timeline Studio Design & Huisstijl Specificatie

Dit document legt de interface-standaarden, design tokens en stylingrichtlijnen vast voor **Timeline AbletonCueSheet**, conform het officiële [Timeline Studio Design System](https://github.com/paulhordijk-coder/design-system).

---

## 🎨 Design Filosofie

De gebruikersinterface van Timeline AbletonCueSheet is ontworpen voor professionele audio- en studiogebruikers:
- **Rustig en zakelijk**: Minimale visuele afleiding, lichte achtergronden en neutrale panelen zodat de focus op de muziek- en arrangementdata blijft liggen.
- **Duidelijke hiërarchie**: Hoge contrasten tussen tekst (Slate 900) en secundaire labels (Slate 600/400).
- **Functionele kleuraccenten**: Cobalt blauw voor interactieve elementen en focus, terughoudend gebruik van signaalkleuren.

---

## 🏷️ Merkidentiteit & Header

In overeenstemming met de Timeline Studio productlijn geldt de volgende header-opbouw:

```html
<header class="timeline-header">
  <div class="timeline-header-inner">
    <div class="timeline-nav-logo">
      <!-- Timeline Studio Logo Mark SVG -->
      <svg class="timeline-nav-logo-img" viewBox="0 0 100 100" fill="none">
        <rect width="100" height="100" rx="20" fill="#2563eb" />
        <rect x="20" y="28" width="34" height="11" rx="4" fill="#ffffff" fill-opacity="0.9" />
        <rect x="58" y="28" width="22" height="11" rx="4" fill="#ffffff" fill-opacity="0.5" />
        <rect x="20" y="44" width="22" height="11" rx="4" fill="#ffffff" fill-opacity="0.5" />
        <rect x="46" y="44" width="34" height="11" rx="4" fill="#ffffff" fill-opacity="0.9" />
        <rect x="20" y="60" width="40" height="11" rx="4" fill="#ffffff" fill-opacity="0.9" />
        <polygon points="41,17 48,25 34,25" fill="#ffffff" />
        <line x1="41" y1="23" x2="41" y2="76" stroke="#ffffff" stroke-width="3.5" stroke-linecap="round" />
      </svg>

      <!-- Titel: Altijd TIMELINE in Slate 900 + ABLETONCUESHEET in Cobalt Blauw -->
      <div class="timeline-nav-title">
        <span class="brand-prefix">TIMELINE</span><span class="brand-product">ABLETONCUESHEET</span>
      </div>

      <!-- Versie Badge -->
      <span class="timeline-nav-version">v1.0.0</span>
    </div>
  </div>
</header>
```

---

## 📐 Afmetingen & Vensterlayout

- **Modal venster**: 680px breed × 720px hoog (geopend via `context.ui.showModalDialog(url, 680, 720)`).
- **Headerhoogte**: 64px (`--timeline-header-h`).
- **Body**: Flexbox kolomlayout met `overflow: hidden` en interne scrollcontainers.
- **Scrollbars**: Subtiele afgeronde 7px schuifbalken (`::-webkit-scrollbar`).

---

## 🎨 Kleurenpalet & Design Tokens

| Token | Waarde | Doel |
|---|---|---|
| `--timeline-primary-500` | `#2563eb` | Zakelijk Cobalt Blauw (accent, focus, actieve tabs) |
| `--timeline-primary-600` | `#1d4ed8` | Primaire knoppen hover-state |
| `--timeline-primary-50` | `#eff6ff` | Zachte blauwe achtergrond voor badges & highlight tabs |
| `--timeline-bg-base` | `#f8fafc` | Achtergrond van het venster (Slate 50) |
| `--timeline-bg-surface` | `#ffffff` | Witte panelen, vensters en modal cards |
| `--timeline-bg-subtle` | `#f1f5f9` | Toolbar achtergrond, tab container, subtiele vlakken |
| `--timeline-border-default` | `#e2e8f0` | Subtiele neutrale randen |
| `--timeline-text-primary` | `#0f172a` | Primaire tekst (Slate 900) |
| `--timeline-text-secondary` | `#475569` | Secundaire toelichtingen en sublabels (Slate 600) |
| `--timeline-text-muted` | `#94a3b8` | Placeholders en subtiele hints (Slate 400) |
| `--timeline-meter-safe` | `#16a34a` | Statusindicator actief / Live connected groen |

---

## 🔤 Typografie

- **Body & Controls**: `'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif`
- **Titels & Branding**: `'Plus Jakarta Sans', -apple-system, BlinkMacSystemFont, sans-serif` (800 gewicht voor logo/titel)
- **Timecodes & CUE syntax**: `'JetBrains Mono', 'Fira Code', 'SF Mono', Consolas, monospace` met `font-variant-numeric: tabular-nums` voor stabiele cijfers zonder verspringing.

---

## 🎛️ Componenten in deze extensie

1. **Stappen Navigatie (`.timeline-tabs`)**:
   - Tab 1: Instellingen
   - Tab 2: Track Overzicht
2. **Formulierinvoer (`.timeline-input`, `.timeline-select`)**:
   - Witte achtergrond met 1px Slate 200 border, actieve blauwe ring bij `:focus`.
3. **Knoppen (`.timeline-btn`)**:
   - `.timeline-btn-primary`: Primaire acties ("Volgende", "Opslaan op bureaublad")
   - `.timeline-btn-secondary`: Annuleren / Terug acties
   - `.timeline-btn-surface`: Neutrale acties ("Kopieer naar klembord")
4. **Interactieve Track-tabel (`.timeline-table`)**:
   - Vaste header met sticky positioning, interactieve bewerkbare input-velden per track en monospace timecode badges.
5. **Toast Bevestigingen (`.timeline-toast`)**:
   - Vloeiende feedback bij acties zoals klembord-kopieën.
