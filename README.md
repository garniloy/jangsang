<p align="center">
  <img src="branding/logo-on-dark.svg" alt="Jangsang logo" width="150" height="150"/>
</p>

<h1 align="center">Jangsang</h1>

<p align="center"><strong>A two-layer CSS framework. One file for layout. One file for your visual skin.</strong></p>

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
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/garnilo/jangsang@v1.0.0/src/layout.css">

<!-- Pick ONE skin -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/garnilo/jangsang@v1.0.0/src/skins/glass.css">
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

## Reskin with 3 variables

Every skin derives its entire color system from 3 seed variables. To use your own brand colors, override them on `:root` (or on any scoped element) **after** loading the skin:

```css
/* your-palette.css */
[data-style="glass"] {
  --palette-primary:   #8B5CF6; /* violet */
  --palette-secondary: #EC4899; /* pink   */
  --palette-neutral:   #6B7280; /* gray   */
}
```

That's all. Every component in the skin — buttons, badges, inputs, glows, gradients — updates automatically.

---

## Usage from npm

```js
/* In your CSS / PostCSS / bundler entry */
@import 'jangsang/layout';
@import 'jangsang/skin/glow';
```

Or with a bundler that resolves `node_modules`:
```css
@import 'jangsang/src/layout.css';
@import 'jangsang/src/skins/glow.css';
```

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
