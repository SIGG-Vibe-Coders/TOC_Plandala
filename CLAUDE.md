# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

TOC Plandala is a static web-based business process visualization platform for the Timber Operations Center (TOC). It renders interactive D3.js node/link graphs from JSON data files, with no backend or build step required. The site is hosted/served as static HTML.

## Architecture

**Data flow:** JSON data files → embedded in viewer HTML as JS constants → D3.js v7 renders interactive graphs in-browser.

- `index.html` — Main landing page with card grid linking to 12 process viewers across 6 categories (Org Chart, Planning & Dev, TSL Management, Engineering, Silviculture, GIS).
- `<Category>/TOC-*-viewer.html` — Self-contained interactive viewer pages (~3,600–6,600 lines each). These are generated/exported outputs from the Plandala app (plandala.io). They contain embedded data declarations marked with `export-critical` comments.
- `<Category>/TOC-*.json` — Source data files defining nodes, links, role colors, process types, and layout settings.
- `<Category>/*.png` — Static diagram images used as card thumbnails on the landing page.

**JSON data schema:**
```
{ appName, dataVersion, headerTitle, headerSubtitle,
  settings: { nodeWidth, nodeHeight, zoom, pan },
  roleColors: { role: hex },
  processTypes: { type: { label, shape, dashed } },
  nodes: [{ id, name, role, processType, x, y, desc, resources, width, height }],
  links: [{ source, target, label }] }
```

## Key Conventions

- **No build system** — No package.json, bundler, or build step. All files are served as-is.
- **Viewer HTML files are exports** — Do not manually rewrite viewer files from scratch. They are generated outputs with embedded Vite module code and D3.js rendering logic. Edit JSON data or the landing page instead.
- **Category directories** — Content is organized into: `Org_Chart/`, `Dev/`, `Eng/`, `Silv/`, `TSL/`, `GIS/`.
- **Naming pattern** — Files follow `TOC-[Process-Name]-viewer.html` and `TOC-[Process-Name].json`.
- **Design system** — Landing page uses warm earth tones (#2c3e2d, #4a7c59), Inter font, glassmorphism cards, 16px border-radius, responsive at 768px breakpoint.
- **External assets** — Logos load from `plandala.io` CDN.

## Git

- Remote: `origin` → `https://github.com/SIGG-Vibe-Coders/TOC_Plandala.git`
- Single branch: `master`
