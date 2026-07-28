# Creative Toolkit — Composants Interactifs (roadmap)

Liste de travail pour le futur dossier `interactive-components/`. Même logique que le reste
du framework : **structure/comportement** dans un fichier neutre (JS + classes squelette sans
couleur), **apparence** redéfinie par chaque `[data-style="..."]`. Coche au fur et à mesure.

Légende de priorité : 🔴 essentiel · 🟡 courant · 🟢 confort/nice-to-have

---

## 1. Overlays & fenêtres flottantes

- [ ] 🔴 **Dropdown / Menu** — menu contextuel ancré à un bouton (ouverture au clic, fermeture au clic extérieur ou `Échap`)
- [ ] 🔴 **Tooltip** — infobulle au survol/focus, positionnement auto (haut/bas/gauche/droite selon l'espace)
- [ ] 🔴 **Popover** — comme le tooltip mais cliquable, peut contenir du contenu riche (pas juste du texte)
- [ ] 🔴 **Drawer / Side panel** — panneau qui glisse depuis un bord (mobile nav, filtres, détail d'un item)
- [ ] 🟡 **Alert dialog / Confirm dialog** — variante du `.modal` déjà existant, avec focus trap et actions destructrices
- [ ] 🟡 **Context menu** — menu au clic droit, positionné à la souris
- [ ] 🟡 **Toast / Snackbar** — notification temporaire empilable (queue, auto-dismiss, action "annuler")
- [ ] 🟢 **Command palette** (type Cmd+K) — recherche globale au clavier, liste filtrée en direct
- [ ] 🟢 **Notification center** — panneau qui liste l'historique des toasts/alertes

## 2. Navigation

- [ ] 🔴 **Tabs** — bascule de panneaux, indicateur animé qui suit l'onglet actif
- [ ] 🔴 **Accordion** — sections repliables, mode "un seul ouvert" ou "plusieurs ouverts"
- [ ] 🔴 **Breadcrumb** — fil d'ariane avec séparateurs configurables
- [ ] 🟡 **Pagination** — numérotée + précédent/suivant, variante "load more"
- [ ] 🟡 **Stepper / Wizard** — formulaire multi-étapes avec indicateur de progression
- [ ] 🟡 **Segmented control** — groupe de boutons exclusifs (remplace un `<select>` à 2-4 options)
- [ ] 🟡 **Sidebar navigation** — collapsible, sous-menus, état actif
- [ ] 🟢 **Mega menu** — dropdown de navigation multi-colonnes
- [ ] 🟢 **Back-to-top** — bouton flottant qui apparaît au scroll
- [ ] 🟢 **Scrollspy** — met en surbrillance le lien de nav correspondant à la section visible

## 3. Formulaires avancés

- [ ] 🔴 **Select personnalisé** — remplace le `<select>` natif, stylable comme les autres composants
- [ ] 🔴 **Toggle / Switch** — interrupteur on/off (au-delà du simple checkbox)
- [ ] 🔴 **Checkbox & Radio stylés** — versions custom cohérentes avec `.input`
- [ ] 🟡 **Combobox / Autocomplete** — champ texte + suggestions filtrées en direct
- [ ] 🟡 **Multi-select / Tag input** — sélection multiple avec chips supprimables
- [ ] 🟡 **Date picker** — calendrier + saisie manuelle, plage de dates
- [ ] 🟡 **Range slider** — simple et double poignée (min/max)
- [ ] 🟡 **File upload** — zone drag & drop + liste de fichiers avec progression
- [ ] 🟡 **Password field** — bouton afficher/masquer + indicateur de force
- [ ] 🟢 **OTP / Pin input** — série de cases pour code à 4-6 chiffres
- [ ] 🟢 **Time picker**
- [ ] 🟢 **Color picker**
- [ ] 🟢 **Rating** — étoiles/cœurs cliquables

## 4. Affichage de données

- [ ] 🔴 **Table triable/filtrable** — clic sur en-tête pour trier, ligne survolée
- [ ] 🟡 **Table avec lignes expansibles** — détail au clic sur une ligne
- [ ] 🟡 **Carousel / Slider** — images ou cartes, swipe mobile, indicateurs
- [ ] 🟡 **Lightbox / Galerie image** — zoom plein écran avec navigation
- [ ] 🟡 **Timeline** — événements chronologiques, verticale/horizontale
- [ ] 🟢 **Tree view** — arborescence repliable (fichiers, catégories)
- [ ] 🟢 **Kanban board** — colonnes + cartes déplaçables (drag & drop)
- [ ] 🟢 **Avatar group / stack** — avatars superposés avec "+N"
- [ ] 🟢 **Calendrier / agenda** — vue mois/semaine avec événements

## 5. Feedback & état système

- [ ] 🔴 **Spinner / Loader** — indicateur de chargement (inline + plein écran)
- [ ] 🔴 **Progress bar** — déterminée et indéterminée
- [ ] 🟡 **Skeleton screen** — placeholders animés pendant le chargement
- [ ] 🟡 **Empty state** — illustration + message quand une liste est vide
- [ ] 🟡 **Alert / Banner inline** — message contextuel (succès/erreur/info) dans le flux, pas en overlay
- [ ] 🟢 **Copy-to-clipboard** — bouton avec confirmation visuelle
- [ ] 🟢 **Scroll progress bar** — fine barre en haut de page qui suit le scroll
- [ ] 🟢 **Like / favorite toggle** — micro-interaction avec animation

## 6. Layout dynamique

- [ ] 🟡 **Split pane / panneaux redimensionnables** — glisser une poignée pour ajuster deux zones
- [ ] 🟢 **Masonry grid** — grille de hauteurs inégales type Pinterest
- [ ] 🟢 **Infinite scroll** — chargement automatique au scroll

## 7. Système / utilitaires transverses

- [ ] 🟡 **Theme switcher formalisé** — le toggle light/dark déjà présent dans la page-catalogue, à transformer en composant réutilisable (persistant via storage)
- [ ] 🟢 **Cookie consent banner**
- [ ] 🟢 **Focus trap utilitaire** — brique commune réutilisée par modal/drawer/dialog pour piéger le Tab à l'intérieur

---

## Conventions à tenir pour chaque composant (à confirmer ensemble au fil du travail)

- Un fichier **structure** (`interactive-components/<nom>.js` + squelette CSS sans couleur dans le reset ou un fichier dédié) et une **apparence** qui suit le même schéma `[data-style="..."] .composant { ... }` que le reste.
- État géré via attributs (`data-open`, `data-selected`, `aria-expanded`, etc.) plutôt que classes JS ad-hoc, pour rester accessible par défaut.
- Réutilisation systématique des tokens existants : `--duration-*`, `--ease-*`, `--z-*` (déjà une pile sémantique dropdown/sticky/modal/overlay/toast/tooltip prête à l'emploi), `--radius-*`, `--focus-ring`.
- Chaque composant à clavier + lecteur d'écran dès la version 1 (pas en rattrapage) : rôles ARIA, gestion `Échap`/flèches/`Tab` selon le pattern WAI-ARIA correspondant.

---

*On travaille cette liste dans l'ordre que tu veux — dis-moi par quel composant on commence.*
