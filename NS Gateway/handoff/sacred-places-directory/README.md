# Sacred Places Directory — developer handoff

Open `index.html` in a browser. Everything it needs is in this folder except three CDN scripts (listed below), which require network access.

## Contents
- `index.html` — the page (identical to "Review_Sacred Places Directory.dc.html")
- `support.js` — runtime that renders the page template
- `assets/` — every image the page references (20 files)

## External dependencies (CDN)
| Library | Version | Purpose |
|---|---|---|
| Leaflet | 1.9.4 (`unpkg.com/leaflet@1.9.4`) | the map — JS + `leaflet.css` |
| topojson-client | 3.1.0 | decodes the US states topology for state shading |
| us-atlas states-10m | via unpkg | state boundary geometry |
| Google Fonts | — | Nunito, Lora, Caveat |

Basemap tiles: `https://tile.openstreetmap.org/{z}/{x}/{y}.png` (keyless). Attribution "© OpenStreetMap contributors" is required and already wired up. **For production, move to a paid or self-hosted tile provider** — OSM's public tile server is not licensed for production traffic. A warm, low-saturation Voyager- or Positron-style basemap matches the brand best.

---

## Map marker specification

There are two marker types. Which one shows depends on zoom and filter state:

| Zoom | Filters active? | Shown |
|---|---|---|
| ≤ 5 | no | **State count bubbles** + pale-leaf state shading + legend |
| 6 | no | **Metro count bubbles** |
| ≥ 7 | no | **Individual bench pins** |
| any | yes | **Individual bench pins** (always) |

### 1. Bench pin (individual Sacred Place)

A cream speech-bubble card with the Nature Sacred bench glyph inside and a downward tail pointing at the coordinate.

**Geometry** — drawn on a `54 × 54` viewBox:
- Card: rounded rect, `x=2 y=2 w=50 h=39`, corner radius `12`
- Tail: triangle from `(27,53)` up to `(20,40)` and `(34,40)`, stroked to match the card edge
- Bench glyph: `assets/bench-icon-sm.png` placed at `x=12 y=9`, `30 × 26`, centered
- Anchor point: bottom center (`iconAnchor: [w/2, h-1]`) — the tail tip sits on the coordinate
- Tooltip anchor: `[0, -h + 12]`

**States**

| | Rest | Active / hovered |
|---|---|---|
| Scale | 0.84 (≈45 × 45px) | 1.0 (54 × 54px) |
| Fill | `#fdfbf6` paper | `#57a143` forest |
| Stroke | `#57a143` forest | `#46852f` deep forest |
| Stroke width | 1.8 | 2.6 |
| Bench glyph | full color | knocked out to white (`brightness(0) invert(1)`, opacity 0.94) |
| Shadow | `0 3px 8px rgba(31,26,20,0.22)` | `0 5px 12px rgba(31,26,20,0.32)` |

The active pin is set to a higher `zIndexOffset` so it renders above its neighbors. Hovering a card in the list activates its pin, and vice versa — the two are bound in both directions.

### 2. Count bubble (state / metro cluster)

A circular cream chip with the number of Sacred Places in that state or metro.

- Diameter: `34px`, or `40px` when count ≥ 10
- Font: Nunito 700, `13px` (or `15px` at 40px diameter)
- Rest: background `#fdfbf6`, border `1.5px solid rgba(87,161,67,0.7)`, text `#1f1a14`
- Active/hover: background `#57a143`, text `#fdfbf6`
- Shadow: `0 2px 6px rgba(31,26,20,0.12)`
- Anchor: dead center (`iconAnchor: [d/2, d/2]`)
- Tooltip: "N Sacred Places · {label}", direction top, offset `[0, -26]`
- Click: zooms to `6` (state bubble) or `9` (metro bubble)

### 3. State shading (national view only)

Pale-leaf fill on states that contain Sacred Places, drawn beneath the markers. Removed above zoom 5, and the legend fades with it.

| Count | Fill | Stroke |
|---|---|---|
| 1–4 | `rgba(175,210,116,0.42)` | `rgba(87,161,67,0.5)` |
| 5–9 | `rgba(150,196,61,0.62)` | `rgba(87,161,67,0.6)` |
| 10+ | `rgba(87,161,67,0.7)` | `rgba(87,161,67,0.75)` |

---

## Layout notes
- Map and list columns are locked to the same height — `min(calc(100vh - 196px), 46vw)`, floor 420px, ceiling 720px — so the section ends on one line. The list scrolls internally.
- Below **1180px** the two columns stack; the list returns to natural height (no nested scroll).
- Below **620px** the map drops to 340px, the legend scales to 82%, and the default view opens one zoom step out so the whole country fits.
- On resize the map calls `invalidateSize()` and refits (debounced 180ms).

## Data
The place records live in the `PLACES` array near the top of the script block: `id, name, where, state, region, setting, feature, lat, lng, img, href`. Filters read from `region`, `setting`, and `feature`. Deep links work off `#{id}` in the URL — the map opens to zoom 12 on that place.

## Type & color
Nunito (400/600/700/800) for everything structural; Lora italic for journal entries; Caveat used sparingly.

Ink `#1f1a14` · Body `#3a3128` · Muted `#6b5e51` / `#9d877a` · Paper `#fdfbf6` · Soft cream `#f5f1e8` · Borders `#e7e0d2` / `#c2b6a4`
Leaf `#96c43d` · Forest `#57a143` · Pale leaf `#afd274` · Deep wood `#77441d` · Journal yellow `#f5d06a` · Coral `#ff4800`

## Known caveats
- Nav links (Homepage, Donate, The Network, Our Design Process) point at sibling pages not included here; they 404 in isolation.
- Images in `assets/opt/` are web-compressed. Originals are available on request.
