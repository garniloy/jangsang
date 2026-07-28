# `glow_design_pattern.css`

**Philosophie :** canvas sombre, accents néon, ombres "bloom" qui rayonnent depuis la couleur de marque. Rien n'est éclairé par une lumière neutre : toute lueur (`--glow-*`) est teintée par la palette, jamais grise.

```html
<body data-style="glow" data-mode="dark">   <!-- glow est pensé dark-first, mais light existe -->
```


## 1. Palette d'entrée

| Variable | Rôle | Défaut |
|---|---|---|
| `--palette-primary` | Halo principal | `#A855F7` (violet) |
| `--palette-secondary` | Deuxième halo | `#22D3EE` (cyan) |
| `--palette-neutral` | Référence gris/texte | `#7C7A99` |
| `--palette-success/danger/warning/info` | Statuts (chacun garde son propre halo) | `#22C55E` / `#EF4444` / `#F59E0B` / `#22D3EE` |
| `--font-display` | Typo identitaire | `"Space Grotesk", "Segoe UI", var(--font-sans)` |

Tokens de halo dérivés à 100% de `--primary-*`/`--secondary-*` : `--glow-strong` (65% opacité), `--glow-mid` (35%), `--glow-soft` (18%), `--glow-accent`, `--glow-border`.


## 2. Classes de composants

### Surface
`.surface` : fond sombre teinté primary, bordure `--glow-border`, `box-shadow` double (liseré + halo `--glow-mid`). Au survol, le halo s'intensifie (`--glow-strong`).

```html
<div class="surface p-lg">Panneau qui rayonne au survol</div>
```

### Texte
| Classe | Rendu |
|---|---|
| `.text-heading` | Blanc, `text-shadow` halo (violet en dark, sans ombre en light) |
| `.text-body` | Gris-violet clair, opacité réduite |
| `.text-label` | Majuscules, `--primary-300`, léger halo |
| `.text-glow` | **Propre à Glow** — texte qui rayonne fort (`--primary-400` + `text-shadow` prononcé) |
| `.text-primary` / `.text-muted` | Rôles neutres standard du socle commun |
| `.text-brand` / `.text-accent` | `--primary-400` / `--secondary-400` |
| `.text-success` / `-danger` / `-warning` / `-info` | Teintes 300 (claires, lisibles sur fond sombre) |

```html
<h2 class="text-heading">Titre</h2>
<p class="text-glow">Ce mot rayonne</p>
```

### Boutons
`.btn-primary` (fond `--primary-600`, double halo, bordure claire) · `.btn-secondary` (transparent, bordure + halo intérieur) · `.btn-accent` (fond `--secondary-600`) · `.btn-ghost` (transparent, texte qui s'illumine au survol) · `.btn-danger`.

```html
<button class="btn btn-primary">Lancer</button>
```

### Champ
`.input` : fond sombre translucide, bordure `--glow-border`. Au focus : anneau `--primary-500` + halo + léger halo intérieur.

### Icônes, badges
`.icon-brand`/`.icon-accent` avec `filter: drop-shadow(halo)`. `.badge-*` : fond très doux + bordure teintée + `box-shadow` halo léger — chaque statut garde sa propre lueur (`badge-primary`, `-secondary`, `-success`, `-danger`, `-warning`, `-info`, `-neutral`).

### Modale, overlay, divider
`.modal` : fond quasi-noir teinté, bordure violette, halo large + ombre portée classique pour la profondeur. `.overlay` : noir 75% + `backdrop-filter: blur`. `.divider` : dégradé transparent → halo → transparent (pas un trait plein).

### Perf & accessibilité (spécifique à ce pattern)
Le halo est coûteux en rendu. Le fichier réduit automatiquement l'intensité des ombres sur mobile (`@media max-width: 47.9375rem`) et désactive la transition du `.surface` sous `prefers-reduced-motion: reduce` — **aucune règle de layout n'est touchée**, seulement l'intensité de l'effet.


## 3. Ce qui est propre à Glow (non présent ailleurs)

`.text-glow`. Voir `00-index.md` §3.2.

## 4. Écarts corrigés lors de cette passe

`.text-primary`, `.text-muted`, `.text-info` et `.badge-info` manquaient (oubli, pas un choix). Ajoutés + ladder `--info-300/500` complétée dans la palette pour que `.text-info`/`.badge-info` dérivent correctement de `--palette-info`.
