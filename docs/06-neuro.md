# `neuro_design_pattern.css`

**Philosophie :** extrusion douce depuis le fond — les ombres simulent une matière physique. Principe important : une ombre neumorphique **n'est pas grise par défaut**. Ici, les deux ombres (claire et sombre) sont calculées à partir de `--nm-bg` elle-même (qui dérive de la palette) : toute la texture change de teinte avec la marque, pas seulement l'accent — c'était le principal défaut corrigé sur ce pattern.

```html
<body data-style="neuro" data-mode="light">
```


## 1. Palette d'entrée

| Variable | Rôle | Défaut |
|---|---|---|
| `--palette-primary` | Accents, focus | `#4C6EF5` |
| `--palette-secondary` | Deuxième signal | `#F76707` |
| `--palette-neutral` | Référence de la matière | `#8892A6` |
| `--palette-success/danger/warning/info` | Statuts | `#22C55E` / `#EF4444` / `#F59E0B` / `#0EA5E9` |
| `--font-display` | Typo identitaire | `"Poppins", "Segoe UI", var(--font-sans)` |

Tokens calculés par mode (pas dans la palette, dans `[data-mode]`) :
- `--nm-bg` : couleur de la "matière", légèrement teintée par `--palette-primary`
- `--nm-shadow-dark` / `--nm-shadow-light` : **dérivées de `--nm-bg`** (mix vers noir / vers blanc), jamais du gris-bleu fixe
- `--nm-text`, `--nm-text-strong`, `--nm-brand`, `--nm-accent`


## 2. Classes de composants

### Surface — les deux états de relief
| Classe | Rendu |
|---|---|
| `.surface` | Extrudée : `box-shadow` claire en haut-gauche + sombre en bas-droite |
| `.surface-inset` | **Propre à Neuro** — creusée : mêmes ombres en `inset` |

```html
<div class="surface p-lg">Relief sortant</div>
<div class="surface-inset p-lg">Relief creusé</div>
```

### Texte
`.text-heading` (semibold) · `.text-body` · `.text-label` · `.text-primary` / `.text-muted` (opacité réduite) · `.text-brand` / `.text-accent` · `.text-success` / `-danger` / `-warning` / `-info`.

### Boutons
| Classe | Rendu |
|---|---|
| `.btn` | Extrudé par défaut (mêmes tokens `--nm-shadow-*` que `.surface`) |
| `.btn:active` / `.btn-inset` | **Propre à Neuro** — s'enfonce (ombres en `inset`) au clic |
| `.btn-primary` | Fond `--nm-brand` plein |
| `.btn-secondary` | Même relief que `.btn` de base, sans couleur de marque |
| `.btn-accent` | Fond `--nm-accent` |
| `.btn-ghost` | Plat, sans relief |
| `.btn-danger` | Fond `--palette-danger` |

```html
<button class="btn btn-primary">Valider</button>
<button class="btn btn-inset">Actif</button>
```

### Champ
`.input` : relief **creusé** en permanence (`inset` — cohérent avec l'idée qu'on "entre" du texte dans la matière), anneau `--nm-brand` au focus.

### Icônes, badges
`.icon-brand`/`.icon-accent`. `.badge` : fond `--nm-bg` + relief léger, texte coloré par statut (`primary/secondary/success/danger/warning/info`).

### Modale, overlay, divider
`.modal` : très grand relief extrudé (20px). `.overlay` : fond assombri dérivé de `--nm-shadow-dark` (pas un noir générique) + léger flou. `.divider` : pas de couleur pleine, juste un filet lumière/ombre.

### Pas d'utilitaires `.shadow-*` — choix assumé
Contrairement à Material, ce fichier ne fournit **volontairement pas** de `.shadow-sm/md/lg` génériques : en neumorphisme l'ombre n'a de sens que par paire et collée à `--nm-bg`. L'appliquer isolément sur un fond arbitraire casserait l'illusion de matière. Utilise `.surface`/`.surface-inset` à la place.


## 3. Ce qui est propre à Neuro (non présent ailleurs)

`.surface-inset`, `.btn-inset`. Voir `00-index.md` §3.2.

## 4. Écart corrigé lors de cette passe

`.btn-secondary` manquait (oubli). Ajouté avec le même relief que `.btn` de base, sans teinte de marque — pour rester cohérent avec le rôle "secondaire" du socle commun.
