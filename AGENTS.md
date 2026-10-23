# AGENTS.md

Guidance for AI agents working in this repository.

## Repository layout

- `index.html` (repo root) — the landing page that links to every app. **Keep its current
  styling as-is**; it is the neutral "lab index" and is intentionally *not* themed per topic.
- Each subdirectory (e.g. `anatonurse/`, `tokenforge/`) is a **separate, self-contained
  single-page web app** (one `index.html` with inline CSS/JS, libraries from CDNs). There is no
  build step, package manager or test suite — open the files directly in a browser.

## Design preference: every app gets a topic-matched aesthetic

The owner wants each app's look & feel to **match its subject matter**, rather than sharing a
generic "dark glassmorphism + cyan gradient" AI look. When you create a new app or touch an
existing one, keep (or give) it a distinctive visual identity derived from its topic: palette,
typography, textures, shapes and small decorative motifs.

Current themes (keep them consistent when editing):

| App | Topic | Theme |
| --- | --- | --- |
| `tokenforge/` | How LLMs work (tokens → embeddings → attention → sampling) | **"The Foundry"** — dark blackened-iron background with hammered-metal noise, ember-orange / molten-gold accents, quench-steel teal as secondary, riveted steel-plate cards, stamped labels. Fonts: Barlow / Barlow Condensed (uppercase display) + JetBrains Mono. |
| `anatonurse/` | 3D anatomy & nursing assessment atlas | **"Clinical Chart"** — light ECG-paper grid background, white charting-paper panels, ceil-blue "scrubs" accents, medical-cross red, bedside-monitor style vitals strip. Fonts: Atkinson Hyperlegible (legibility-focused) + IBM Plex Mono. |
| `cardiotrace/` | EKG & bedside telemetry interpretation (Primer → Basic → Intermediate → Advanced) | **"Telemetry Central & Thermal Strip"** — ICU/telemetry central station dark phosphor-slate bezels (`#070d12` / `#0d1720`) paired with authentic 25mm/s pink/red millimeter thermal ECG paper strips (`#fff8f6` with `#d13b49` 5mm & `#e26270` 1mm grids), phosphor waveform green (`#00f57a`), SpO2 cyan, NIBP amber, alarm crimson, and draggable gold electronic calipers. Fonts: Atkinson Hyperlegible + Chakra Petch + IBM Plex Mono. |
| `linux95/` | 1995 Linux Workstation & FVWM95 Micro-OS Emulator (WebContainer API + Comlink) | **"1995 Beige CRT Workstation & FVWM95 / Linux 95 Desktop"** — tactile putty-beige ABS Trinitron monitor & hardware deck (`#d5cfc1` / `#c2bba9`) with 3.5" floppy bay, 7-segment green/amber Turbo LED (`133` / `66` MHz), physical power switch, Award BIOS + LILO boot screen, and classic 3D beveled Windows 95 / FVWM95 desktop (`#008080` teal, `#c0c0c0` win-gray, `#000080` navy titlebars). Fonts: VT323 + IBM Plex Mono + Chakra Petch + Tahoma/MS Sans Serif. |

Each app's theme is documented in a comment at the top of its `<style>` block and most of the
theme flourishes live in a clearly labelled "THEME LAYER" section placed *before* the
responsive `@media` rules (so the responsive overrides still win).

## Restyling rules

When asked to change appearance/aesthetics:

1. **Presentation only.** Do not change functionality, behaviour, text content, data, element
   IDs, class names used by JavaScript, DOM structure relied on by scripts, or library
   versions/imports.
2. Acceptable edits: CSS, font `<link>` tags, CSS custom properties, and *pure presentation
   literals* inside JS (colour strings, canvas/D3/Chart.js/Three.js styling colours, font names).
3. **Keep categorical data colours consistent.** Some colours encode meaning and must stay in
   sync between markup legends and JS data (e.g. the embedding-cluster colours in
   `tokenforge`, the anatomical system / assessment-site colours in `anatonurse`, and the
   "Teal = Active Pool" chart legend). Change them only together, or leave them alone.
4. Watch contrast when switching between light and dark themes: JS-generated markup may inject
   inline colours (e.g. badge text in a system colour). Prefer a scoped CSS override over
   rewriting logic.
5. Verify visually before finishing, e.g. with headless Firefox:
   `firefox --headless --no-remote --profile "$(mktemp -d)" --window-size=1400,2600 --screenshot out.png file://$PWD/<app>/index.html`
   (Headless Firefox here has no WebGL, so Three.js canvases render blank — that is expected.)
   Check a narrow (~400px) viewport too.
