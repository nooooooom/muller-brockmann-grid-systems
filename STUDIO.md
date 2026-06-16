# Grid Prompt Studio — Acid Swiss

A single-file web app that generates modular-grid **layout templates** and emits a ready-to-use
build prompt. It keeps the *load-bearing grid engineering* of the Müller-Brockmann skill (one
CSS-var source of truth, overlay sharing the content box, subgrid placement, baseline lock,
runtime optical alignment, G-key toggle) but renders in an **acid-Swiss** style (electric-blue
ground, hot-pink ink, navy offset "ghost" double-print, sparkles + squiggles).

Open `grid-prompt-studio.html` in any browser. No build step.

## Two orthogonal axes

The first version conflated these — fixed now:

- **LAYOUT (composition)** — *how the elements are arranged*. Each template places every element
  by **column line AND row line** (true 2D), so switching templates genuinely **reflows** the page.
  Picked via clickable **skeleton wireframe cards** (骨架图) auto-derived from the layout data.
- **GRID / FIELD (density)** — *how many columns × rows* the module grid has. Independent control;
  changing it re-densifies the grid without changing the composition.

### Composition templates

| Key | Name | Arrangement |
|-----|------|-------------|
| `editorial` | Editorial Stack | kicker → masthead → headline + big numeral → lead + tall figure → meta A/B + caption → folio |
| `split` | Asymmetric Split | full-height image left, text stack right |
| `poster` | Centered Poster | date top · arched/rotated masthead · giant central numeral · centered sub-headline · bottom pill caption (the reference look) |
| `index` | Index / Manifesto | giant data numeral left, right column reads as an index list, full-width folio |
| `mosaic` | Modular Mosaic | title band, then figure + numeral + meta tiled into separate modules |
| `feature` | Feature Spread | full-bleed figure top, masthead beneath, two body columns + meta |
| `cover` | Full-Bleed Cover | kicker top, masthead fills the page, meta + lead at the foot |
| `essay` | Two-Column Essay | masthead + sub-headline, left body column facing right figure |
| `triptych` | Triptych | three equal columns: title/headline/numeral over body/figure/meta |
| `statement` | Statement | single centered statement holds the page, kicker above, lead below |
| `contents` | Table of Contents | big title + numeral left, entries list running down the right |
| `datasheet` | Data Sheet | giant numeral left, title/headline + meta table on the right |

> The skill does **not** prescribe a fixed set of compositions — it only names the grid *density*
> options (field counts) and the typographic discipline; layout is open ("a number of possible
> uses ... each designer can look for a solution appropriate to his personal style"). These 12
> templates are representative starting points, not an exhaustive list — add more freely in the
> `TEMPLATES` map (each `place()` just returns elements positioned by column + row line).

### Field (density) presets

`col12` (12-col + baseline) · `f6x6` · `f4x8` · `f8` (4×2) · `f20` (5×4) · `f32` (8×4).

### Canvas (format) presets

`spread` 1296 · `w1440` / `w900` (verify widths) · `a4p` / `a4l` · `sq` 1080² · `posterB2` (√2).

## Acid style

- Palette: ground `#1e22ff`, ink `#ff2e88`, ghost `#15158f`, body `#bfc0ff` (accent editable).
- **Ghost double-print** on display type — a navy `::before` copy offset behind the pink.
- **Decor layer** — 4-point sparkle stars + wavy squiggle lines (pink + navy), behind content.
- Toggles in the toolbar: **Show/Hide grid** (or `G`), **Decor**, **Ghost**.

## Page elements

KICKER/date, TITLE/MASTHEAD, HEADLINE, LEAD, NUMERAL (+caption), META COLUMN A, META COLUMN B,
IMAGE URL, CAPTION. Each template uses these in its own arrangement.

## Output

- **Copy prompt** — emits, per element, its **column span + row placement** (true 2D), the acid
  palette + decoration directives (ghost, sparkles, squiggles, arched masthead, pill caption where
  used), the load-bearing-engineering rules, and the verify checklist.
- **Export PNG** — renders the preview at 2× (grid overlay auto-hidden in the export).

## Shareable presets (URL params)

`grid-prompt-studio.html?layout=poster&field=col12&canvas=posterB2&lang=zh&bl=8&gu=24&im=12&accent=ff2e88&grid=1&decor=1&ghost=1`

- `lang` = `zh` (default) or `en` — UI, template/field/canvas names, sample content, and the
  generated prompt are all bilingual; toggle live with the language button in the toolbar
- `layout` = composition template · `field` = density · `canvas` = format
- `grid` / `decor` / `ghost` = `0` to start that layer off (all default on)

## Notes

- The preview auto-scales to fit BOTH width and height, so even tall canvases (A4, B2 poster)
  stay fully on screen — nothing is clipped.
- The navy ghost double-print fills the same box as the real text and inherits its wrapping /
  alignment, so it tracks the actual typeset layout (multi-line, centered, arched).
- CJK text uses Noto Sans SC; Latin display uses Inter.
