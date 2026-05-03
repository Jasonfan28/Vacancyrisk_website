# Philly Stat 360 Design System

## Overview

**Philly Stat 360** is the City of Philadelphia's performance management and open data dashboard initiative. It gives Philadelphia residents transparent, accessible views into how city government is performing across departments — public safety, parks, licenses, permits, sanitation, and more.

The product family lives at:
- **Public dashboard:** https://philly-stat-360.phila.gov
- **ArcGIS Hub:** https://philly-stat-360-phl.hub.arcgis.com
- **City standards:** https://standards.phila.gov

This design system enforces the **City of Philadelphia Digital Standards** — a government property where accessibility (WCAG AA) is non-negotiable.

---

## Sources Provided

| Source | Path / Link |
|---|---|
| City of Philadelphia logo variants | `assets/logo-*.png` |
| Montserrat font family (full weight range) | `fonts/Montserrat-*.ttf` |
| City Digital Standards | https://standards.phila.gov |
| Live dashboard (reference) | https://philly-stat-360.phila.gov |
| ArcGIS Hub (reference) | https://philly-stat-360-phl.hub.arcgis.com |

> No Figma links or codebase import was provided. The design system is derived from the City of Philadelphia Digital Standards specification and the live reference sites.

---

## Products / Surfaces

| Surface | Description |
|---|---|
| **Public Performance Dashboard** | Data-heavy web app showing KPIs by department. Residents track on-time rates, complaint resolution, permit timelines, etc. |
| **ArcGIS Hub Portal** | Map-centric view of city data; uses same brand but ArcGIS-specific layout constraints apply. |
| **phila.gov** (parent) | The City's main CMS site. Philly Stat inherits its design language from here. |

---

## CONTENT FUNDAMENTALS

**Voice:** Plainspoken, civic, trustworthy. For Philadelphia residents — not data scientists or government insiders.

**Reading level:** Target 8th grade. Short sentences. Active voice. No jargon.

**Tagline direction:** *"Giving Philadelphians a government they can see, feel, and touch."*

**Casing rules:**
- Sentence case everywhere — headings, nav labels, body copy
- Buttons may use ALL CAPS with letter-spacing 0.4px (acceptable, not required)
- Never ALL CAPS for body copy or headings
- Never italics for emphasis — use font-weight 600 instead

**Numbers always include context:**
- ✅ "87% on-time" not "87%"
- ✅ "$2.4M invested" not "2400000"
- ✅ Dates: "October 20, 2025" in prose; "10/20/25" in tables

**Banned words:** leverage, synergy, stakeholder, drill down, utilize

**Emoji:** Never in UI copy. Acceptable only in data or chart labels if genuinely useful.

**Tone examples:**
- ✅ "Philadelphia collected 94% of trash on schedule last month."
- ✅ "311 calls answered within 5 business days"
- ❌ "Leveraging data-driven insights to synergize resident stakeholder engagement"

---

## VISUAL FOUNDATIONS

### Colors
- Blues do 70% of the work. Dark Ben Franklin Blue (`#0f4d90`) anchors headings and heroes.
- Bell Yellow (`#f3c613`) is the single accent — one CTA per page, left-border callouts, chart highlights. **Never on white text (fails WCAG).**
- Semantic colors: orange=warning, red=error/decline, green=success/positive
- Flat design — no gradients anywhere, ever.

### Typography
- **Headings:** Montserrat 700, sentence case, slight tight tracking (-0.3px on h1/h2)
- **Body:** Open Sans 400, line-height 1.5–1.6 (loaded from Google Fonts)
- **Scale:** h1 40px → h2 28px → h3 20px → h4 16px → body 16px → small 13–14px
- **Heading color:** `#0f4d90` by default; body `#444`

### Spacing & Layout
- 12/24-column grid, Foundation-style (City's framework)
- Max content width: 1200px centered
- Gutters: 24–32px desktop, 16px mobile
- Section padding: 48–80px vertical desktop
- Generous whitespace — "if it looks empty, it's probably right"

### Backgrounds & Surfaces
- White is default. `#f0f0f0` (ghost-gray) for surface fills.
- `#0f4d90` hero backgrounds with white text
- No photography overlaid with text unless a solid color scrim is present
- No gradients, no textures, no patterns

### Cards
- White bg, 1px `#cfcfcf` border, border-radius 4–8px, padding 20–24px
- No drop shadows — borders only (civic, not SaaS)
- Clickable cards: border shifts to `#2176d2` on hover

### Callouts (Philly Signature Pattern)
- 4px left border in `#f3c613` (or semantic color)
- `#f0f0f0` background, padding 14px 16px, no other borders

### Animation & Interaction
- No animations or transitions beyond hover color changes
- Hover: darken background ~10%; no scale transforms, no shadow lifts
- No dark mode
- No carousels on homepage

### Corner Radii
- Buttons: 2px
- Cards: 4–8px
- Inputs: 2px
- No pill shapes

### Iconography
See ICONOGRAPHY section below.

### Accessibility
- WCAG AA required for all color combinations (4.5:1 body text, 3:1 large text/UI)
- Yellow (`#f3c613`) text on white **fails** — never use
- Light gray (`#a1a1a1`) on white passes for large text only
- Always use darker text on lighter backgrounds

---

## ICONOGRAPHY

**Icon system:** The City of Philadelphia Digital Standards uses a simple icon approach — no proprietary icon font was provided. The live sites use standard civic/utility icons.

**Recommended CDN substitute:** [Lucide Icons](https://lucide.dev) — clean, stroke-based, 1.5px stroke weight, consistent with the flat civic aesthetic. Load via CDN:
```html
<script src="https://unpkg.com/lucide@latest/dist/umd/lucide.min.js"></script>
```

**Usage rules:**
- Never icon-only buttons — always pair with a visible text label or aria-label
- Icons in body copy: 16×16px, vertically centered, `#444` color
- Icons in nav: 18×18px, `#444`
- External link icon: always append to external link text ("opens in new window")
- No custom-drawn SVG icons — use the CDN set

**Logo assets (in `assets/`):**
| File | Use |
|---|---|
| `logo-standard.png` | Default: yellow bell + dark gray text. Use on white/light backgrounds. |
| `logo-blue-text.png` | Preferred official: yellow bell + Ben Franklin Blue text. White/light bg. |
| `logo-white.png` | White version: use on `#0f4d90` or dark backgrounds. |
| `logo-yellow-white.png` | Yellow bell + white text: use on `#0f4d90` dark backgrounds. |
| `logo-gray.png` | Monochrome: printing, embossing, single-color contexts. |

**Hard don'ts:** Don't redraw the logo in SVG. Don't apply shadows or gradients to it. Don't put it in a white box on dark backgrounds.

---

## File Index

```
README.md                      ← This file
SKILL.md                       ← Agent skill descriptor
colors_and_type.css            ← All CSS custom properties (tokens)

assets/
  logo-standard.png            ← City of Philadelphia logo (standard)
  logo-blue-text.png           ← City of Philadelphia logo (blue text)
  logo-white.png               ← City of Philadelphia logo (all white)
  logo-yellow-white.png        ← City of Philadelphia logo (yellow bell, white text)
  logo-gray.png                ← City of Philadelphia logo (all gray)

fonts/
  Montserrat-*.ttf             ← Full Montserrat family (Thin → Black, Regular + Italic)

preview/
  colors-primary.html          ← Primary blue palette swatches
  colors-accent.html           ← Bell Yellow + semantic colors
  colors-neutrals.html         ← Neutral grayscale palette
  colors-semantic.html         ← Semantic color usage (status, data viz)
  type-headings.html           ← Heading scale specimen
  type-body.html               ← Body + small text specimen
  type-montserrat-weights.html ← Montserrat weight showcase
  spacing-tokens.html          ← Spacing scale tokens
  spacing-radii-borders.html   ← Border radii + border tokens
  components-buttons.html      ← All button variants + states
  components-cards.html        ← Card + callout patterns
  components-forms.html        ← Form input + label + error states
  components-table.html        ← Data table pattern
  components-nav.html          ← Navigation bar pattern
  brand-logos.html             ← Logo usage guide
  brand-hero.html              ← Hero section pattern

ui_kits/
  dashboard/
    README.md                  ← Dashboard UI kit notes
    index.html                 ← Interactive dashboard prototype
    Header.jsx                 ← Top navigation component
    StatCard.jsx               ← KPI stat card component
    DataTable.jsx              ← Sortable data table component
    Callout.jsx                ← Callout/alert component
    Sidebar.jsx                ← Department filter sidebar
```
