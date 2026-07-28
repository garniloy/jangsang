# `glass_design_pattern.css`

**Philosophie :** couches de verre dépoli sur un fond vivant en dégradé. Important : le "verre" **n'est pas un blanc neutre universel** — sa teinte de fond ET sa translucidité dérivent toutes deux de la palette de marque. C'est le point corrigé lors de la refonte : avant, deux projets avec des palettes différentes produisaient un glassmorphism visuellement identique.

```html
<body data-style="glass" data-mode="light">
```


## 1. Palette d'entrée

| Variable | Rôle | Défaut |
|---|---|---|
| `--palette-primary` | Dégradé de fond + teinte du verre | `#6366F1` (indigo) |
| `--palette-secondary` | Deuxième teinte du dégradé | `#14B8A6` (teal) |
| `--palette-neutral` | Référence gris/texte | `#64748B` |
| `--palette-success/danger/warning/info` | Statuts | `#22C55E` / `#EF4444` / `#F59E0B` / `#0EA5E9` |
| `--font-display` | Typo identitaire | `"SF Pro Display", -apple-system, var(--font-sans)` |

Le fond `[data-mode]` est un **dégradé** construit à partir de `--primary-*`/`--secondary-*` (pas une image). Le "verre" lui-même est un jeu de tokens calculés par mode : `--glass-bg` (fond translucide **teinté** — mix imbriqué de primary et blanc/transparent, pas du blanc pur), `--glass-bg-hover`, `--glass-border`, `--glass-blur`, `--glass-text`, `--glass-text-2`, `--glass-shadow`.


## 2. Classes de composants

### Surface
`.surface` : `background: var(--glass-bg)` + `backdrop-filter: blur(var(--glass-blur)) saturate(160%)` + bordure `--glass-border` + `--glass-shadow` (ombre douce + liseré lumineux interne). `:hover` passe à `--glass-bg-hover`.

```html
<div class="surface p-lg">Panneau de verre</div>
```
> `backdrop-filter` n'a d'effet que si quelque chose (le dégradé de fond, une image) est visible **derrière** l'élément.

### Texte
`.text-heading` (blanc/quasi-noir selon mode + gras) · `.text-body` / `.text-primary` / `.text-muted` (opacités du même `--glass-text`) · `.text-label` · `.text-brand` / `.text-accent` · `.text-success` / `-danger` / `-warning` / `-info`.

### Boutons
| Classe | Rendu |
|---|---|
| `.btn-primary` | Verre lui-même (translucide), reste dans l'esprit glassmorphism |
| `.btn-brand` | **Propre à Glass** — fond plein teinté marque, non-translucide, pour un CTA très visible sur fond chargé |
| `.btn-secondary` | Transparent, juste une bordure de verre |
| `.btn-ghost` | Transparent, s'illumine légèrement au survol |
| `.btn-danger` | Fond `--palette-danger` translucide |

```html
<button class="btn btn-primary">Verre</button>
<button class="btn btn-brand">CTA plein</button>
```

### Champ
`.input` : même traitement que `.surface` (fond translucide + blur), bordure lumineuse au focus.

### Icônes, badges
`.icon-brand`/`.icon-accent`. `.badge-*` : fond de verre commun + bordure/texte teintés par statut (`primary/secondary/success/danger/warning/info`).

### Modale, overlay, divider
`.modal` : blur plus fort (`--blur-lg`) que `.surface`. `.overlay` : fond sombre teinté + blur. `.divider` : simple trait `--glass-border` (pas de dégradé comme Glow).

### Accessibilité & perf (spécifique à ce pattern)
`prefers-reduced-transparency: reduce` bascule `.surface`/`.modal`/`.input`/`.badge` sur un fond opaque clair sans `backdrop-filter`. Sur mobile, `--glass-blur` repasse à `--blur-sm` (moins coûteux). Aucune règle de layout n'est touchée.


## 3. Ce qui est propre à Glass (non présent ailleurs)

`.btn-brand`. Voir `00-index.md` §3.2.

## 4. Écart corrigé lors de cette passe

`.text-info` manquait. Ajouté (`color: var(--info-300)`), la variable existait déjà dans la palette dérivée mais n'était pas exposée en classe.
