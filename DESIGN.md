# Timeline Studio Design & Style Specification

This document defines the interface standards, design tokens, and styling guidelines for **Timeline AbletonCueSheet**, following the official [Timeline Studio Design System](https://github.com/paulhordijk-coder/design-system).

---

## 🎨 Design Philosophy

The user interface of Timeline AbletonCueSheet is tailored for audio producers, DJs, and studio engineers:
- **Calm & Professional**: Minimal visual distractions, calm light backgrounds, and neutral surfaces so focus remains on waveforms and arrangement data.
- **Clear Hierarchy**: High contrast between primary text (Slate 900) and secondary labels (Slate 600/400).
- **Functional Accents**: Cobalt blue for interactive elements, focus states, and primary actions; conservative use of signal colors.

---

## 🏷️ Brand Identity & Header

In accordance with the Timeline Studio product line, the header must follow this exact structure:

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

      <!-- Title: Always TIMELINE in Slate 900 + ABLETONCUESHEET in Cobalt Blue -->
      <div class="timeline-nav-title">
        <span class="brand-prefix">TIMELINE</span><span class="brand-product">ABLETONCUESHEET</span>
      </div>

      <!-- Version Badge -->
      <span class="timeline-nav-version">v1.0.0</span>
    </div>
  </div>
</header>
```

---

## 📐 Dimensions & Window Layout

- **Modal Window**: 680px width × 720px height (launched via `context.ui.showModalDialog(url, 680, 720)`).
- **Header Height**: 64px (`--timeline-header-h`).
- **Body**: Flexbox column layout with `overflow: hidden` and custom internal scroll containers.
- **Scrollbars**: Clean rounded 7px scrollbars (`::-webkit-scrollbar`).

---

## 🎨 Color Palette & Design Tokens

| Token | Value | Purpose |
|---|---|---|
| `--timeline-primary-500` | `#2563eb` | Cobalt Blue (accents, focus rings, active tabs) |
| `--timeline-primary-600` | `#1d4ed8` | Primary button hover state |
| `--timeline-primary-50` | `#eff6ff` | Light blue tint for badges & highlighted tabs |
| `--timeline-bg-base` | `#f8fafc` | Application background (Slate 50) |
| `--timeline-bg-surface` | `#ffffff` | Pure white cards, modal panels, and tables |
| `--timeline-bg-subtle` | `#f1f5f9` | Toolbar background, step tab container, subtle lanes |
| `--timeline-border-default` | `#e2e8f0` | Subtle neutral borders |
| `--timeline-text-primary` | `#0f172a` | Primary text (Slate 900) |
| `--timeline-text-secondary` | `#475569` | Secondary labels and helper text (Slate 600) |
| `--timeline-text-muted` | `#94a3b8` | Placeholders and subtle hints (Slate 400) |
| `--timeline-meter-safe` | `#16a34a` | Normal level / active green |

---

## 🔤 Typography

- **Body & Controls**: `'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif`
- **Headings & Branding**: `'Plus Jakarta Sans', -apple-system, BlinkMacSystemFont, sans-serif` (800 weight)
- **Timecodes & CUE syntax**: `'JetBrains Mono', 'Fira Code', 'SF Mono', Consolas, monospace` with `font-variant-numeric: tabular-nums` to ensure steady, non-jittering numeric display.

---

## 🎛️ UI Components

1. **Step Navigation (`.timeline-tabs`)**:
   - Tab 1: Settings
   - Tab 2: Track Preview
2. **Form Inputs (`.timeline-input`, `.timeline-select`)**:
   - Clean white background, 1px Slate 200 border, cobalt blue outline on `:focus`.
3. **Buttons (`.timeline-btn`)**:
   - `.timeline-btn-primary`: Primary actions ("Next", "Save to Desktop")
   - `.timeline-btn-secondary`: Cancel / Back navigation
   - `.timeline-btn-surface`: Secondary neutral actions ("Copy to Clipboard")
4. **Interactive Track Table (`.timeline-table`)**:
   - Sticky table header, editable inline inputs per track, and monospace timecode tags.
5. **Toast Notifications (`.timeline-toast`)**:
   - Smooth animated confirmation upon clipboard copy.
