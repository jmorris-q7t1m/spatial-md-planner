# Semantic Page Planner
<p align="center">
  <img src="https://github.com/user-attachments/assets/65aeed98-30f3-4f7c-b44a-85ae5274bae7" alt="3D Spatial Constellation" width="48%" />
  <img src="https://github.com/user-attachments/assets/a2b58b31-0505-4eae-b46c-c4573bde61a0" alt="3D Spatial Planner" width="48%" />
</p>


A zero-backend, single-file **3D spatial Markdown editor and semantic dependency planner**. Each document section is rendered as a live, scrollable HTML/KaTeX card floating in Three.js (`WebGLRenderer` + `CSS3DRenderer`) space, connected in real time by 3-axis semantic beams.

Built around **SDS_Parser** (`v1.8.2`), it runs offline directly from a local `index.html` file while supporting direct folder sync (`pages/*.json`) and lossless Markdown round-tripping.

## Features

- **Scrollable 3D Document Cards:** Renders full Markdown, KaTeX math (`$...$` and `$$...$$`), currency-protected numbers (`$1,500`), tables, blockquotes, and fenced code blocks inside interactive 3D cards.
- **3-Axis Semantic Web:** Automatically analyzes section text and draws color-coded 3D Bezier connections:
  - **White (X-Axis):** Explicit `Section N` cross-references.
  - **Cyan (Y-Axis):** Shared formulas, frequencies, latencies, and metric patterns.
  - **Gold (Z-Axis):** Shared domain concepts and technical terminology.
  - **Red Alert:** Numeric threshold drift warnings when two linked sections cite conflicting percentages.
  - **Purple (External Layer):** Optional precomputed links (e.g., from an external Python NLP, embedding, or rough-set pass).
- **Per-Page JSON & Local Folder Sync:** Uses the File System Access API (`Bind Local Folder`) to read and write individual `page_XX.json` files and `semantic_index.json` straight to disk alongside `localStorage` persistence.
- **Lossless Markdown Round-Tripping:** Exports a unified `.md` file (`Compile & Download .md`) with embedded `<!-- page-meta: {...} -->` HTML comments so 3D coordinates, pin states, and revision numbers survive re-imports or external script passes.

## Quick Start

1. Clone or download this repository.
2. Open `index.html` directly in any modern browser (Chrome, Edge, Brave, Firefox, or Safari).
   - *Note:* Direct local folder sync (`Bind Local Folder`) uses the File System Access API and requires a Chromium-based browser; `localStorage`, `.json` download/import, and `.md` compilation work in all browsers.

## Controls

<p align="center">
  <img src="https://github.com/user-attachments/assets/0362c03d-778c-4cae-84db-bc753a90570a" alt="3D Spatial Constellation with HUD" width="48%" />
  <img src="https://github.com/user-attachments/assets/a10fbdc7-05d1-488b-a57c-6ab2b0ef1f3c" alt="3D Spatial Planner with HUD" width="48%" />
</p>

| Action | Control |
|---|---|
| **Orbit Camera** | Left-click + drag empty space |
| **Pan Camera** | Right-click + drag empty space |
| **Zoom** | Scroll wheel on empty space |
| **Scroll Card Content** | Hover over any card body + scroll wheel |
| **Focus / Fly to Card** | Click a card's header bar |
| **Reposition Card (XY)** | `Shift` + drag a card's header bar |
| **Adjust Card Depth (Z)** | Click `-Z` or `+Z` on the card header |
| **Edit / Save Markdown** | Click `Edit` on a card header, modify text, and click `Save` |
| **Insert / Delete Section** | Click `+Sec` on a header to insert after, or `Del` to remove |
| **Toggle Controls Drawer** | Click `◀` / `▶` on the top-left HUD tab |

## Customizing Semantic Rules

Open `index.html` and edit the `USER CONFIG` section inside the `<script type="module">` block to tailor the lightweight client-side analyzer to your own domain:

```javascript
const AXIS_2_PATTERNS = {
  "latex_math": /\$[^$\s][^$]*\$/,
  "frequency_hz": /\b\d+\s*Hz\b/i,
  "latency_ms": /\b\d+\s*ms\b/i,
  "threshold_pct": /\b(\d{2})%\b/
};

const AXIS_3_TERMS = [
  "Architecture", "Pipeline", "Schema", "Interface", "Module",
  "Protocol", "Engine", "Runtime", "Storage", "Graph"
];
```
For heavier offline analysis (such as TF-IDF, vector embeddings, or Tolerance Rough Set approximations), populate the SEEDED_PAGES and SEEDED_ROUGH_LINKS arrays from an external Python script before opening index.html.

## License
Licensed under the Apache License, Version 2.0.
