# `flat_design_pattern.css`

**Philosophie :** zéro profondeur. Couleur pure, aplats nets, bordures franches. Aucune ombre, aucun flou, aucun dégradé — la hiérarchie visuelle vient uniquement de la couleur et du contraste. C'est le pattern le plus "neutre" du framework, souvent utilisé comme base documentation/dashboard.

```html
<body data-style="flat" data-mode="light">   <!-- ou data-mode="dark" -->
```


## 1. Palette d'entrée (seule zone à modifier)

| Variable | Rôle | Défaut |
|---|---|---|
| `--palette-primary` | Marque — CTA, liens, focus | `#3B82F6` |
| `--palette-secondary` | Accent — deuxième signal | `#10B981` |
| `--palette-neutral` | Référence pour **tous** les gris | `#64748B` |
| `--palette-success` | Statut succès | `#22C55E` |
| `--palette-danger` | Statut erreur | `#EF4444` |
| `--palette-warning` | Statut avertissement | `#F59E0B` |
| `--palette-info` | Statut information | `#0EA5E9` |
| `--font-display` | Identité typographique | `"Inter", "Helvetica Neue", var(--font-sans)` |

Reskin depuis un stylesheet projet chargé après ce fichier :
```css
[data-style="flat"] { --palette-primary: #FF6B00; }
```

Tout le reste (échelles `--primary-100…900`, `--gray-50…950`, rôles `--text-primary`, `--btn-primary-bg`, etc.) est **calculé** depuis ces 7 valeurs via `color-mix()` — voir `00-index.md` §2 pour le schéma de dérivation complet. Ce fichier ne code aucune couleur en dur au-delà du bloc palette.


## 2. Classes de composants

### Surface
| Classe | Rendu |
|---|---|
| `.surface` | Fond `--bg-elevated` (blanc / gris très sombre), bordure 1px `--border-default`, radius `--radius-md` |

```html
<div class="surface p-lg">Contenu</div>
```

### Texte
| Classe | Rendu | Impact |
|---|---|---|
| `.text-heading` | Gras, `--text-primary`, interlignage serré | Titres |
| `.text-body` | `--text-secondary` | Paragraphes |
| `.text-label` | Majuscules, espacé, `--text-muted` | Étiquettes de champ, sur-titres |
| `.text-code` | Police mono, fond `--bg-surface`, radius sm | Extrait de code inline |
| `.text-primary` | `--text-primary` (le plus foncé/clair du gris) | Texte principal |
| `.text-secondary` | `--text-secondary` | Texte secondaire |
| `.text-muted` | `--text-muted` | Texte discret (métadonnées) |
| `.text-inverse` | Blanc / `--gray-900` selon mode | Texte sur fond plein (ex. dans `.btn-primary`) |
| `.text-link` (+ `:hover`) | `--text-link` → `--text-link-hover` | Liens |
| `.text-brand` | `--primary-500` | Accent marque brut |
| `.text-accent` | `--secondary-500` | Accent secondaire brut |
| `.text-success` / `-danger` / `-warning` / `-info` | Couleur de statut (teinte 700 en light, 300 en dark) | Messages de statut |

```html
<p class="text-label">Adresse e-mail</p>
<p class="text-body">Nous ne partageons jamais votre <a href="#" class="text-link">adresse</a>.</p>
<code class="text-code">npm install</code>
```

### Boutons
| Classe | Rendu |
|---|---|
| `.btn-primary` (+ `:hover`, `:active`) | Fond `--primary-500` → `700` → `900`, texte blanc |
| `.btn-secondary` (+ `:hover`) | Fond blanc/gris foncé, bordure `--gray-300` |
| `.btn-outline` (+ `:hover`) | Transparent, bordure et texte `--primary-*` |
| `.btn-ghost` (+ `:hover`) | Transparent, devient `--bg-surface` au survol |
| `.btn-accent` (+ `:hover`) | Fond `--secondary-500` → `700` |
| `.btn-danger` (+ `:hover`) | Fond `--danger-500` → `700` |
| `.btn:disabled` | Gris clair, `cursor:not-allowed` |

```html
<div class="row gap-sm">
  <button class="btn btn-primary">Enregistrer</button>
  <button class="btn btn-outline">Annuler</button>
  <button class="btn btn-danger">Supprimer</button>
</div>
```

### Champ
| Classe / état | Rendu |
|---|---|
| `.input` | Fond `--input-bg`, bordure `--input-border`, radius md |
| `.input:hover` | Bordure `--input-border-hover` |
| `.input:focus` | Bordure `--primary-500` + anneau `--focus-ring` |
| `.input.error` | Bordure `--danger-500` |

```html
<input class="input" placeholder="vous@exemple.com">
<input class="input error" value="adresse invalide">
```

### Icônes
`.icon` (gris muted), `.icon-brand` (primary), `.icon-accent` (secondary), `.icon-danger`, `.icon-success` — colore un `<svg>`/icône enfant via `currentColor`.

### Badges
`.badge` (forme pilule, bordure transparente) + variantes **fond doux / texte foncé** : `.badge-primary`, `-secondary`, `-success`, `-danger`, `-warning`, `-info`, `-neutral`.

```html
<span class="badge badge-success">Payé</span>
<span class="badge badge-warning">En attente</span>
```

### Modale & overlay
`.modal` (fond `--bg-elevated`, bordure, radius xl) · `.overlay` (fond noir semi-transparent, `position:fixed; inset:0`, `z-index:var(--z-overlay)`).

### Séparateurs
`.divider` (trait 1px horizontal) · `.divider-vertical` (trait 1px vertical).

### Fonds sémantiques
`.bg` (fond de page) · `.bg-surface` (fond de section) · `.bg-elevated` (fond de carte, le plus clair/contrasté).


## 3. Ce qui est propre à Flat (non présent ailleurs)

`.text-secondary`, `.text-inverse`, `.text-link`, `.text-code`, `.btn-outline`, `.btn-accent`, `.icon-danger`, `.icon-success`, `.badge-neutral`, `.bg`, `.bg-elevated`. Voir `00-index.md` §3.2 pour la justification — Flat sert souvent de base UI/dashboard, d'où un jeu de rôles de texte plus étoffé.
