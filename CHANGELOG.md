# Changelog

All notable changes to Jangsang are documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).
Jangsang adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.0.1] — 2025-07-27

### Changed
- `package.json`: removed `main` field (not relevant for CSS-only packages)
- `package.json`: added `sideEffects` to prevent bundlers from dropping CSS imports during tree-shaking
- `package.json`: added `"."` entry in `exports` — allows `@import "jangsang"` directly
- `package.json`: bumped version to 1.0.1

### Added
- `CHANGELOG.md` — this file
- `CODE_OF_CONDUCT.md` — contributor code of conduct
- `examples/` — minimal HTML usage examples for each skin

---

## [1.0.0] — 2025-07-27

### Added
- Initial public release
- `src/layout.css` — reset, flex, grid, spacing, typography, z-index, transitions
- `src/skins/flat.css` — flat design skin
- `src/skins/material.css` — material design skin
- `src/skins/glow.css` — neon/glow skin
- `src/skins/glass.css` — glassmorphism skin
- `src/skins/neuro.css` — neumorphism skin
- `src/skins/all.css` — all skins bundled in one file
- `src/skins/_skin-template.css` — starter template for custom skins
- `docs/` — full documentation for each skin and the layout layer
- `branding/` — SVG logo, favicon, brand guidelines
- `README.md`, `LICENSE`, `CONTRIBUTING.md`
