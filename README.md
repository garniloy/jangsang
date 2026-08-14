<p align="center">
  <img src="branding/logo-on-dark.svg" alt="Jangsang logo" width="96" height="96"/>
</p>

<h1 align="center">Jangsang</h1>

<p align="center"><strong>Build once. Reskin forever.</strong></p>

<p align="center">
  <a href="https://www.npmjs.com/package/jangsang"><img src="https://img.shields.io/npm/v/jangsang?color=FF6B00&labelColor=111" alt="npm version"></a>
  <a href="https://github.com/garniloy/jangsang/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-FF6B00?labelColor=111" alt="MIT license"></a>
  <img src="https://img.shields.io/badge/CSS_only-no_JS-FF6B00?labelColor=111" alt="CSS only">
</p>

---

Jangsang separates structure from appearance. Your layout never changes when you swap a skin. Your skin never breaks when you change layout. Switch from glassmorphism to neumorphism to flat design by changing a single HTML attribute.

---

## Install

**npm**
```bash
npm install jangsang
```

**CDN** — no install needed, paste into your `<head>`:
```html
<!-- Layout (always required) -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/garniloy/jangsang@v1.0.0/src/layout.css">

<!-- Pick ONE skin -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/garniloy/jangsang@v1.0.0/src/skins/glass.css">
```

---

## How it works

Jangsang has two layers:

| Layer | File | Does what |
|---|---|---|
| **Layout** | `layout.css` | Reset, flex, grid, spacing, typography scale, z-index, transitions |
| **Skin** | `skins/*.css` | Colors, shadows, borders, backgrounds — the visual identity |

You load `layout.css` once. Then you pick a skin. That's it.

```html
<link rel="stylesheet" href="layout.css">
<link rel="stylesheet" href="skins/glass.css">

<body data-style="glass" data-mode="dark">
  <div class="surface">...</div>
</body>
```

Switch skin by changing `data-style`. Switch mode with `data-mode`. Both can be set on any element — they scope downward automatically.

```html
<!-- Mix skins on a single page -->
<body data-style="flat" data-mode="light">
  <section data-style="glass" data-mode="dark">
    Dark glass section inside a light flat page.
  </section>
</body>
```

---

## Available skins

| Skin | `data-style` | Description |
|---|---|---|
| Flat | `flat` | Zero depth, pure color, sharp edges |
| Material | `material` | Tonal fills, elevation shadows, contained variants |
| Glow | `glow` | Dark canvas, neon accents, bloom shadows |
| Glass | `glass` | Frosted glass layers over a vivid gradient background |
| Neuro | `neuro` | Soft extrusion from the surface — tactile, monochrome |

---

## Reskin with 2 variables

Every skin derives its entire color system from palette variables. To apply your brand colors, override them **after** loading the skin — in your own CSS file or in a `<style>` tag:

```css
/* Override on the skin selector, after loading the skin */
[data-style="glass"] {
  --palette-primary:   #FF6B00; /* your brand color  */
  --palette-secondary: #8B5CF6; /* your accent color */
}
```

That's all. Every component in the skin — buttons, badges, inputs, glows, focus rings, gradients — updates automatically via `color-mix()`. No rebuild required.

Each skin exposes these variables:

| Variable | Role |
|---|---|
| `--palette-primary` | Brand color — CTAs, links, focus rings |
| `--palette-secondary` | Accent — secondary signals, badges |
| `--palette-neutral` | Reference for all grays and muted tones |
| `--palette-success` | Success states |
| `--palette-danger` | Error / destructive states |
| `--palette-warning` | Warning states |
| `--palette-info` | Informational states |

You only need to override `--palette-primary` and `--palette-secondary` for a full rebrand. The rest default to sensible values.

---

## Usage from npm

```bash
npm install jangsang
```

Then in your CSS entry point (works with Vite, Webpack, Next.js, Astro, Svelte…):

```css
@import 'jangsang';            /* layout layer */
@import 'jangsang/skin/glow';  /* pick a skin  */
```

Or in JavaScript / TypeScript (React, Vue, Next.js…):

```js
import 'jangsang';
import 'jangsang/skin/glass';
```

> **Bundler note:** Jangsang declares `sideEffects: ["*.css"]` in its `package.json`. This tells Webpack and Vite not to drop CSS imports during tree-shaking.

---

## HTML component classes

All components are plain HTML with utility classes. No JavaScript required for static rendering.

```html
<!-- Surface (card) -->
<div class="surface">...</div>

<!-- Buttons -->
<button class="btn btn-primary">Primary</button>
<button class="btn btn-secondary">Secondary</button>
<button class="btn btn-outline">Outline</button>
<button class="btn btn-ghost">Ghost</button>

<!-- Input -->
<input class="input" type="text" placeholder="Type here…">

<!-- Badges -->
<span class="badge badge-primary">New</span>
<span class="badge badge-success">Active</span>
<span class="badge badge-danger">Error</span>

<!-- Dividers -->
<!-- Pair a size class with the visual class -->
<hr class="divider h-divider-l">          <!-- 70% wide horizontal line -->
<div class="divider-vertical v-divider-m"> <!-- 50% tall vertical line  -->

<!-- Modal -->
<div class="overlay">
  <div class="modal">...</div>
</div>
```

### Layout helpers (from layout.css)

```html
<!-- Flex -->
<div class="row align-center justify-between gap-md">...</div>
<div class="col gap-lg">...</div>

<!-- Grid -->
<div class="grid-3 gap-lg">...</div>
<div class="grid-auto-md">...</div>

<!-- Typography -->
<h1 class="text-2xl weight-bold">Title</h1>
<p class="text-sm text-muted">Subtitle</p>
```

---

## Dark mode

Set `data-mode="dark"` on any ancestor. The skin adapts automatically.

```html
<body data-style="flat" data-mode="light">
  <!-- light by default -->
  <aside data-mode="dark">
    <!-- this section is dark -->
  </aside>
</body>
```

Toggle it with JavaScript:
```js
document.body.dataset.mode = 'dark';
```

---

## Create your own skin

Copy the template, fill in the blanks, use it immediately:

```bash
cp node_modules/jangsang/src/skins/_skin-template.css my-skin.css
```

Then follow `docs/08-create-a-skin.md` — it walks through every component with examples.

Want to share your skin? Open a Pull Request. See `CONTRIBUTING.md`.

---

## File reference

```
jangsang/
├── src/
│   ├── layout.css          ← always load this first
│   └── skins/
│       ├── flat.css
│       ├── material.css
│       ├── glow.css
│       ├── glass.css
│       ├── neuro.css
│       ├── all.css         ← bundle: all 5 skins in one file
│       └── _skin-template.css
├── docs/
│   ├── 00-index.md
│   ├── 01-layout.md
│   ├── 02-flat.md … 06-neuro.md
│   ├── 07-all.md
│   └── 08-create-a-skin.md
├── README.md
├── CONTRIBUTING.md
└── LICENSE
```

---

## License

MIT — free to use, modify, and distribute. See `LICENSE`.
