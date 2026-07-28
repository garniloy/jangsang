# Creating a custom skin for Jangsang

A Jangsang skin is a single CSS file. It defines only the **visual rendering** of components — colors, shadows, borders, backgrounds — for a specific aesthetic. Layout and spacing come from `layout.css` and are never touched by a skin.

---

## The two rules a skin must follow

1. **Scope everything to your `data-style` attribute.** Every selector starts with `[data-style="your-skin-name"]`. Nothing leaks out.
2. **Only use visual properties.** No `width`, `height`, `padding`, `margin`, `display`, `flex-*`, `grid-*`, `font-size`, or `font-family`. Those belong to `layout.css`.

Allowed properties: `background`, `color`, `border`, `border-radius`, `box-shadow`, `outline`, `filter`, `backdrop-filter`, `text-shadow`, `opacity` (for state), `transition` (for color/shadow/border only), `cursor`.

---

## Step 1 — Copy the template

Copy `src/skins/_skin-template.css` and rename it to your skin name (e.g. `retro.css`).

```bash
cp src/skins/_skin-template.css src/skins/retro.css
```

---

## Step 2 — Define your palette

At the top of your file, declare your 3 seed variables inside your scoped selector. Everything else will be derived from these using `color-mix()`.

```css
[data-style="retro"] {
  --palette-primary:   #D97706; /* your brand color         */
  --palette-secondary: #059669; /* your accent color        */
  --palette-neutral:   #57534E; /* reference for all grays  */
}
```

You can add more local variables for values you'll reuse inside the skin (glow colors, glass tints, shadow tones, etc.).

```css
[data-style="retro"] {
  --palette-primary:   #D97706;
  --palette-secondary: #059669;
  --palette-neutral:   #57534E;

  /* local helpers */
  --retro-shadow-dark:  rgba(40, 30, 10, 0.5);
  --retro-shadow-light: rgba(255, 240, 200, 0.7);
  --retro-border:       color-mix(in srgb, var(--palette-primary) 35%, transparent);
}
```

---

## Step 3 — Handle dark mode

Add a `[data-style="retro"][data-mode="dark"]` block right after the base block. Override only what changes between light and dark.

```css
[data-style="retro"][data-mode="dark"] {
  --retro-shadow-dark:  rgba(10, 8, 3, 0.7);
  --retro-shadow-light: rgba(60, 45, 20, 0.4);
}
```

---

## Step 4 — Style the components

Work through each component in this order (same order as the template):

| Component     | Selector             | Key properties                                  |
|---------------|----------------------|-------------------------------------------------|
| Page bg       | `[data-style]`       | `background`                                    |
| `.surface`    | `.surface`           | `background`, `border`, `border-radius`, `box-shadow` |
| Text roles    | `.text-heading` etc. | `color`, `text-shadow` (optional)               |
| `.btn-*`      | all button variants  | `background`, `color`, `border`, `box-shadow`   |
| `.input`      | `.input`             | `background`, `border`, `color`                 |
| Icons         | `.icon`, `.icon-*`   | `color`, `filter`                               |
| Badges        | `.badge-*`           | `background`, `color`, `border`                 |
| `.modal`      | `.modal`             | `background`, `border`, `box-shadow`            |
| `.overlay`    | `.overlay`           | `background`, `backdrop-filter`                 |
| `.divider`    | `.divider` etc.      | `background`, `box-shadow`                      |
| Scrollbar     | `::-webkit-scrollbar*` | `background`                                  |

---

## Step 5 — Use it

```html
<link rel="stylesheet" href="layout.css">
<link rel="stylesheet" href="retro.css">

<body data-style="retro" data-mode="light">
  ...
  <section data-mode="dark">...</section>
</body>
```

`data-mode` can be set on any ancestor — the skin adapts automatically.

---

## Step 6 — Submit it (optional)

If you'd like to contribute your skin to the official Jangsang collection:

1. Fork the repo on GitHub.
2. Place your skin in `src/skins/your-skin-name.css`.
3. Add a matching doc file in `docs/` following the pattern of `docs/02-flat.md`.
4. Open a Pull Request with a short description and a screenshot or CodePen demo.

See `CONTRIBUTING.md` for the full contribution guide.

---

## Template file

```css
/* ============================================================
   JANGSANG — Skin template
   Replace "your-skin-name" everywhere with your skin's name.
   Delete this comment block before submitting.
   ============================================================ */

/* ----------------------------------------------------------
   PALETTE — 3 seed variables, everything derives from these
---------------------------------------------------------- */
[data-style="your-skin-name"] {
  --palette-primary:   #3B82F6;
  --palette-secondary: #10B981;
  --palette-neutral:   #64748B;
}

[data-style="your-skin-name"][data-mode="dark"] {
  /* override only what changes in dark mode */
}

/* ----------------------------------------------------------
   PAGE BACKGROUND
---------------------------------------------------------- */
[data-style="your-skin-name"][data-mode="light"] { background: /* … */; }
[data-style="your-skin-name"][data-mode="dark"]  { background: /* … */; }

/* ----------------------------------------------------------
   SURFACE
---------------------------------------------------------- */
[data-style="your-skin-name"] .surface {
  background:    /* … */;
  border:        /* … */;
  border-radius: /* use a --radius-* token */;
  box-shadow:    /* … */;
}

/* ----------------------------------------------------------
   TEXT
---------------------------------------------------------- */
[data-style="your-skin-name"] .text-heading { color: /* … */; }
[data-style="your-skin-name"] .text-body    { color: /* … */; }
[data-style="your-skin-name"] .text-label   { color: /* … */; text-transform: uppercase; }

/* ----------------------------------------------------------
   BUTTONS
---------------------------------------------------------- */
[data-style="your-skin-name"] .btn            { transition: /* colors/shadow only */; }
[data-style="your-skin-name"] .btn-primary    { background: /* … */; color: /* … */; }
[data-style="your-skin-name"] .btn-primary:hover { background: /* … */; }
[data-style="your-skin-name"] .btn-secondary  { background: /* … */; color: /* … */; border: /* … */; }
[data-style="your-skin-name"] .btn-outline    { background: transparent; color: /* … */; border: /* … */; }
[data-style="your-skin-name"] .btn-ghost      { background: transparent; color: /* … */; }

/* ----------------------------------------------------------
   INPUT
---------------------------------------------------------- */
[data-style="your-skin-name"] .input              { background: /* … */; border: /* … */; color: /* … */; border-radius: /* … */; }
[data-style="your-skin-name"] .input::placeholder { color: /* … */; }
[data-style="your-skin-name"] .input:focus        { outline: none; border-color: /* … */; box-shadow: /* … */; }

/* ----------------------------------------------------------
   ICONS
---------------------------------------------------------- */
[data-style="your-skin-name"] .icon        { color: /* … */; }
[data-style="your-skin-name"] .icon-brand  { color: /* … */; }
[data-style="your-skin-name"] .icon-accent { color: /* … */; }

/* ----------------------------------------------------------
   BADGES
---------------------------------------------------------- */
[data-style="your-skin-name"] .badge           { border-radius: var(--radius-full); }
[data-style="your-skin-name"] .badge-primary   { background: /* … */; color: /* … */; }
[data-style="your-skin-name"] .badge-secondary { background: /* … */; color: /* … */; }
[data-style="your-skin-name"] .badge-success   { background: /* … */; color: /* … */; }
[data-style="your-skin-name"] .badge-danger    { background: /* … */; color: /* … */; }
[data-style="your-skin-name"] .badge-warning   { background: /* … */; color: /* … */; }
[data-style="your-skin-name"] .badge-info      { background: /* … */; color: /* … */; }
[data-style="your-skin-name"] .badge-neutral   { background: /* … */; color: /* … */; }

/* ----------------------------------------------------------
   MODAL & OVERLAY
---------------------------------------------------------- */
[data-style="your-skin-name"] .modal   { background: /* … */; border: /* … */; border-radius: /* … */; box-shadow: /* … */; }
[data-style="your-skin-name"] .overlay { position: fixed; inset: 0; background: /* … */; z-index: var(--z-overlay); }

/* ----------------------------------------------------------
   DIVIDERS
---------------------------------------------------------- */
[data-style="your-skin-name"] .divider          { height: 1px; background: /* … */; }
[data-style="your-skin-name"] .divider-vertical { width: 1px;  background: /* … */; }

/* ----------------------------------------------------------
   SCROLLBAR
---------------------------------------------------------- */
[data-style="your-skin-name"] ::-webkit-scrollbar       { width: 6px; }
[data-style="your-skin-name"] ::-webkit-scrollbar-track { background: /* … */; }
[data-style="your-skin-name"] ::-webkit-scrollbar-thumb { background: /* … */; border-radius: var(--radius-full); }
```
