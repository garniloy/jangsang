# Creative Toolkit — Documentation du framework

Cette documentation couvre les 7 fichiers CSS du framework :

| Fichier | Rôle | Contient de la couleur ? |
|---|---|---|
| `reset_layout_framework.css` | Reset + layout + spacing + typo structurelle + responsive | **Non, jamais** |
| `flat_design_pattern.css` | Design pattern FLAT | Oui |
| `material_design_pattern.css` | Design pattern MATERIAL | Oui |
| `glow_design_pattern.css` | Design pattern GLOW | Oui |
| `glass_design_pattern.css` | Design pattern GLASS (glassmorphism) | Oui |
| `neuro_design_pattern.css` | Design pattern NEURO (neumorphism) | Oui |
| `full_design_pattern.css` | Bundle des 6 styles ci-dessus, une seule palette partagée | Oui |

Chaque fichier a sa propre page de doc (`01-...` à `07-...`). Ce document-ci est la carte du territoire : l'architecture globale, la règle de séparation des responsabilités, et surtout — puisque c'est ce qui a motivé cette doc — le **contrat de classes commun** entre les 6 patterns, avec un tableau qui montre noir sur blanc ce qui est partagé et ce qui ne l'est pas, et pourquoi.


## 1. La règle d'or : deux couches, deux responsabilités

```
reset_layout_framework.css   →  OÙ et COMBIEN (position, taille, espace)
   +
<style>_design_pattern.css   →  QUOI (couleur, matière, ombre, identité visuelle)
```

- Le **reset** ne contient **aucune couleur**. Il pose : les tokens d'espacement (`--sp-*`), la typographie structurelle (tailles, graisses, interlignage — jamais de couleur de texte), les radius/blur en tant que *dimensions*, le z-index, les transitions, le grid/flexbox, le responsive, et un "squelette" de composants (`.btn`, `.input`, `.badge`, `.surface`, `.modal`, `.divider`, `.icon`) qui ne fixe que padding/hauteur/gap/font-size — jamais de fond, bordure visible, ombre ou radius.
- Un **design pattern** ne contient **aucun spacing/layout**. Il pose : la palette du projet (7 couleurs d'entrée), les échelles dérivées via `color-mix()`, les rôles sémantiques (texte/fond/bordure), et habille en couleur/texture les mêmes classes `.btn`, `.input`, etc. déjà dimensionnées par le reset.

Concrètement, un bouton est **toujours** `class="btn btn-primary"` — jamais autre chose selon le style actif. C'est le reset qui lui donne son padding, c'est le pattern actif (via `data-style`) qui lui donne sa couleur et sa matière.

### Pourquoi cette séparation

1. **Un bug de couleur ne peut jamais venir du reset**, et un bug de layout ne peut jamais venir d'un pattern. Ça borne instantanément où chercher.
2. **Changer de style = changer une seule ligne** (`data-style="glass"` → `data-style="neuro"`) sans toucher au HTML ni au reset.
3. **Chaque pattern peut être reskinné indépendamment** en ne touchant qu'un seul bloc PALETTE, en haut de son fichier.


## 2. Chaîne de dérivation des couleurs

Aucune couleur n'est écrite en dur au-delà du bloc PALETTE. Tout en découle :

```
PALETTE (7 couleurs projet)
   --palette-primary / secondary / neutral / success / danger / warning / info
        │
        ▼  color-mix(in srgb, ...)
ÉCHELLES DÉRIVÉES
   --primary-100…900, --secondary-100…900, --gray-50…950,
   --success/danger/warning/info-100…700
        │
        ▼
RÔLES SÉMANTIQUES (mode light, puis override [data-mode="dark"])
   --text-primary, --bg-surface, --btn-primary-bg, --badge-danger-bg, …
        │
        ▼
COMPOSANTS (classes CSS appliquées aux éléments)
   .btn-primary, .badge-danger, .surface, .input:focus, …
```

Reskinner un pattern = changer les 7 valeurs du bloc PALETTE. Tout le reste se recalcule automatiquement — c'est le point central demandé lors de la refonte de ce framework.

### Comment reskinner depuis un stylesheet projet

Le bloc PALETTE est scopé à `[data-style="nom-du-pattern"]`, pas à `:root`. Pour le surcharger depuis un fichier chargé **après** le pattern :

```css
/* mon-projet.css, chargé après flat_design_pattern.css */
[data-style="flat"] {
  --palette-primary: #FF6B00;
  --palette-secondary: #002B5B;
}
```


## 3. Le contrat de classes commun

**C'est la remarque qui a motivé cette doc : tous les patterns n'avaient pas exactement les mêmes classes.** Deux choses différentes se cachaient derrière ce constat, et il fallait les traiter différemment :

- Des **oublis réels** (une classe du socle commun manquante dans un pattern par erreur) → **corrigés** dans cette passe (voir le détail dans chaque fiche pattern, section "Écarts corrigés").
- Des **extras volontaires**, propres à la philosophie d'un pattern (ex. `.btn-tonal` n'a de sens qu'en Material, `.surface-inset` n'a de sens qu'en Neuro) → **conservés et documentés comme tels**, pas comme un défaut.

### 3.1 — Le socle commun (présent, à l'identique, dans les 6 patterns)

| Catégorie | Classes du socle |
|---|---|
| Surface | `.surface` |
| Texte — structure | `.text-heading`, `.text-body`, `.text-label` |
| Texte — rôle | `.text-primary`, `.text-muted`, `.text-brand`, `.text-accent` |
| Texte — statut | `.text-success`, `.text-danger`, `.text-warning`, `.text-info` |
| Bouton | `.btn`, `.btn-primary`, `.btn-secondary`, `.btn-ghost`, `.btn-danger` |
| Champ | `.input` (+ `:hover`, `:focus`, `::placeholder`) |
| Icône | `.icon`, `.icon-brand`, `.icon-accent` |
| Badge | `.badge`, `.badge-primary`, `.badge-secondary`, `.badge-success`, `.badge-danger`, `.badge-warning`, `.badge-info` |
| Modale | `.modal`, `.overlay` |
| Séparateur | `.divider`, `.divider-vertical` |
| Fond | `.bg-surface` (au minimum) |

Ces classes se comportent partout de la même façon *structurellement* (même rôle, même déclencheur), même si leur rendu visuel change radicalement d'un pattern à l'autre — c'est précisément le but.

### 3.2 — Extras propres à chaque pattern (volontaires, pas des oublis)

| Pattern | Classes en plus du socle | Pourquoi ça n'existe que là |
|---|---|---|
| **Flat** | `.text-secondary`, `.text-inverse`, `.text-link`, `.text-code`, `.btn-outline`, `.btn-accent`, `.icon-danger`, `.icon-success`, `.badge-neutral`, `.bg`, `.bg-elevated` | Flat est le pattern "par défaut", le plus riche en rôles de texte utilitaires (liens, code inline) car c'est souvent le pattern de base d'une UI de type documentation/dashboard. |
| **Material** | `.surface-elevated`, `.surface-flat`, `.text-secondary`, `.btn-tonal`, `.badge-neutral`, `.bg`, `.bg-elevated`, `.shadow-sm/md/lg/none` | Le système d'élévation (Material) a besoin de paliers de surface et d'utilitaires d'ombre explicites — ça n'a de sens que dans un système bâti sur la profondeur par ombre neutre. |
| **Glow** | `.text-glow` | Rôle de texte spécifique au halo lumineux (texte qui *rayonne*), sans équivalent dans les autres patterns. |
| **Glass** | `.btn-brand` | Variante de bouton "plein" tinté marque, utile en glass car `.btn-primary` y reste volontairement translucide (esprit verre) — `.btn-brand` donne une option non-translucide quand il faut un CTA très visible sur un fond chargé. |
| **Neuro** | `.surface-inset`, `.btn-inset` | Le negatif du relief neumorphique (creusé plutôt qu'extrudé) — concept qui n'existe que dans une matière "molle". |

### 3.3 — Différence assumée : pas d'utilitaires `.shadow-*` en Neuro

Material a des utilitaires `.shadow-sm/md/lg/none` génériques ; Neuro n'en a **volontairement pas**. En neumorphisme, une ombre n'a de sens que par paire (claire + sombre) et collée à `--nm-bg` : l'appliquer isolément sur un fond arbitraire casse l'illusion de matière. Utilise `.surface` / `.surface-inset` à la place. C'est documenté dans le fichier lui-même en commentaire.


## 4. Sommaire des fiches

1. [`01-reset-layout-framework.md`](01-reset-layout-framework.md) — tous les tokens et toutes les classes utilitaires de layout/spacing/typo/responsive
2. [`02-flat.md`](02-flat.md)
3. [`03-material.md`](03-material.md)
4. [`04-glow.md`](04-glow.md)
5. [`05-glass.md`](05-glass.md)
6. [`06-neuro.md`](06-neuro.md)
7. [`07-full-bundle.md`](07-full-bundle.md) — le fichier combiné, pour mélanger plusieurs `data-style` sur une même page
