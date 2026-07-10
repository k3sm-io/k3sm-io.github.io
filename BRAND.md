# k3sm brand & style guide

The single source of truth for k3sm's visual identity. Every k3sm-io repo, doc site,
and generated page should derive from these tokens rather than restating values.
Canonical implementation: [`index.html`](index.html) on this repo (live at [k3sm.io](https://k3sm.io)).

## Wordmark

Lowercase `k3sm`, set in the UI monospace stack, weight 600, letter-spacing `.02em`,
preceded by a 9×9px square with 2px radius in the accent color:

```html
<span class="wordmark">k3sm</span>
```
```css
.wordmark{
  display:inline-flex;align-items:center;gap:.6ch;
  font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;
  font-weight:600;font-size:18px;letter-spacing:.02em;
}
.wordmark::before{
  content:"";width:9px;height:9px;border-radius:2px;
  background:var(--accent);display:inline-block;
}
```

Never capitalize (`K3sm`, `K3SM`), never add a space (`k3 sm`), never restyle the
square (it is the mark). The favicon is the dark rounded square with a monospace
lowercase `k` (see `index.html` for the inline SVG).

## Color tokens

Define once on `:root`, override per theme. Components must reference tokens, never
raw hex.

| Token | Light | Dark | Role |
|---|---|---|---|
| `--bg` | `#f7f7f8` | `#0a0b0d` | page ground |
| `--ink` | `#0b0c0e` | `#f3f4f6` | primary text |
| `--muted` | `#6b7177` | `#9aa1a9` | secondary text |
| `--line` | `#e4e6ea` | `#23262c` | hairline rules, borders |
| `--grid` | `rgba(0,0,0,.035)` | `rgba(255,255,255,.035)` | background grid |
| `--accent` | `#3b5bdb` | `#6d8bff` | the one accent — wordmark square, links, emphasis |
| `--glow` | `rgba(59,91,219,.06)` | `rgba(109,139,255,.10)` | radial wash behind heroes |

Semantic status colors (docs, dashboards, tables) are separate from the accent and
used only for state, never decoration:

| Token | Light | Dark | Meaning |
|---|---|---|---|
| `--good` | `#2f9e63` | `#4cc287` | ok / supported / yes |
| `--warn` | `#c47f17` | `#e0a33e` | partial / caution |
| `--none` | `#9aa1a9` | `#7c838b` | absent / not applicable |

Rules of use: one accent per page, spent sparingly. Neutrals do the work. No
gradients except the single radial `--glow` wash. No additional hues.

## Typography

- **Body:** `system-ui,"Segoe UI",Roboto,Helvetica,Arial,sans-serif` — the platform's
  own face, deliberately. k3sm is mac-native software; it wears the system type.
- **Mono (structural voice):** `ui-monospace,SFMono-Regular,Menlo,Consolas,monospace`
  — wordmark, eyebrows/labels, table headers, data, code. Labels get uppercase +
  `.10–.14em` letter-spacing at 11–12px.
- Headlines: weight 600, tight leading (`1.08–1.1`), letter-spacing `-.02em`,
  `text-wrap:balance`. No font heavier than 600 anywhere.
- Body ~15–17px, line-height ~1.55, measure ≤ 65ch. Numeric columns get
  `font-variant-numeric:tabular-nums`.

## Layout language

- Single centered column (`max-width` 680px for prose pages, up to ~940px for docs
  with tables), generous top padding.
- **Hairline rules** (`1px` `--line`) frame sections — the landing page's
  top-rule/content/bottom-rule rhythm is the house structure.
- **Grid ground:** 46px background grid in `--grid` plus one radial `--glow` wash,
  `background-attachment:fixed`. Use on standalone pages; omit inside embedded docs.
- Corners: 7–8px radius on cards/containers, 2px on the mark. Nothing pill-shaped
  except status chips.
- Borders over shadows. If a shadow is unavoidable, keep it under `0 1px 3px`.

## Theming

Both themes are first-class. Token-level switching only:

```css
:root{ /* light values */ }
@media (prefers-color-scheme: dark){ :root{ /* dark values */ } }
:root[data-theme="dark"]{ /* dark values — explicit override */ }
:root[data-theme="light"]{ /* light values — explicit override */ }
```

## Voice

- Lowercase confidence: sentence case everywhere, including headings. No exclamation
  marks, no marketing superlatives.
- Say what the thing does: "runs your manifests on every Mac in the fleet," not
  "revolutionizes orchestration."
- Short declaratives. Technical nouns stay precise (launchd, vmnet, OCI); no
  invented jargon.
- Tagline register: *"Developer infrastructure, reimagined."* — statements, not
  slogans with verbs demanding things of the reader.

## GitHub repo conventions

- README title is the bare repo name in lowercase (`# runtimed`), first line a
  one-sentence plain description — matching the module's vanity import
  (`k3sm.io/runtimed`).
- Shared social-preview / banner assets live in this repo under `assets/` (to be
  added); repos reference, never fork, brand assets.
- Badges: minimal, monochrome where the service allows; never more than one row.
