# Grid Prompt Studio — Swiss Grid

A single-file web app that generates modular-grid **layout templates** and emits a ready-to-use
build prompt. It keeps the *load-bearing grid engineering* of the Müller-Brockmann skill (one
CSS-var source of truth, overlay sharing the content box, subgrid placement, baseline lock,
runtime optical alignment, G-key toggle) and renders in a clean **monochrome Swiss** design
system (warm off-white ground, near-black ink, light-gray offset "ghost" double-print, subtle
gray borders, tiny uppercase JetBrains-Mono labels) styled after the Grayn Studio shell. The
accent color is editable, so any hue (pink, blue, …) can be reintroduced on the poster.

Open `grid-prompt-studio.html` in any browser. No build step.

## Three-pane shell

- **LEFT — Layout picker.** A scrollable list of **256** clickable skeleton wireframe cards
  (骨架图), each a real composition. A search box + archetype filter chips narrow the list.
- **CENTER — Preview.** The live grid-engineered paper + toolbar (grid / decor / ghost
  toggles, dimensions, language, copy prompt, export PNG).
- **RIGHT — Properties.** Grid/field density, canvas format, grid-parameter sliders, accent
  color, and all page-element content fields, organized into cards.

## Two orthogonal axes

- **LAYOUT (composition)** — *how the elements are arranged*. Each layout places every element
  by **column line AND row line** (true 2D), so switching layouts genuinely **reflows** the page.
- **GRID / FIELD (density)** — *how many columns × rows* the module grid has. Independent control;
  changing it re-densifies the grid without changing the composition.

### 256 procedural layouts

Layouts are produced by a deterministic generator, not hand-authored. The layout index
`0…255` is a mixed-radix word over four orthogonal axes:

| Axis | Count | Values |
|------|-------|--------|
| Archetype | 8 | `editorial` · `split` · `poster` · `index` · `mosaic` · `feature` · `cover` · `triptych` |
| Row-count | 4 | 4 / 5 / 6 / 7 module rows |
| Mirror | 2 | columns flipped (centered items stay centered) |
| Emphasis | 4 | Standard / Swap (numeral↔figure) / Banner (full-width headline) / Hero (widened hero) |

`8 × 4 × 2 × 4 = 256`, and all 256 are **geometrically distinct** (a per-variation kicker-band
shift guarantees uniqueness even where a semantic transform would no-op). Archetypes store
items with normalized row bands; the chosen row-count maps them onto integer row lines at
placement time. Add archetypes freely in the `ARCHES` array — each contributes 32 layouts.

### Field (density) presets

`col12` (12-col + baseline) · `f6x6` · `f4x8` · `f8` (4×2) · `f20` (5×4) · `f32` (8×4).

### Canvas (format) presets

`spread` 1296 · `w1440` / `w900` (verify widths) · `a4p` / `a4l` · `sq` 1080² · `posterB2` (√2).

## Style

- Palette: ground `#FCFBF9`, ink `#171717` (near-black, editable accent), ghost `#D4D4D4`,
  body `hsl(0 0% 13%)`.
- **Ghost double-print** on display type — a light-gray copy offset behind the ink.
- **Decor layer** — 4-point sparkle stars + wavy squiggle lines, behind content.
- Toggles in the toolbar: **Show/Hide grid** (or `G`), **Decor**, **Ghost**.

## Page elements

KICKER/date, TITLE/MASTHEAD, HEADLINE, LEAD, NUMERAL (+caption), META COLUMN A, META COLUMN B,
IMAGE URL, CAPTION. Each template uses these in its own arrangement.

## Output

- **Copy prompt** — emits, per element, its **column span + row placement** (true 2D), the
  palette + decoration directives (ghost, sparkles, squiggles, arched masthead, pill caption where
  used), the load-bearing-engineering rules, and the verify checklist.
- **Export PNG** — renders the preview at 2× (grid overlay auto-hidden in the export).

## Shareable presets (URL params)

`grid-prompt-studio.html?layout=18&field=col12&canvas=posterB2&lang=zh&bl=8&gu=24&im=12&accent=171717&grid=1&decor=1&ghost=1`

- `lang` = `zh` (default) or `en` — UI, layout/field/canvas names, sample content, and the
  generated prompt are all bilingual; toggle live with the language button in the toolbar
- `layout` = layout index `0…255` (legacy archetype names like `poster` still map to a
  representative index) · `field` = density · `canvas` = format
- `grid` / `decor` / `ghost` = `0` to start that layer off (all default on)

## Notes

- The preview auto-scales to fit BOTH width and height, so even tall canvases (A4, B2 poster)
  stay fully on screen — nothing is clipped.
- The ghost double-print fills the same box as the real text and inherits its wrapping /
  alignment, so it tracks the actual typeset layout (multi-line, centered, arched).
- CJK text uses Noto Sans SC; Latin display uses Inter; labels/captions use JetBrains Mono.
