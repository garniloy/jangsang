# `reset_layout_framework.css`

**Responsabilité unique : où et combien.** Position, taille, espacement, structure typographique, mouvement, responsive. **Zéro couleur** — pas de palette, pas de `text-*`/`bg-*`/`border-*` de couleur, pas de dark mode, pas d'ombre colorée. Ce fichier doit toujours être chargé **avant** un fichier de design pattern.

```html
<link rel="stylesheet" href="reset_layout_framework.css">
<link rel="stylesheet" href="flat_design_pattern.css">
<body data-style="flat" data-mode="light">
```

Base : `html { font-size: 62.5% }` → `1rem = 10px`. Toutes les tailles du framework sont en `rem` pour rester proportionnelles au zoom navigateur.


## 1. Tokens — Spacing (`--sp-*`)

Échelle unique utilisée par tout le reset (gap, padding, margin, container).

| Token | Valeur | ≈ px |
|---|---|---|
| `--sp-3xs` | 0.2rem | 2px |
| `--sp-2xs` | 0.4rem | 4px |
| `--sp-xs` | 0.6rem | 6px |
| `--sp-sm` | 0.8rem | 8px |
| `--sp-md` | 1.2rem | 12px |
| `--sp-lg` | 1.6rem | 16px |
| `--sp-xl` | 2.4rem | 24px |
| `--sp-2xl` | 3.2rem | 32px |
| `--sp-3xl` | 4.8rem | 48px |
| `--sp-4xl` | 6.4rem | 64px |
| `--sp-5xl` | 9.6rem | 96px |

**Usage direct (rare, préfère les classes `.gap-*`/`.p-*`/`.m-*` de la section 6) :**
```css
.mon-composant-custom { padding: var(--sp-lg); }
```


## 2. Tokens — Typographie structurelle

Aucune couleur. `--font-display` n'est **volontairement pas défini ici** : c'est le rôle du pattern actif (fallback automatique vers `--font-sans` si aucun pattern ne le définit).

| Token | Valeur |
|---|---|
| `--font-sans` | `system-ui, -apple-system, "Segoe UI", Roboto, sans-serif` |
| `--font-mono` | `ui-monospace, "SFMono-Regular", Menlo, Consolas, monospace` |
| `--font-display` | *non défini ici* — fourni par le pattern actif |

`--fs-*` : échelle **fluide** (`clamp()`), s'interpole automatiquement entre mobile et desktop large sans media query à écrire.

| Token | clamp | ≈ mobile → desktop |
|---|---|---|
| `--fs-xs` | `clamp(1.15rem, 1.05rem + 0.25vw, 1.25rem)` | 12 → 13px |
| `--fs-sm` | `clamp(1.3rem, 1.2rem + 0.3vw, 1.45rem)` | 13 → 14.5px |
| `--fs-md` (base) | `clamp(1.5rem, 1.4rem + 0.35vw, 1.65rem)` | 15 → 16.5px |
| `--fs-lg` | `clamp(1.65rem, 1.5rem + 0.4vw, 1.85rem)` | 16.5 → 18.5px |
| `--fs-xl` | `clamp(1.8rem, 1.6rem + 0.5vw, 2.1rem)` | 18 → 21px |
| `--fs-2xl` | `clamp(2.1rem, 1.85rem + 0.65vw, 2.5rem)` | 21 → 25px |
| `--fs-3xl` | `clamp(2.6rem, 2.2rem + 1vw, 3.4rem)` | 26 → 34px |
| `--fs-4xl` | `clamp(3.1rem, 2.6rem + 1.4vw, 4.2rem)` | 31 → 42px |
| `--fs-5xl` | `clamp(3.6rem, 2.9rem + 1.8vw, 5rem)` | 36 → 50px |

`--weight-*` : `thin 100 · light 300 · normal 400 · medium 500 · semibold 600 · bold 700 · black 900`
`--leading-*` : `none 1 · tight 1.2 · snug 1.35 · normal 1.5 · relaxed 1.65 · loose 1.8`
`--tracking-*` : `tighter -0.02em · tight -0.01em · normal 0 · wide 0.02em · wider 0.04em · widest 0.08em`


## 3. Tokens — Radius / Blur

Dimensions pures. Chaque pattern décide quel palier appliquer à quel composant (ex. Flat utilise `--radius-md` sur les boutons, Material utilise `--radius-full`).

| Radius | Valeur | | Blur | Valeur |
|---|---|---|---|---|
| `--radius-none` | 0 | | `--blur-sm` | 4px |
| `--radius-xs` | 0.125rem | | `--blur-md` | 12px |
| `--radius-sm` | 0.25rem | | `--blur-lg` | 24px |
| `--radius-md` | 0.5rem | | `--blur-xl` | 48px |
| `--radius-lg` | 0.75rem | | | |
| `--radius-xl` | 1rem | | | |
| `--radius-2xl` | 1.5rem | | | |
| `--radius-3xl` | 2rem | | | |
| `--radius-full` | 9999px | | | |


## 4. Tokens — Z-index

Pile sémantique fixe — ne jamais utiliser de nombre magique ailleurs dans le projet.

| Token | Valeur | Usage typique |
|---|---|---|
| `--z-base` | 0 | Contenu normal |
| `--z-raised` | 10 | Carte survolée, élément en avant-plan léger |
| `--z-dropdown` | 100 | Menu déroulant |
| `--z-sticky` | 200 | Header collant |
| `--z-modal` | 300 | Contenu d'une modale |
| `--z-overlay` | 400 | Fond assombri derrière une modale |
| `--z-toast` | 500 | Notification |
| `--z-tooltip` | 600 | Infobulle |


## 5. Tokens — Motion

| Easing | Valeur | | Durée | Valeur |
|---|---|---|---|---|
| `--ease-out` | `cubic-bezier(.22,1,.36,1)` | | `--duration-instant` | 80ms |
| `--ease-in` | `cubic-bezier(.4,0,1,1)` | | `--duration-fast` | 120ms |
| `--ease-inout` | `cubic-bezier(.45,0,.55,1)` | | `--duration-normal` | 220ms |
| `--ease-linear` | `linear` | | `--duration-slow` | 380ms |
| `--ease-bounce` | `cubic-bezier(.34,1.56,.64,1)` | | | |

Raccourcis prêts à l'emploi : `--transition-all`, `--transition-colors`, `--transition-transform`, `--transition-shadow`, `--transition-opacity`.
```css
.mon-bouton { transition: var(--transition-colors); }
```


## 6. Classes utilitaires

### 6.1 Flexbox

| Classe | Effet |
|---|---|
| `.row` / `.row-rev` | `display:flex` en ligne / ligne inversée |
| `.col` / `.col-rev` | `display:flex` en colonne / colonne inversée |
| `.wrap` / `.nowrap` | `flex-wrap` |
| `.justify-start/center/end/between/around/evenly` | `justify-content` |
| `.align-start/center/end/stretch` | `align-items` |
| `.self-start/center/end/stretch` | `align-self` |
| `.flex-1` / `.flex-auto` / `.flex-none` | `flex` raccourci |
| `.grow` / `.grow-0` / `.shrink` / `.shrink-0` | `flex-grow` / `flex-shrink` |

**Exemple** — barre d'actions avec espace entre logo et boutons :
```html
<div class="row justify-between align-center gap-md">
  <span class="text-heading">Logo</span>
  <div class="row gap-sm">
    <button class="btn btn-ghost">Annuler</button>
    <button class="btn btn-primary">Valider</button>
  </div>
</div>
```

### 6.2 Grid

| Classe | Effet |
|---|---|
| `.grid` | `display:grid` |
| `.grid-2/3/4` | Grille à 2/3/4 colonnes égales |
| `.grid-auto-sm/md/lg` | `repeat(auto-fill, minmax(12/18/24rem, 1fr))` — colonnes qui s'adaptent seules |
| `.place-center` | `display:grid; place-items:center` |
| `.col-span-2/3/full` | Un item qui s'étend sur 2, 3 ou toutes les colonnes |

**Exemple** — grille de cartes qui s'auto-ajuste sans media query :
```html
<div class="grid grid-auto-md gap-lg">
  <div class="surface">...</div>
  <div class="surface">...</div>
  <div class="surface">...</div>
</div>
```

### 6.3 Container

| Classe | Effet |
|---|---|
| `.container` | Largeur max `--container-max` (120rem/1200px), centré, padding latéral qui grandit avec l'écran (`--sp-lg` → `--sp-xl` dès tablette → `--sp-2xl` dès desktop) |
| `.container-fluid` | Même padding responsive, mais pleine largeur (pas de `max-width`) |

```html
<div class="container">
  <!-- contenu centré, jamais plus large que 1200px -->
</div>
```

### 6.4 Position & Z-index

| Classe | Effet |
|---|---|
| `.relative` / `.absolute` / `.fixed` / `.sticky` | `position` |
| `.inset-0` | `inset:0` (colle aux 4 bords du parent positionné) |
| `.center-absolute` | Centrage absolu classique (`top/left:50%` + `translate(-50%,-50%)`) |
| `.z-base/raised/dropdown/sticky/modal/overlay/toast/tooltip` | Applique le z-index sémantique correspondant (section 4) |

```html
<div class="relative">
  <span class="badge badge-danger absolute" style="top:-6px; right:-6px;">3</span>
</div>
```

### 6.5 Sizing & aspect-ratio

| Classe | Effet |
|---|---|
| `.w-full` / `.w-screen` | `width: 100%` / `100vw` |
| `.h-full` / `.h-screen` / `.min-h-screen` | `height: 100%` / `100vh` / `min-height: 100dvh` |
| `.max-w-container` | `max-width: var(--container-max)` |
| `.aspect-square/video/portrait` | `aspect-ratio: 1/1`, `16/9`, `3/4` |
| `.h-divider-xs→xl` | Largeur d'un séparateur horizontal (15/30/50/70/90%) |
| `.v-divider-xs→xl` | Hauteur d'un séparateur vertical (15/30/50/70/90%) |

> Les `-divider-*` ne fixent que la **taille** du trait ; sa couleur/épaisseur visuelle vient de `.divider`/`.divider-vertical` dans le pattern actif.

```html
<img src="hero.jpg" class="aspect-video w-full">
<hr class="divider h-divider-sm mx-auto">  <!-- trait centré, 30% de large -->
```

### 6.6 Spacing utilitaires — gap / padding / margin

Toutes alignées sur l'échelle `--sp-*` (section 1).

| Famille | Classes disponibles |
|---|---|
| Gap | `.gap-3xs .gap-2xs .gap-xs .gap-sm .gap-md .gap-lg .gap-xl .gap-2xl .gap-3xl` |
| Padding (tous côtés) | `.p-0 .p-xs .p-sm .p-md .p-lg .p-xl .p-2xl` |
| Padding axe | `.px-xs/sm/md/lg/xl` (inline) et `.py-xs/sm/md/lg/xl` (block) |
| Padding un côté | `.pt-xs/sm/md/lg` (top), `.pb-xs/sm/md/lg` (bottom) |
| Margin (tous côtés) | `.m-0 .m-xs .m-sm .m-md .m-lg .m-xl` |
| Margin auto | `.mx-auto` (centrage horizontal), `.my-auto` |
| Margin axe | `.mx-xs/sm/md/lg` (inline), `.my-xs/sm/md/lg` (block) |
| Margin un côté | `.mt-xs/sm/md/lg/xl` (top), `.mb-xs/sm/md/lg/xl` (bottom) |

```html
<div class="col gap-md p-lg">
  <h2 class="mb-sm">Titre</h2>
  <p>Texte...</p>
</div>
```

### 6.7 Overflow

| Classe | Effet |
|---|---|
| `.ox-hidden` / `.ox-auto` | `overflow-x` |
| `.oy-hidden` / `.oy-auto` | `overflow-y` |
| `.o-hidden` | `overflow: hidden` (les deux axes) |

### 6.8 Typographie — utilitaires (sans couleur)

| Classe | Effet |
|---|---|
| `.font-display` / `.font-sans` / `.font-mono` | Applique la famille de police |
| `.fs-xs → .fs-4xl` | Applique une taille de la section 2 |
| `.fw-thin → .fw-black` | Applique une graisse |
| `.leading-none → .leading-loose` | Applique un interlignage |
| `.tracking-tighter → .tracking-widest` | Applique un espacement de lettres |
| `.ta-l`/`.text-left`, `.ta-r`/`.text-right`, `.ta-c`/`.text-center`, `.ta-j` | Alignement (alias historiques conservés) |
| `.tt-up`/`.uppercase`, `.tt-lo`/`.lowercase`, `.tt-ca`/`.capitalize` | Transformation de casse |
| `.underline` / `.overline` / `.line-through` | Décoration |
| `.truncate` | Coupe sur une ligne avec `…` |
| `.clamp-2` / `.clamp-3` | Coupe sur 2 ou 3 lignes avec `…` |

```html
<p class="fs-sm text-muted truncate" style="max-width: 24rem;">
  Un texte potentiellement très long qui sera coupé proprement…
</p>
```

### 6.9 Accessibilité

| Classe | Effet |
|---|---|
| `.sr-only` | Visible uniquement par les lecteurs d'écran (retiré visuellement sans `display:none`) |
| `.skip-link` | Lien "aller au contenu", caché hors-écran, réapparaît au focus clavier |

Le reset désactive aussi automatiquement les animations pour les utilisateurs `prefers-reduced-motion: reduce` — rien à faire côté composant.

```html
<a href="#main" class="skip-link">Aller au contenu principal</a>
<span class="sr-only">Menu de navigation</span>
```

### 6.10 Utilitaires divers

| Classe | Effet |
|---|---|
| `.hidden` | `display:none` |
| `.invisible` | `visibility:hidden` (garde la place) |
| `.opacity-0/50/100` | Opacité |
| `.pointer` / `.not-allowed` / `.grab` | `cursor` |
| `.pointer-none` | `pointer-events:none` |
| `.border-none` | `border:none` |
| `.rounded-none → .rounded-full` | Applique un radius de la section 3 |
| `.transition` / `.transition-colors/shadow/transform/opacity` | Applique une transition de la section 5 |

```html
<button class="btn btn-primary rounded-full transition-colors">Envoyer</button>
```

### 6.11 Responsive — mobile-first

**Stratégie mobile-first stricte** : le style de base cible le mobile ; chaque préfixe (`tablet-`, `laptop-`, `desktop-`, `wide-`) ne fait que **surcharger à partir** de son seuil, jamais en dessous. Les seuils sont documentés en dur dans les `@media` (les custom properties CSS ne fonctionnent pas dans un `@media`) :

| Préfixe | Seuil | ≈ px |
|---|---|---|
| *(aucun, base)* | — | < 768px |
| `tablet-` | `min-width: 48rem` | ≥ 768px |
| `laptop-` | `min-width: 64rem` | ≥ 1024px |
| `desktop-` | `min-width: 80rem` | ≥ 1280px |
| `wide-` | `min-width: 96rem` | ≥ 1536px |

Classes disponibles par palier (voir le fichier pour le détail exact par palier, certains n'ont pas tous les raccourcis) : `-hidden`, `-block`, `-flex`, `-grid`, `-row`, `-col`, `-grid-2/3/4/6`, et à partir de `laptop-` uniquement des `-gap-sm/md/lg/xl`.

```html
<!-- invisible sur mobile, devient flex à partir de la tablette -->
<nav class="hidden tablet-flex gap-lg">...</nav>

<!-- colonne + gap serré sur mobile, ligne + gap large dès laptop -->
<div class="col laptop-row gap-sm laptop-gap-lg">...</div>

<!-- 1 colonne sur mobile, 3 dès laptop, 4 dès desktop -->
<div class="grid laptop-grid-3 desktop-grid-4 gap-lg">...</div>
```


## 7. Squelette de composants (boîte/taille uniquement)

**Le point de jonction avec les design patterns.** Ces classes fixent uniquement padding/hauteur/gap interne/taille de police/display — jamais de couleur, ombre, bordure visible, fond ou radius. Sans elles, un pattern ne fait qu'ajouter de la couleur sur une boîte déjà bien dimensionnée.

| Classe | Ce qu'elle fixe |
|---|---|
| `.btn` | `display:inline-flex`, centré, `gap:var(--sp-xs)`, padding `var(--sp-sm) var(--sp-lg)`, `font-size:var(--fs-md)`, `font-weight:var(--weight-medium)`, pas de retour à la ligne |
| `.btn-sm` / `.btn-lg` | Variante de padding/taille de police |
| `.btn-icon-only` | Carré (`aspect-ratio:1/1`), padding uniforme — pour un bouton avec seulement une icône |
| `.btn-block` | Pleine largeur |
| `.input` | Bloc pleine largeur, padding `var(--sp-sm) var(--sp-md)`, `font-size:var(--fs-md)` |
| `.input-sm` / `.input-lg` | Variante de padding/taille |
| `.badge` | `inline-flex`, petit gap, padding compact, `font-size:var(--fs-xs)`, `font-weight:var(--weight-semibold)` |
| `.surface` | Padding `var(--sp-lg)` |
| `.surface-sm` / `.surface-lg` | Padding `var(--sp-md)` / `var(--sp-xl)` |
| `.modal` | Padding `var(--sp-xl)`, `max-width:48rem`, pleine largeur jusque-là |
| `.modal-sm` / `.modal-lg` | `max-width: 36rem` / `64rem` |
| `.divider` | Pleine largeur, marge verticale `var(--sp-lg)` |
| `.divider-vertical` | Pleine hauteur, marge horizontale `var(--sp-lg)` |
| `.icon` | `inline-flex`, 2rem × 2rem |
| `.icon-sm` / `.icon-lg` | 1.6rem / (voir fichier pour la valeur `lg` exacte selon la dernière révision) |

```html
<!-- Le reset donne la boîte, le pattern actif donne la couleur -->
<button class="btn btn-primary">Créer</button>
<input class="input" placeholder="Rechercher…">
<span class="badge badge-success">Actif</span>
<div class="surface">Contenu…</div>
```

**Ce squelette est identique quel que soit `data-style`** : c'est ce qui garantit qu'un composant garde exactement la même taille et le même comportement de layout en passant de `flat` à `glass` — seule son apparence change.
