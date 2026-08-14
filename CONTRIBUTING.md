# Contributing to Jangsang

Thank you for your interest in contributing! Jangsang is a small, opinionated framework — contributions that respect its core philosophy are most likely to be merged.

---

## Core philosophy (read this first)

Jangsang has **two layers that must never mix**:

| Layer | File | Responsible for |
|---|---|---|
| Layout | `src/layout.css` | Structure, spacing, typography, flex, grid |
| Visual | `src/skins/*.css` | Colors, shadows, borders, backgrounds |

A skin file **must not** contain any layout property (`width`, `height`, `padding`, `margin`, `display`, `flex-*`, `grid-*`, `font-size`, `font-family`).  
`layout.css` **must not** contain any color or visual rendering.

PRs that mix these two layers will not be merged.

---

## Ways to contribute

### 1. Submit a new skin
The most welcome type of contribution. See `docs/08-create-a-skin.md` for the full guide.

Checklist before opening a PR:
- [ ] File is in `src/skins/your-skin-name.css`
- [ ] All selectors are scoped to `[data-style="your-skin-name"]`
- [ ] Light mode and dark mode are both handled
- [ ] No layout properties in the skin file
- [ ] A doc file exists at `docs/0X-your-skin-name.md` (follow the pattern of existing docs)
- [ ] A screenshot or live demo (CodePen, etc.) is included in the PR description

### 2. Fix a bug in an existing skin
Open an issue first if you're unsure whether it's intentional. For clear visual bugs, a PR directly is fine.

### 3. Improve layout.css
Layout changes affect every project using Jangsang, so these are reviewed carefully. Open an issue before writing code to discuss the change.

### 4. Improve documentation
Always welcome — typos, clarifications, missing examples.

---

## PR process

1. Fork the repo and create a branch: `git checkout -b skin/your-skin-name` or `fix/what-you-fixed`
2. Make your changes
3. Open a Pull Request with a clear description of what and why
4. A maintainer will review and leave feedback

---

## Code style

- CSS only — no preprocessors, no build step required
- Use `color-mix(in srgb, …)` for palette derivation (already used throughout)
- Use existing `--radius-*`, `--duration-*`, `--ease-*`, `--z-*` tokens from `layout.css`
- Comments in English

---

## Questions?

Open an issue tagged `question`. We're happy to help you get started.
