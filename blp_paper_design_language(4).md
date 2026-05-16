# BLP Paper — Design System Specification

> 난해하고 유동적이며 몽환적인 논문의 시각화  
> A design language for visual academic communication.

---

## 1. Philosophy & Taboos

### 1.1 Three Central Themes

| Theme | Definition | Visual Expression |
|-------|-----------|-------------------|
| **Heterogeneity** | Coexistence of diverse styles | Mixed geometry (rect + triangle + asymmetric), mixed borders (solid + dashed), mixed rhythms |
| **Fluidity** | Nothing is static | All data elements breathe in time. Animation is explanation, not decoration |
| **Dreamlike** | Boundary between real and unreal blurs | Achieved only through **opacity layering**, **halftone dots**, and **tuned color families**. No blur, no gradient, no bloom |

### 1.2 Absolute Taboos

| Taboo | Exception |
|-------|-----------|
| Gradient (`linear-gradient`, `radial-gradient` as color transition) | None |
| Blur (`backdrop-filter`, `filter: blur`) | None |
| Bloom / Glow (`box-shadow` with spread, `filter: glow`) | None |
| Blurred shadow (`box-shadow` with blur radius > 0) | None. Only sharp offset shadows allowed (`blur: 0`) |
| Glassmorphism with blur | Forbidden |
| Circular blobs / organic rounded shapes | None. Functional pills only (`border-radius: 50px` for buttons/tags) |

> **How to create depth without blur/gradient/blobs:** opacity layering, halftone texture, tuned color families, sharp geometric contrast.

---

## 2. Design Tokens

### 2.1 Color Tokens

Colors are organized by **function**, not by hue. Each family has 4 tuned steps (Soft → Light → Deep → Ultra) where **hue is preserved but saturation and lightness are tuned together** for visual coherence.

#### Atmosphere (Backgrounds)

| Token | Hex | Usage |
|-------|-----|-------|
| `--blp-bg-orange` | `#FCF5EE` | Warm section backgrounds |
| `--blp-bg-blue` | `#EEF5FC` | Cool section backgrounds |
| `--blp-bg-gray` | `#F5F5F5` | Default page background |
| `--blp-bg-green` | `#B8E1D8` | Organic / natural sections |
| `--blp-bg-purple` | `#D9B8E1` | Dreamlike section accents |
| `--blp-bg-brown` | `#D09C7B` | Earthy / grounded sections |

#### Data (Primary Visual Elements)

| Token | Hex | HSL | Usage |
|-------|-----|-----|-------|
| `--blp-soft-blue` | `#7FBCFF` | 211°, 100%, 75% | Primary data, main charts |
| `--blp-soft-red` | `#FF7F7F` | 0°, 100%, 75% | Warnings, negative values, contrast |
| `--blp-soft-yellow` | `#FFEB7F` | — | Highlights, attention points |
| `--blp-soft-green` | `#6BD67B` | 129°, 57%, 63% | Growth, positive values |
| `--blp-soft-purple` | `#D67FFF` | 281°, 100%, 75% | Special / dreamlike data series |
| `--blp-soft-dark-blue` | `#7F9BFF` | — | Secondary data series |
| `--blp-soft-dark` | `#1E2B3D` | — | Primary text, anchors, dark elements |

#### Surface (Cards, Tables, Containers)

| Token | Hex | Usage |
|-------|-----|-------|
| `--blp-paper-orange` | `#F9F1E5` | Warm card surfaces |
| `--blp-paper-green` | `#EAF7EF` | Organic card surfaces |
| `--blp-paper-purple` | `#F1F0F5` | Dreamlike card surfaces |
| `--blp-paper-brown` | `#F5F2E9` | Grounded card surfaces |
| `--blp-paper-pink` | `#F1E8EC` | Soft card surfaces |
| `--blp-paper-blue` | `#F4F8FC` | Default card / chart container |
| `--blp-paper-lime` | `#F2F6ED` | Fresh card surfaces |

#### Depth Steps (Tuned Families)

**Blue Family:**

| Step | Hex | HSL | Role |
|------|-----|-----|------|
| Soft | `#7FBCFF` | 211°, 100%, 75% | Life. High saturation |
| Light | `#DBEDFF` | 210°, 100%, 93% | Surface. High lightness |
| Deep | `#BDCBDB` | 212°, 29%, 80% | Structure. Low saturation |
| Ultra | `#8598AD` | 212°, 20%, 60% | Text. Dark and muted |

**Purple, Green, Red families follow the same 4-step structure.** Saturation drops from 100% to ~20% across the steps. This is **visually tuned**, not mathematically monochromatic.

### 2.2 Typography Tokens

**Single Font Family:** `Goorm Sans`  
**CDN:** `https://statics.goorm.io/fonts/GoormSans/v1.0.0/GoormSans.min.css`

| Token | Size | Weight | Line Height | Letter Spacing | Transform | Usage |
|-------|------|--------|-------------|----------------|-----------|-------|
| Display XL | 72px | 700 | 1.1 | -0.02em | — | Hero titles |
| Display L | 48px | 700 | 1.1 | -0.02em | — | Section headers |
| Heading | 24px | 700 | 1.3 | — | — | Sub-sections |
| Body | 16px | 400 | 1.6 | — | — | Paragraphs, descriptions |
| Caption | 12px | 400 | 1.4 | 0.1em | uppercase | Labels, metadata, figure numbers |
| Mono | 14px | 400 | 1.5 | 0.02em | — | Data values, code, formulas |

> **Rule:** Text is always secondary to visual data. Use the minimum text necessary.

### 2.3 Spacing Tokens (4px base)

| Token | Value | Usage |
|-------|-------|-------|
| `space-xs` | 4px | Tight gaps, icon padding |
| `space-sm` | 8px | Inline spacing, halftone dot size reference |
| `space-md` | 16px | Component internal padding |
| `space-lg` | 24px | Card padding, section internal gaps |
| `space-xl` | 32px | Component margins |
| `space-2xl` | 48px | Section sub-gaps |
| `space-3xl` | 64px | Major section breaks |
| `space-4xl` | 96px | Section vertical padding (`py-24` equivalent) |

### 2.4 Border & Radius Tokens

**Border Width:**

| Token | Value | Usage |
|-------|-------|-------|
| `border-default` | 1px | Glass surfaces, dividers |
| `border-emphasis` | 2px | Hetero-1 cards, primary outlines |

**Border Style:**

| Token | Value | Usage |
|-------|-------|-------|
| `style-solid` | solid | Default, geometric precision |
| `style-dashed` | dashed | Fluidity, secondary states (Hetero-2) |

**Border Color:**

| Token | Value | Usage |
|-------|-------|-------|
| `border-glass` | `rgba(255,255,255,0.8)` | Glass surfaces |
| `border-soft` | Soft series color | Emphasis borders |

**Radius:**

| Token | Value | Usage |
|-------|-------|-------|
| `radius-sm` | 12px | Table cell corners |
| `radius-md` | 24px | Cards, containers |
| `radius-lg` | 28px / 4px | Hetero-1 (asymmetric) |
| `radius-xl` | 4px / 32px | Hetero-2 (asymmetric) |
| `radius-full` | 50px | Buttons, pills, tags, bars only |

> **Rule:** `radius-full` is forbidden for large containers or decorative shapes. Use only for buttons, tags, pills, and progress bars where content is centered and never clipped.

### 2.5 Animation Tokens

| Token | Value | Usage |
|-------|-------|-------|
| `duration-fast` | 0.3s | Hover states, micro-interactions |
| `duration-normal` | 0.4s | Button transitions, card transforms |
| `duration-slow` | 0.6s | Morphing, drawing animations |
| `duration-ambient` | 3s–8s | Background loops, floating |
| `easing-default` | `cubic-bezier(0.4, 0, 0.2, 1)` | Standard transitions |
| `easing-bounce` | `ease-in-out` | Floating, levitation |

---

## 3. Foundation Rules

### 3.1 Color Usage Matrix (Hard Rules)

| Context | Background | Border | Text | Accent / Data |
|---------|-----------|--------|------|---------------|
| **Primary Button** | `--blp-soft-blue` | — | White | — |
| **Secondary Button** | Transparent | `rgba(30,43,61,0.2)` | `--blp-soft-dark` | — |
| **Default Card** | `--blp-paper-blue` | `rgba(255,255,255,0.8)` | `--blp-soft-dark` | — |
| **Card Hover** | `rgba(219,237,255,0.4)` | `rgba(255,255,255,0.8)` | `--blp-soft-dark` | — |
| **Table Header** | Transparent | — | `--blp-ultra-dark` | — |
| **Table Row** | `rgba(255,255,255,0.55)` | `rgba(255,255,255,0.9)` | `--blp-soft-dark` | — |
| **Table Row Hover** | `rgba(219,237,255,0.6)` | `rgba(255,255,255,0.9)` | `--blp-soft-dark` | — |
| **Chart Primary** | `--blp-paper-blue` | — | — | `--blp-soft-blue` |
| **Chart Secondary** | — | — | — | `--blp-soft-red` |
| **Chart Tertiary** | — | — | — | `--blp-soft-green` |
| **Navigation** | `rgba(255,255,255,0.65)` | `rgba(255,255,255,0.6)` | `--blp-ultra-dark` | — |
| **Page Background** | `--blp-bg-gray` | — | — | Halftone overlay |
| **Tag / Badge** | Soft series 20% opacity | Soft series 30% opacity | `--blp-soft-dark` | — |

> **Rule:** Never use a Data (Soft) color for a large surface area. Soft colors are for data points, accents, and small interactive elements only.

### 3.2 Transparency Layering Rules

```css
/* Level 1: Base glass */
.layer-glass {
  background: rgba(244, 248, 252, 0.45);
  border: 1px solid rgba(255, 255, 255, 0.8);
}

/* Level 2: Strong glass */
.layer-glass-strong {
  background: rgba(255, 255, 255, 0.65);
  border: 1px solid rgba(255, 255, 255, 0.9);
}
```

**Rules:**
- Always combine with a solid `border` (1px, white with opacity).
- Never use `backdrop-filter`.
- Layer multiple `.layer-glass` elements with 8px–16px offset to create depth.
- Background opacity must stay between 0.35 and 0.65 for readability.

### 3.3 Halftone Rules

```css
body::before {
  content: '';
  position: fixed;
  inset: 0;
  z-index: -1;
  pointer-events: none;
  background-image: radial-gradient(
    circle,
    rgba(214, 127, 255, 0.12) 1.5px,
    transparent 1.6px
  );
  background-size: 28px 28px;
}
```

**Hard Rules:**
- **Dot size:** 1.5px radius (3px diameter).
- **Spacing:** 28px × 28px (wide).
- **Opacity:** 12% (0.12).
- **Color:** Default is Soft Purple (`#D67FFF`). Change to match the section's dominant hue if needed.
- **Placement:** Only on `body::before` or large section backgrounds. Never on cards, tables, or data elements.
- **Purpose:** Atmospheric texture only. Not for representing images or data.

### 3.4 Heterogeneity Rules

Two border systems exist. Use them intentionally:

| System | Class | Radius | Border | Background | Usage |
|--------|-------|--------|--------|-----------|-------|
| **Geo-Precision** | `.hetero-1` | 28px 4px 28px 4px | 2px solid Soft Blue | Paper Blue | Data cards, charts |
| **Fluid-Secondary** | `.hetero-2` | 4px 32px 4px 32px | 1.5px dashed Soft Purple | Paper Purple | Process flows, secondary info |

**Rules:**
- Never use plain `border-radius: 8px` or `16px`. Always use one of the two systems or `radius-md` (24px).
- Mix at least two different hetero systems within one viewport to maintain heterogeneity.
- Organic blob shapes (`.hetero-3`) are **removed** — content clipping issues.

---

## 4. Component Specifications

### 4.1 Button

**Primary Button (`.fluid-btn`)**

```css
.fluid-btn {
  position: relative;
  overflow: hidden;
  background: var(--blp-soft-blue);      /* #7FBCFF */
  border: none;
  border-radius: 50px;                     /* radius-full */
  color: white;
  font-family: var(--font-body);             /* Goorm Sans */
  font-weight: 500;
  font-size: 16px;
  padding: 16px 32px;
  cursor: pointer;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.fluid-btn:hover {
  transform: translateY(-2px);
  background: var(--blp-soft-dark-blue);   /* #7F9BFF */
}
```

**Secondary Button**

```css
.btn-secondary {
  background: transparent;
  border: 1px solid rgba(30, 43, 61, 0.2);
  border-radius: 50px;
  color: var(--blp-soft-dark);
  font-family: var(--font-body);
  font-weight: 500;
  font-size: 16px;
  padding: 16px 32px;
  cursor: pointer;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.btn-secondary:hover {
  background: rgba(255, 255, 255, 0.6);
}
```

> **Rule:** All buttons must be pill-shaped (`radius-full`). Never use rectangular buttons.

### 4.2 Card / Surface

**Default Card**

```css
.card-default {
  background: var(--blp-paper-blue);       /* #F4F8FC */
  border-radius: 24px;                     /* radius-md */
  padding: 32px;                             /* space-xl */
  /* No shadow. No blur. */
}
```

**Glass Card**

```css
.card-glass {
  background: rgba(244, 248, 252, 0.45);
  border: 1px solid rgba(255, 255, 255, 0.8);
  border-radius: 24px;
  padding: 32px;
}
```

**Hetero Cards**

Apply `.hetero-1` or `.hetero-2` directly. Padding is always `32px` unless nested.

### 4.3 Table

```css
.blp-table {
  width: 100%;
  border-collapse: separate;
  border-spacing: 0 8px;                     /* Fixed. Never change. */
}

.blp-table th {
  font-family: var(--font-mono);             /* Goorm Sans */
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--blp-ultra-dark);              /* #94989E */
  padding: 12px 16px;
  text-align: left;
}

.blp-table td {
  padding: 16px;
  background: rgba(255, 255, 255, 0.55);
  border-top: 1px solid rgba(255, 255, 255, 0.9);
  border-bottom: 1px solid rgba(255, 255, 255, 0.9);
  transition: all 0.3s ease;
}

.blp-table tr td:first-child {
  border-radius: 12px 0 0 12px;              /* radius-sm */
  border-left: 1px solid rgba(255, 255, 255, 0.9);
}

.blp-table tr td:last-child {
  border-radius: 0 12px 12px 0;
  border-right: 1px solid rgba(255, 255, 255, 0.9);
}

.blp-table tbody tr:hover td {
  background: rgba(219, 237, 255, 0.6);      /* Light Blue at 60% */
  transform: translateX(4px);                /* Micro-movement */
}
```

> **Rule:** `border-spacing: 0 8px` is sacred. The gap between rows creates the ethereal floating effect.

### 4.4 Chart Container

```css
.chart-container {
  position: relative;
  background: var(--blp-paper-blue);         /* #F4F8FC */
  border-radius: 24px;                       /* radius-md */
  padding: 32px;                             /* space-xl */
  overflow: hidden;
  /* No shadow. No border unless specified. */
}
```

**Internal Grid (for academic precision):**

```css
.chart-grid {
  background-image:
    linear-gradient(rgba(133, 152, 173, 0.15) 1px, transparent 1px),
    linear-gradient(90deg, rgba(133, 152, 173, 0.15) 1px, transparent 1px);
  background-size: 40px 40px;
}
```

> **Rule:** Chart grids use 1px solid lines at 15% opacity of Ultra Blue. Never use dotted or dashed grids.

### 4.5 Navigation

```css
.nav-glass {
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 50;
  background: rgba(255, 255, 255, 0.65);   /* layer-glass-strong */
  border-bottom: 1px solid rgba(255, 255, 255, 0.6);
  padding: 16px 24px;                        /* space-md space-lg */
}
```

> **Rule:** Nav height is not fixed by pixel. Let padding define it (16px vertical → ~64px total with content).

### 4.6 Tag / Badge

```css
.blp-tag {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 4px 12px;                         /* space-xs space-md */
  border-radius: 50px;                       /* radius-full */
  font-size: 12px;
  font-weight: 500;
  background: rgba(127, 188, 255, 0.2);      /* Soft Blue at 20% */
  border: 1px solid rgba(127, 188, 255, 0.3); /* Soft Blue at 30% */
  color: var(--blp-soft-dark);
}
```

> **Rule:** Tags always use a Soft color at 20% background + 30% border. Never solid Soft colors for tags.

---

## 5. Patterns

### 5.1 Data Visualization Color Assignment

When displaying multiple data series, assign colors in this exact priority:

1. **Primary:** Soft Blue (`#7FBCFF`)
2. **Secondary:** Soft Red (`#FF7F7F`)
3. **Tertiary:** Soft Green (`#6BD67B`)
4. **Quaternary:** Soft Yellow (`#FFEB7F`)
5. **Quinary:** Soft Purple (`#D67FFF`)
6. **Senary:** Soft Dark Blue (`#7F9BFF`)

**Rules:**
- Never use Light / Deep / Ultra colors for data lines or bars.
- Soft Dark (`#1E2B3D`) is reserved for text and outline nodes only.
- Background of all charts must be Paper Blue (`#F4F8FC`) or Paper Gray.

### 5.2 Animation Patterns

| Pattern | CSS Implementation | Duration | Usage |
|---------|-------------------|----------|-------|
| **Drawing** | `stroke-dasharray` + `stroke-dashoffset` animation | 3s | Paths, functions, flow diagrams |
| **Width Flow** | `width` percentage animation | 3s | Progress, distribution bars |
| **Dash Flow** | `stroke-dashoffset` loop | 2s–4s | Network edges, connections |
| **Pulse** | `scale` + opacity toggle | 2s | Live indicators, new data points |
| **Staggered Appear** | `opacity` + `transform` with delay | 0.5s each | Scatter points, histogram bars |

**Ambient Loop Easing:** Always `ease-in-out` for breathing animations. Never `linear` for organic motion.

### 5.3 Layout Patterns

**Container:**
- Max width: `1280px` (`max-w-7xl`)
- Horizontal padding: `24px` (mobile), `48px` (desktop)

**Section Spacing:**
- Vertical padding between major sections: `96px` (`space-4xl`)
- Gap between cards in a grid: `32px` (`space-xl`)

**Grid:**
- Use CSS Grid or Flexbox. No strict 12-column enforcement.
- Heterogeneity rule: vary card sizes within the same row intentionally.

---

## 6. Visualization Component Gallery

### 6.1 Mathematical Function Canvas

Real-time flowing function visualization. Multiple overlapping sine/cosine waves with floating data points.

- **Background:** Paper Blue (`#F4F8FC`)
- **Grid:** 1px lines at 15% opacity
- **Lines:** Soft series, 2–2.5px stroke, no glow
- **Points:** 6px radius, Soft color fill, 12px radius ring at 30% opacity
- **Animation:** Continuous time-based wave motion

### 6.2 Ethereal Data Table

Glass-layered table with row separation.

- **Spacing:** `border-spacing: 0 8px`
- **Row background:** `rgba(255,255,255,0.55)`
- **Hover:** Light Blue at 60% + 4px X translate
- **Cell corners:** 12px asymmetric (first/last cell only)

### 6.3 Heterogeneous Network Graph

Mixed-geometry node network.

- **Nodes:** Rectangles, circles, triangles, diamonds mixed
- **Edges:** 2px solid, `stroke-dasharray: 6,4` with dashoffset animation
- **Hover:** Node scales to 1.3x
- **No filters, no glow**

### 6.4 Scatter Plot with Regression

Sequential point appearance with regression line drawing.

- **Points:** 120 data points, 2–5px radius, staggered delay
- **Regression line:** Dashed purple (`#D67FFF`), 8px dash / 4px gap
- **Grid:** 50px interval, 15% opacity
- **Animation:** Points appear one by one, line draws after 60 frames

### 6.5 Correlation Heatmap

CSS Grid-based matrix with color-coded cells.

- **Cell size:** 48px × 48px
- **Color mapping:**
  - ≥ 0.6: Soft Blue
  - 0.2 ~ 0.6: Light Blue
  - -0.2 ~ 0.2: BG Gray
  - -0.6 ~ -0.2: Light Red
  - ≤ -0.6: Soft Red
- **Opacity:** `|value| × 0.6 + 0.2`
- **Hover:** Scale to 1.15x, z-index elevation
- **Legend:** 5-segment horizontal bar below matrix

### 6.6 Distribution Histogram

SVG bar chart with staggered height animation.

- **Bins:** 20 bars
- **Bar width:** 22px, gap 4px
- **Corner radius:** 2px
- **Fill:** Soft Blue at 85% opacity
- **Hover:** Changes to Soft Purple, 100% opacity
- **Animation:** Height grows from 0 with 0.05s stagger per bar

### 6.7 Radar Chart (Multivariate)

SVG polygon radar with 6 dimensions.

- **Grid:** 5 concentric polygons, 1px stroke at 20% opacity
- **Data polygon:** Soft Blue fill at 20% opacity, 2.5px stroke
- **Data dots:** 5px radius, white 2px stroke
- **Labels:** 11px mono, outside grid at radius + 25px
- **Scale:** 0–100

### 6.8 Data Flow Diagram (Sankey)

3-stage flow visualization with curved connectors.

- **Nodes:** Rounded rectangles (4px radius), Soft colors at 90% opacity
- **Flow lines:** SVG `path` with `stroke-linecap: round`, 40% opacity
- **Line width:** Proportional to flow volume
- **Labels:** 12px sans-serif, white text on colored nodes
- **Stages:** Raw → Train/Val → Model

---

## 7. Complete Starter Template

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>BLP Paper — Example</title>
  <link rel="stylesheet" href="https://statics.goorm.io/fonts/GoormSans/v1.0.0/GoormSans.min.css"/>
  <style>
    :root {
      /* Colors */
      --blp-soft-blue: #7FBCFF;
      --blp-soft-purple: #D67FFF;
      --blp-soft-green: #6BD67B;
      --blp-soft-red: #FF7F7F;
      --blp-soft-dark: #1E2B3D;
      --blp-bg-gray: #F5F5F5;
      --blp-paper-blue: #F4F8FC;
      --blp-ultra-dark: #94989E;
      --blp-light-blue: #DBEDFF;

      /* Typography */
      --font-body: 'Goorm Sans', sans-serif;
      --font-display: 'Goorm Sans', sans-serif;
      --font-mono: 'Goorm Sans', monospace;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: var(--font-body);
      background: var(--blp-bg-gray);
      color: var(--blp-soft-dark);
      -webkit-font-smoothing: antialiased;
    }

    /* Halftone background */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      z-index: -1;
      pointer-events: none;
      background-image: radial-gradient(
        circle,
        rgba(214, 127, 255, 0.12) 1.5px,
        transparent 1.6px
      );
      background-size: 28px 28px;
    }

    /* Components */
    .layer-glass {
      background: rgba(244, 248, 252, 0.45);
      border: 1px solid rgba(255, 255, 255, 0.8);
    }

    .layer-glass-strong {
      background: rgba(255, 255, 255, 0.65);
      border: 1px solid rgba(255, 255, 255, 0.9);
    }

    .hetero-1 {
      border-radius: 28px 4px 28px 4px;
      border: 2px solid var(--blp-soft-blue);
      background: var(--blp-paper-blue);
    }

    .hetero-2 {
      border-radius: 4px 32px 4px 32px;
      border: 1.5px dashed var(--blp-soft-purple);
      background: var(--blp-paper-purple);
    }

    .fluid-btn {
      background: var(--blp-soft-blue);
      border: none;
      border-radius: 50px;
      color: white;
      font-family: var(--font-body);
      font-weight: 500;
      font-size: 16px;
      padding: 16px 32px;
      cursor: pointer;
      transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    }

    .fluid-btn:hover {
      background: var(--blp-soft-dark-blue);
      transform: translateY(-2px);
    }

    .blp-table {
      width: 100%;
      border-collapse: separate;
      border-spacing: 0 8px;
    }

    .blp-table th {
      font-family: var(--font-mono);
      font-size: 12px;
      text-transform: uppercase;
      letter-spacing: 0.05em;
      color: var(--blp-ultra-dark);
      padding: 12px 16px;
      text-align: left;
    }

    .blp-table td {
      padding: 16px;
      background: rgba(255, 255, 255, 0.55);
      border-top: 1px solid rgba(255, 255, 255, 0.9);
      border-bottom: 1px solid rgba(255, 255, 255, 0.9);
    }

    .blp-table tr td:first-child {
      border-radius: 12px 0 0 12px;
      border-left: 1px solid rgba(255, 255, 255, 0.9);
    }

    .blp-table tr td:last-child {
      border-radius: 0 12px 12px 0;
      border-right: 1px solid rgba(255, 255, 255, 0.9);
    }

    .blp-table tbody tr:hover td {
      background: rgba(219, 237, 255, 0.6);
      transform: translateX(4px);
    }

    .chart-container {
      background: var(--blp-paper-blue);
      border-radius: 24px;
      padding: 32px;
      overflow: hidden;
    }
  </style>
</head>
<body>
  <nav class="layer-glass-strong" style="padding: 16px 24px; border-bottom: 1px solid rgba(255,255,255,0.6);">
    <span style="font-family: var(--font-display); font-weight: 700; font-size: 20px;">BLP Paper</span>
  </nav>

  <main style="max-width: 1280px; margin: 0 auto; padding: 96px 24px;">
    <h1 style="font-family: var(--font-display); font-weight: 700; font-size: 48px; line-height: 1.1; margin-bottom: 24px;">
      논문의 시각화
    </h1>
    <p style="font-size: 16px; line-height: 1.6; color: var(--blp-ultra-dark); margin-bottom: 32px;">
      BLP Paper는 글자가 아닌 시각적 자료를 중심으로 합니다.
    </p>
    <button class="fluid-btn">시작하기</button>
  </main>
</body>
</html>
```

---

## 8. Consistency Checklist

Before shipping any BLP Paper interface, verify:

- [ ] No `linear-gradient` or `radial-gradient` used as color transition.
- [ ] No `backdrop-filter` or `filter: blur` anywhere.
- [ ] No `box-shadow` with blur radius > 0.
- [ ] No circular blobs or organic rounded shapes (except functional pills/buttons/tags).
- [ ] All buttons are pill-shaped (`border-radius: 50px`).
- [ ] All cards use one of the two hetero systems or `radius-md` (24px).
- [ ] Table `border-spacing` is exactly `0 8px`.
- [ ] Data visualization uses only Soft series colors.
- [ ] Background halftone uses 28px spacing, 1.5px dots, 12% opacity.
- [ ] Only Goorm Sans is used. No other font families.
- [ ] Text is secondary. Visual data dominates the viewport.
- [ ] At least two different hetero border styles exist in the same view.

---

*BLP Paper — 난해하고 유동적이며 몽환적인 논문의 시각화*
