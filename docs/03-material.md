# `material_design_pattern.css`

**Philosophie :** surfaces tonales (teintées par la marque à mesure qu'elles s'élèvent) + système d'élévation par ombres **neutres** superposées (physiquement, une ombre portée n'a pas la couleur de l'objet — c'est volontairement la seule ombre du framework qui ne dérive pas de la palette). Formes pleines (boutons pilule), contrastes forts entre styles de bouton.

```html
<body data-style="material" data-mode="light">
```


## 1. Palette d'entrée

| Variable | Rôle | Défaut |
|---|---|---|
| `--palette-primary` | Marque | `#6750A4` (violet) |
| `--palette-secondary` | Accent | `#00897B` (teal) |
| `--palette-neutral` | Référence des gris | `#79747E` |
| `--palette-success/danger/warning/info` | Statuts | `#22C55E` / `#EF4444` / `#F59E0B` / `#0EA5E9` |
| `--font-display` | Typo identitaire | `"Roboto", "Google Sans", var(--font-sans)` |

Token supplémentaire propre à Material : `--on-warning` (texte sombre calculé pour rester lisible sur un badge/bouton ambre, qui reste clair même en version "700").

Tokens d'élévation calculés par mode (pas dans la palette, dans le bloc `[data-mode]`) :
`--md-tint` (glacis de teinte posé sur chaque surface, dérivé de primary), `--md-elev-1/2/3` (paliers d'ombre neutre, plus prononcés en dark qu'en light).


## 2. Classes de composants

### Surface — le cœur du système Material
| Classe | Rendu |
|---|---|
| `.surface` | Fond carte + glacis `--md-tint` + `--md-elev-1` |
| `.surface-elevated` | Idem + `--md-elev-2` (plus haute) |
| `.surface-flat` | Idem sans ombre, bordure à la place (élévation "0") |

```html
<div class="grid grid-3 gap-lg">
  <div class="surface-flat p-lg">Niveau 0</div>
  <div class="surface p-lg">Niveau 1</div>
  <div class="surface-elevated p-lg">Niveau 2</div>
</div>
```

### Texte
`.text-heading` (medium weight, tracking serré) · `.text-body` (opacité réduite) · `.text-label` (majuscules, opacité réduite) · `.text-primary` / `.text-secondary` / `.text-muted` · `.text-brand` / `.text-accent` · `.text-success` / `-danger` / `-warning` / `-info`.

### Boutons — 4 registres distincts
| Classe | Rendu | Usage |
|---|---|---|
| `.btn-primary` | Fond plein `--primary-500`, `--md-elev-1` → `2` au survol | Action principale |
| `.btn-secondary` | Transparent, bordure `--primary-500` | Action secondaire visible |
| `.btn-tonal` | Fond teinté doux (`color-mix` primary + fond) | Action secondaire discrète mais colorée |
| `.btn-ghost` | Transparent, aucune bordure | Action tertiaire |
| `.btn-accent` | Fond `--secondary-500` | CTA alternatif |
| `.btn-danger` | Fond `--danger-500` | Action destructrice |

```html
<div class="row gap-sm">
  <button class="btn btn-primary">Contained</button>
  <button class="btn btn-tonal">Tonal</button>
  <button class="btn btn-secondary">Outlined</button>
  <button class="btn btn-ghost">Text</button>
</div>
```

### Champ — style "filled" Material
`.input` : pas de bordure complète, seulement un **soulignement** 2px `--gray-300` qui devient `--primary-500` au focus. Fond légèrement teinté (`--bg-surface`).

### Icônes & Badges
`.icon-brand` / `.icon-accent`. `.badge-*` sont **pleins et saturés** (contrairement au badge "doux" de Flat) — `background: var(--primary-500); color:#fff`, sauf `.badge-warning` qui utilise `--on-warning` (texte sombre) pour rester lisible.

```html
<span class="badge badge-primary">Nouveau</span>
<span class="badge badge-warning">Attention</span>
```

### Modale, overlay, divider
`.modal` reprend le glacis `--md-tint` + `--md-elev-3`. `.overlay` fond noir 55%. `.divider` trait `--gray-300`.

### Ombres utilitaires (propres à Material)
`.shadow-sm` (`--md-elev-1`) · `.shadow-md` (`--md-elev-2`) · `.shadow-lg` (`--md-elev-3`) · `.shadow-none`.

```html
<div class="p-lg shadow-md rounded-lg">Carte flottante manuelle</div>
```


## 3. Ce qui est propre à Material (non présent ailleurs)

`.surface-elevated`, `.surface-flat`, `.btn-tonal`, `.badge-neutral`, `.bg`, `.bg-elevated`, `.shadow-sm/md/lg/none`. Le système d'élévation par ombre est la spécificité structurelle de ce pattern — voir `00-index.md` §3.2.
