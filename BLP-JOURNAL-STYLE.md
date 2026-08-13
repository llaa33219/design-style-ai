# BLP Journal Style

> A restrained, paper-tone design language for scholarly web.
> Scholarly journal + research report feel. 2px hairline. Fully orthogonal.
> Single accent: BLP BLUE. Soft tones reserved for state only.

This document is the **single source of truth**. To build a page in this style,
read it once, then build from the tokens and components defined here. Do not
hard-code values — read from CSS custom properties.

---

## 0. The Five Rules

1. **2px borders only.** No other border weights. No `border-radius`.
2. **Single accent color** — `BLP BLUE #007BFF` (light) / `CLI ACCENT BLUE #2fc2ff` (dark). Used only for links, the 4px emphasis bar, and the active state of the section nav. Nothing else may be blue.
3. **Soft tones are state only** — `SOFT GREEN / YELLOW / RED` are for badges and `OK / WARN / ERR` states. Never decorative.
4. **1200px main container.** Body is paper-blue (`#F4F8FC`); the main container is a white paper sheet (`#FAFCFF`) framed by 2px hairlines on its left and right.
5. **BookkMyungjo for prose; CloudSansCode for code and data.** Body leading is 1.75. Headings tighten to 1.25.

---

## 1. Design Tokens

All tokens are CSS custom properties declared on `:root`. The dark theme
is declared on `:root[data-theme="dark"]`. There is no class-based theme;
the `data-theme` attribute on `<html>` is the only switch.

### 1.1 Color

#### Light (default)

| Token           | Value      | Source                  | Use                                  |
|-----------------|------------|-------------------------|--------------------------------------|
| `--bg`          | `#F4F8FC`  | BLP PAPER BLUE          | Page ground (desk)                   |
| `--surface`     | `#FAFCFF`  | BLP WHITE               | Main container / card / table ground |
| `--surface-alt` | `#EEF5FC`  | BLP BG BLUE             | Table head fill, inline-code chip    |
| `--line`        | `#C7CBD1`  | BLP LIGHT DEEP DARK     | 2px hairline                         |
| `--line-strong` | `#3e4d5f`  | BLP SUB DARK            | Heavy rules (rare)                   |
| `--ink`         | `#000a19`  | BLP DEEP DARK           | Body text                            |
| `--ink-soft`    | `#3e4d5f`  | BLP SUB DARK            | Caption, meta, secondary text        |
| `--ink-mute`    | `#8598AD`  | BLP LIGHT ULTRA DEEP BLUE | Disabled                            |
| `--accent`      | `#007BFF`  | BLP BLUE                | Links, emphasis bar                  |
| `--accent-deep` | `#005BDD`  | BLP DEEP BLUE           | `:hover`                             |
| `--accent-soft` | `#DBEDFF`  | BLP LIGHT BLUE          | `::selection`, mark                  |
| `--ok`          | `#6bd67b`  | BLP SOFT GREEN          | OK badge                             |
| `--warn`        | `#ffeb7f`  | BLP SOFT YELLOW         | Warn badge                           |
| `--err`         | `#ff7f7f`  | BLP SOFT RED            | Error badge                          |
| `--ok-ink`      | `#007512`  | BLP ULTRA DEEP GREEN    | OK badge text                        |
| `--warn-ink`    | `#B2A400`  | BLP ULTRA DEEP YELLOW   | Warn badge text                      |
| `--err-ink`     | `#A30000`  | BLP ULTRA DEEP RED      | Error badge text                     |

#### Dark (overrides only)

| Token           | Value      | Source                  | Note                            |
|-----------------|------------|-------------------------|---------------------------------|
| `--bg`          | `#00193D`  | BLP DARK                |                                 |
| `--surface`     | `#00193D`  | BLP DARK                | Same as bg; the 2px border separates |
| `--surface-alt` | `#000a19`  | BLP DEEP DARK           |                                 |
| `--line`        | `#1e2b3d`  | BLP SOFT DARK           |                                 |
| `--line-strong` | `#BDCBDB`  | BLP LIGHT DEEP BLUE     |                                 |
| `--ink`         | `#FAFCFF`  | BLP WHITE               |                                 |
| `--ink-soft`    | `#BDCBDB`  | BLP LIGHT DEEP BLUE     |                                 |
| `--accent`      | `#2fc2ff`  | BLP CLI ACCENT BLUE     | Replaces BLP BLUE for readability |
| `--accent-deep` | `#7fbcff`  | BLP SOFT BLUE           | `:hover`                        |
| `--accent-soft` | `#0026A3`  | BLP ULTRA DEEP BLUE     | `::selection`                   |

The state tones (`--ok`, `--warn`, `--err`) are identical in both themes.

### 1.2 Spacing (4px base)

```
--s-1:   4px
--s-2:   8px
--s-3:  12px
--s-4:  16px
--s-5:  20px
--s-6:  24px
--s-7:  32px
--s-8:  40px
--s-9:  56px
--s-10: 72px
```

Use these exclusively. Never write raw `px` for spacing.

### 1.3 Type Scale (1.25 ratio, 17px base)

```
--fs-0: 12px   caption / meta
--fs-1: 14px   small
--fs-2: 17px   body
--fs-3: 21px   h4
--fs-4: 26px   h3
--fs-5: 33px   h2
--fs-6: 41px   h1
--fs-7: 52px   display (rare)
```

```
--lh-tight: 1.25   headings
--lh-body:  1.75   body
```

### 1.4 Borders & Radius

```
--bw:        2px     all rules
--bw-thick:  4px     emphasis bar (left of quote/abstract/callout)
--radius:    0       always
```

### 1.5 Motion

```
--t-fast: 150ms     hover, focus, theme switch
--t-base: 150ms     same
--ease:   ease-out
```

There is no `slow` transition. Do not introduce one.

### 1.6 Container

```
--container: 1200px
--gutter:    24px
```

---

## 2. Typography

### 2.1 Fonts

```css
@font-face {
  font-family: 'BookkMyungjo';
  src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_2302@1.0/BookkMyungjo-Lt.woff2') format('woff2');
  font-weight: 400;
  font-display: swap;
}
@font-face {
  font-family: 'BookkMyungjo';
  src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_2302@1.0/BookkMyungjo-Bd.woff2') format('woff2');
  font-weight: 700;
  font-display: swap;
}
@font-face {
  font-family: 'CloudSansCode';
  src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/2408@1.0/goorm-sans-code.woff2') format('woff2');
  font-weight: 400;
  font-display: swap;
}
```

### 2.2 Stack

- **Body & headings:** `'BookkMyungjo', 'Source Serif Pro', 'Noto Serif KR', Georgia, serif`
- **Code & data:** `'CloudSansCode', ui-monospace, monospace`

The same family (BookkMyungjo) is used for both body and headings; the
contrast comes from `font-weight: 700` and size, not from switching
families. The only exception is code.

### 2.3 Application

- Body: 17px / 1.75.
- Headings: tighter leading (1.25); size follows the scale.
- Code inline: 0.88em on `--surface-alt` with a 1px `--line` chip.
- Code block: 14px / 1.6, no box — only top & bottom 2px hairlines.

---

## 3. Geometry

### 3.1 The Page

Three horizontal bands stacked vertically, all on the paper-blue desk (`--bg`):

```
┌──────────────────────────────────────────────────┐
│  meta-bar  (top hairline)                        │
├──────────────────────────────────────────────────┤
│  site-header  (left/right open, bottom hairline) │
├────┬──────────────────────────────────────┬──────┤
│    │  main .container  (left+right hair)  │      │
│    │   white paper, padding 24            │      │
│    │                                      │      │
├────┴──────────────────────────────────────┴──────┤
│  site-footer  (top hairline)                     │
└──────────────────────────────────────────────────┘
```

- `meta-bar` is full-width; inner is centered at 1200px max.
- `site-header` is full-width; inner is centered at 1200px max; **no left/right hairline on header inner**.
- `main.page` holds the only `.container` that gets `border-left` + `border-right`.
  The container's top is closed by the header's `border-bottom`; its bottom
  is closed by the footer's `border-top`.
- `site-footer` is full-width; **the .container inside the footer must not
  have left/right hairlines**. The implementation uses
  `.site-footer .container { border-left: 0; border-right: 0; }` to enforce this.
- The four-column footer grid is `1.4fr 1fr 1fr 1fr`.

### 3.2 The Emphasis Bar

The 4px `--bw-thick` bar is the system's only decoration. It is reserved
for:

- the left edge of an `abstract`, `quote`, or `callout`
- the active section indicator on `primary-nav`
- nothing else

### 3.3 Mobile

Below 880px:

- Header switches to a two-row layout: brand + actions on row 1, nav below
  the nav becomes horizontally scrollable.
- Paper meta `dl` collapses to a two-column key/value grid.
- Figure swatches: 4 cols → 2 cols.
- Component gallery grid: 2 cols → 1 col.
- Footer columns: 4 → 2.
- Paper article body width: full.
- Paper title size: 34px.
- Container still extends full-bleed (no `max-width: 100%` regression);
  the 2px hairlines continue to be drawn on the container's edges.

---

## 4. Components

### 4.1 Meta Bar (top strip)

Vol. / No. / ISSN / today stamp. `var(--fs-0)`, `var(--ink-soft)`. The
`<b>` label `BLP JOURNAL` is `var(--ink)`. Bottom hairline only.

### 4.2 Site Header (left logo / center nav / right buttons)

- **Brand (left):** a 32×32 mark on `--accent` showing the letter `B` in
  `BookkMyungjo 700`, then the wordmark `BLP JOURNAL` in `700` with
  `letter-spacing: 0.08em`.
- **Primary nav (center):** five items, `var(--fs-1)`, color `--ink-soft`,
  `border-bottom: 0`. Active state: `color: var(--ink)` +
  `border-top: var(--bw) solid var(--accent)`. Hover: color `--ink`.
- **Actions (right):** theme toggle (`btn--ghost btn--sm`) and a
  `Subscribe` call to action (`btn--solid btn--sm`).
- Sticky at top with `position: sticky`.

### 4.3 Buttons

Two variants; never invent a third.

| Variant    | Background                | Border              | Text          |
|------------|---------------------------|---------------------|---------------|
| `--solid`  | `var(--accent)`           | `var(--accent)`     | `#fff`        |
| `--ghost`  | transparent               | `var(--ink)`        | `var(--ink)`  |

Sizes: default (8/16 padding, `--fs-1`) and `--sm` (5/10 padding, `--fs-0`).

Hover: solid → fill darkens to `var(--accent-deep)`, border matches.
       ghost → fill becomes `var(--ink)`, text becomes `var(--bg)`.

Focus: `outline: var(--bw) solid var(--accent); outline-offset: 2px`.

Disabled: `opacity: 0.4; cursor: not-allowed`.

### 4.4 Masthead (article title block)

- `masthead__kicker` (uppercase, `--fs-0`, `--ink-soft`, letter-spacing 0.12em).
- `.paper-title` (`--fs-6`, 700, line-height tight).
- `.byline` (flex row) — names in 700, affiliation in `--ink-soft`.
  Wrapped in a 2px top + 2px bottom hairline band.
- `.paper-meta dl` — three columns of `dt` / `dd`. `dt` is uppercase
  `--ink-soft` with letter-spacing; `dd` is `--ink` in `CloudSansCode`.

### 4.5 Abstract

`var(--surface)` background, 2px `--line` border, **4px `--accent` left
bar**. Heading `Abstract` is uppercase `--accent` 700. Body uses
`<b>` and `<i>` for emphasis; `<code class="inline">` for token names;
`.ink-accent` (color `--accent`, weight 700) for inline accent phrases.

### 4.6 Headings

- `h2.paper-h2` — `--fs-5`, 700, tight leading, `border-bottom: var(--bw)
  solid var(--line)`, generous top margin (`--s-9`).
- `h3.paper-h3` — `--fs-4`, 700, tight leading, no border, top margin `--s-7`.
- `h4` (rare) — `--fs-3`, 700.

### 4.7 Quote

`border-left: var(--bw-thick) solid var(--accent)`, no background. Quote
text in `--fs-3` italic. Cite in `--fs-0` `--ink-soft`.

### 4.8 Table

`border: var(--bw) solid var(--line)`, no zebra. `<thead> <th>` are
inverted: `background: var(--ink)`, color `var(--bg)`, uppercase,
`--fs-0`, letter-spacing 0.08em. Body cells: top hairline, vertical-align
top. Inline `<code class="inline">` is the standard for token/value
cells.

### 4.9 Code block

`pre.codeblock`. No box. Just `border-top` and `border-bottom` 2px.
`--fs-1`, leading 1.6, `CloudSansCode`. `overflow-x: auto`.

### 4.10 Inline code

`code.inline` — `0.88em` on `--surface-alt` with 1px `--line` chip. Use
for token names, file paths, command snippets, and small data references.

### 4.11 Figure / swatch

`figure` holds a `figure__swatches` grid. Each `swatch` is a flex row:
40×40 chip + name + `<code>` hex. Grid is 4 cols on desktop, 2 cols on
mobile. `border-right` separates cells; the rightmost in each row has
`border-right: 0`.

### 4.12 Form

`.field` is a labeled block. `.field__label` is uppercase `--ink-soft`
`--fs-0`. `.field__input` is full-width, `var(--bg)` background, 2px
`--line` border, focus → `var(--accent)` border.

### 4.13 Badges

Three states: `--ok`, `--warn`, `--err`. The badge *fills* the soft tone
and uses the corresponding `--*-ink` text. Uppercase, `--fs-0`, 2px
border matching fill.

### 4.14 Callout

`background: var(--surface-alt)`, 2px `--line` border, **4px `--accent`
left bar**. Body in `--fs-1`. Use sparingly — one per section.

### 4.15 Footer

- 4 columns (1.4fr 1fr 1fr 1fr).
- All text is `var(--ink)` — color does not carry hierarchy. Hierarchy
  is created by weight (`brand` is 700), uppercase + letter-spacing
  (section heads), and the absence of decoration.
- Links: `border-bottom: 0`, hover → `var(--accent)`.
- `.site-footer__copy` is separated from the columns by a top hairline.
- The footer `.container` does not have a left/right hairline (see §3.1).

---

## 5. Theming

- Default is `light`. Set `data-theme="light"` on `<html>` explicitly.
- Toggle JS flips between `light` and `dark` and persists to
  `localStorage` under the key `blp-journal-theme`.
- Restoration order: `localStorage` → `light` default.
- On theme switch, the only thing that should change is which token
  values apply. Components and layout do not change.

---

## 6. Reference HTML Skeleton

```html
<!DOCTYPE html>
<html lang="ko" data-theme="light">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>...</title>
  <style>@font-face{ /* BookkMyungjo 400, 700; CloudSansCode 400 */ }</style>
  <link rel="stylesheet" href="./tokens.css" />
  <link rel="stylesheet" href="./style.css" />
</head>
<body>
  <div class="meta-bar"><div class="meta-bar__inner">...</div></div>

  <header class="site-header"><div class="site-header__inner">
    <a class="brand" href="#"><span class="brand__mark">B</span><span class="brand__word">BLP JOURNAL</span></a>
    <nav class="primary-nav">...items...</nav>
    <div class="site-header__actions">
      <button class="btn btn--ghost btn--sm" id="themeToggle">...</button>
      <a class="btn btn--solid btn--sm" href="#">Subscribe</a>
    </div>
  </div></header>

  <main class="page">
    <div class="container">
      <!-- paper, components, etc. -->
    </div>
  </main>

  <footer class="site-footer">
    <div class="container site-footer__inner">...</div>
    <div class="container site-footer__copy">...</div>
  </footer>

  <script src="./script.js" defer></script>
</body>
</html>
```

---

## 7. Do / Don't

| Do                                                 | Don't                                       |
|----------------------------------------------------|---------------------------------------------|
| Read every value from a token                      | Hard-code `#007BFF`, `2px`, `1.75`          |
| Use `var(--accent)` for links and the 4px bar      | Use BLP BLUE for buttons, headings, or icons |
| Use `var(--ok/warn/err)` for state                 | Use a soft tone as decoration               |
| Use BookkMyungjo for prose, CloudSansCode for code | Mix code-font glyphs into body text         |
| Use one of the spacing tokens                      | Write `13px` or `23px`                      |
| Set `border-radius: 0` once and inherit            | Round any corner                            |
| Use `--bw` (2px) for hairlines                     | Use 1px or 3px borders                      |
| Use `--bw-thick` (4px) for the emphasis bar        | Use 3px or 5px                              |
| Mark up tokens as `<code class="inline">`          | Use `<span>` with manual styling            |
| Animate at 150ms ease-out                          | Animate at 300ms or with `linear`           |

---

## 8. Acceptance Checklist

Before shipping a page in BLP Journal Style, verify:

- [ ] Every color, size, and spacing is read from a token.
- [ ] No element has `border-radius` other than 0.
- [ ] Every border is 2px (or 4px for the emphasis bar).
- [ ] BLP BLUE is used only on links, the 4px bar, and the active nav indicator.
- [ ] Soft tones appear only on badges / state.
- [ ] Body sets 17px / 1.75 in BookkMyungjo.
- [ ] Code is CloudSansCode.
- [ ] The main container is 1200px and has 2px hairlines on its left and right.
- [ ] The footer `.container` has no left/right hairlines.
- [ ] Light/dark both render; theme toggle persists in `localStorage`.
- [ ] Mobile ≤ 880px collapses grids, scrolls nav, and keeps full-bleed hairlines.
