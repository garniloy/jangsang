# `full_design_pattern.css`

**Rôle :** le bundle. Contient les 6 styles (`flat`, `flat-deep`, `material`, `glow`, `glass`, `neuro`) dans un seul fichier, tous branchés sur **une seule palette projet** définie une fois dans `:root`. À utiliser quand plusieurs `data-style` doivent coexister sur une même page tout en restant reconnaissables comme la même marque (ex. une section `material` et une section `glass` sur le même site).

Si un seul style suffit pour tout le site, préfère le fichier individuel correspondant (plus léger, palette scopée à `[data-style="..."]` donc sans risque de collision si tu changes d'avis plus tard et charges un deuxième fichier de pattern).

```html
<link rel="stylesheet" href="reset_layout_framework.css">
<link rel="stylesheet" href="full_design_pattern.css">
<body data-style="flat" data-mode="light">
  <section data-style="glass" data-mode="dark">...</section>
  <section data-style="material" data-mode="light">...</section>
</body>
```


## 1. Palette d'entrée — unique pour tout le bundle

Définie une seule fois dans `:root` (et non plus scopée par `[data-style]` comme dans les fichiers individuels, puisque c'est précisément le but du bundle : une identité de marque partagée entre tous les styles).

| Variable | Défaut |
|---|---|
| `--palette-primary` | `#4F46E5` |
| `--palette-secondary` | `#14B8A6` |
| `--palette-neutral` | `#64748B` |
| `--palette-success/danger/warning/info` | `#22C55E` / `#EF4444` / `#F59E0B` / `#0EA5E9` |

Reskin global (tous les styles du bundle changent ensemble) :
```css
:root { --palette-primary: #FF6B00; }
```


## 2. Composants par style

Les classes de chaque section (`[data-style="flat"]`, `[data-style="material"]`, etc.) sont un **sous-ensemble condensé** des fichiers individuels correspondants — même socle commun (voir `00-index.md` §3.1), mêmes noms de classes, mêmes rôles. Pour le détail complet de chaque classe, référence-toi à la fiche du pattern individuel :

- `[data-style="flat"]` → voir `02-flat.md`
- `[data-style="material"]` → voir `03-material.md`
- `[data-style="glow"]` → voir `04-glow.md`
- `[data-style="glass"]` → voir `05-glass.md`
- `[data-style="neuro"]` → voir `06-neuro.md`


## 3. `flat-deep` — n'existe QUE dans ce fichier

Flat-deep, c'est Flat + une hiérarchie par ombre portée neutre (`--shadow-xs` → `--shadow-2xl`, définis dans ce fichier). Il partage tous les tokens `--text-*`/`--btn-*`/`--badge-*` de Flat (même bloc de rôles sémantiques, sélecteur combiné `[data-style="flat"], [data-style="flat-deep"]`), mais ses classes de composants ajoutent une ombre :

| Classe | Rendu |
|---|---|
| `.surface` | Ombre `--shadow-md`, `:hover` → `--shadow-lg` |
| `.surface-sunken` | Ombre `inset` (aspect creusé, ex. zone de saisie de code) |
| `.btn-primary` | Fond plein + ombre teintée marque qui s'intensifie au survol |
| `.btn-secondary` | Fond carte + `--shadow-sm` → `--shadow-md` au survol |
| `.input` | Bordure fine + `--shadow-xs` |
| `.modal` | `--shadow-2xl` |
| `.overlay` | Fond noir 45% + `backdrop-filter: blur(2px)` |

```html
<body data-style="flat-deep" data-mode="light">
  <div class="surface p-lg">Carte avec ombre portée</div>
  <button class="btn btn-primary">Action avec ombre</button>
</body>
```

Utilise `flat-deep` plutôt que `flat` quand la page a besoin de plusieurs niveaux de hiérarchie visuelle par la profondeur (dashboard avec cartes empilées, par exemple) sans basculer vers l'identité beaucoup plus marquée de Material.


## 4. Différences avec les fichiers individuels

- Palette en `:root` (partagée) plutôt que scopée `[data-style]` (isolée par fichier).
- Pas de commentaire pédagogique répété section par section (pour rester lisible malgré la taille) — la pédagogie est dans les fichiers individuels et dans cette documentation.
- Contient `flat-deep`, absent des fichiers individuels.
- Les corrections appliquées aux fichiers individuels (`.text-primary`/`.text-muted`/`.text-info`/`.badge-info` en Glow, `.text-info` en Glass, `.btn-secondary` en Neuro) sont également répercutées ici, pour que le bundle reste rigoureusement équivalent aux fichiers individuels sur le socle commun.
