# The Complete Shelf

An original, interactive Three.js library of seven clothbound hardcovers. Browse the continuous shelf, pull a volume into a responsive detail view, orbit the binding, and drag through a small set of physically curved pages.

[**View the live experience**](https://mengto.github.io/complete-shelf/) · [**Read the build prompt**](PROMPT.md)

![The Complete Shelf with seven clothbound volumes](assets/complete-shelf-preview.jpg)

The collection is organized around seven tools for modern creative work:

1. Codex
2. Claude Code
3. Cursor
4. Antigravity
5. Figma
6. Framer
7. Xcode

## What is inside

- A continuous seven-volume shelf navigated with the wheel, arrow keys, buttons, or position markers.
- Detailed hardcover construction with separate boards, spine, hinges, endpapers, page block, headbands, bookmark, foil, and contact shadows.
- Responsive inspection mode with orbit, pan, zoom, hover-to-crack-open, click-to-open, and drag-to-turn page interactions.
- Book-specific color systems that recolor the scene and editorial detail layout.
- Procedural cloth, foil, paper, page-edge, wood, roughness, normal, and shadow textures.
- Deterministic shelf-to-detail transitions with exact endpoints so reparenting the selected volume never produces a last-frame jump.
- Accessible HTML controls and status announcements layered over the WebGL scene.
- A **Free Library** page (`library.html`, linked from the top-right of the shelf) with eight complete,
  public-domain novels — real EPUBs and cover art sourced from [Project Gutenberg](https://www.gutenberg.org),
  downloadable with no account required.

## How it is made

The entire experience lives in [`index.html`](index.html): markup, responsive layout, shaders and materials, book geometry, interaction state, animation, and embedded image atlases. There is no framework, bundler, backend, analytics layer, Mint dependency, or MCP call in the browser.

The render stack uses [Three.js](https://threejs.org/) with physically based materials and `OrbitControls`. Cover and wood artwork are stored as embedded WebP atlases; supporting surface detail is generated at runtime with canvas textures. Each book is assembled from reusable geometry, while the front cover and pages use hinged groups and segmented meshes for curved page-turn motion.

Interaction is managed as a small state machine:

```text
shelf -> opening detail -> closed inspection -> open book -> closing -> shelf
```

Camera, book, shelf, and view-offset transforms share deterministic eased timelines. This keeps the animation continuous when a book moves between the shelf and inspection scene graphs.

## Build or remix it with an agent

Start from [`PROMPT.md`](PROMPT.md), attach a visual reference if you have one, and ask your preferred coding agent to work directly in `index.html`.

- [**Codex**](https://openai.com/codex/get-started/) — work in the repository, run the local site, inspect interactions, and iterate against browser proof.
- [**Cursor**](https://www.cursor.com/) — open the folder, give Agent the prompt, and review changes in the editor.
- [**Claude Code**](https://claude.com/product/claude-code) — run Claude in the project directory and point it at the prompt and HTML file.
- [**Aura Build**](https://aura.build) — use the prompt and screenshots as a starting point for a visual build or remix.

Whichever tool you use, the useful loop is the same: make one focused change, run the page, verify the real interaction, inspect the console, and keep only the revision that improves the experience.

## Run locally

The page uses JavaScript modules, so serve it over HTTP instead of opening it directly from disk:

```bash
python3 -m http.server 4173
```

Then visit [http://localhost:4173](http://localhost:4173).

No install or build step is required. An internet connection is needed for the pinned Three.js modules and Inter font.

## Project structure

```text
complete-shelf/
├── index.html          # Complete production experience (the 3D shelf)
├── library.html         # Free Library — real public-domain e-books
├── ebooks/               # Downloaded EPUBs (Project Gutenberg, public domain)
├── assets/
│   ├── complete-shelf-preview.jpg
│   └── covers/           # Downloaded cover art for the Free Library
├── vercel.json           # Static hosting config (headers, clean URLs)
├── PROMPT.md             # Portable recreation and remix brief
└── README.md             # Project overview and implementation notes
```

## Deploy

This is a static site — no build step. On Vercel: import the repo (or run `vercel deploy`
from this folder) with no framework preset selected; `vercel.json` handles headers and
clean URLs. Any other static host (Netlify, GitHub Pages, S3 + CloudFront) works the same way.

## Design notes

The visual direction studies the clarity, material craft, and book photography of contemporary editorial publishers, including [Stripe Press](https://press.stripe.com/), while using original book titles, cover artwork, textures, layouts, and interaction design. This project is independent and is not affiliated with Stripe Press or the products represented by the seven volumes.

## More open source

- **[Skills](https://github.com/MengTo/Skills)** — agent skills for designers and builders using Codex, Claude, Cursor and other AI coding agents. Browse them at [ui-skills.com](https://ui-skills.com).
- **[Sketchbook](https://github.com/MengTo/sketchbook)** — a page-flipping sketchbook of Singapore in one static HTML file. [Live](https://mengto.com)
- **[A Long-Expected Party](https://github.com/MengTo/a-long-expected-party)** — a procedural short film rendered live in the browser, with a Higgsfield-generated score and narration. [Live](https://mengto.github.io/a-long-expected-party/)

## What I build

- **[Aura](https://aura.build)** — an AI website builder that creates landing pages in seconds and exports to HTML and Figma.
- **[Design+Code](https://designcode.io)** — learn to design and code React and Swift apps.
- **[DreamCut](https://dreamcut.ai)** — an AI video editor and screen recorder.
