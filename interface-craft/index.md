# interface-craft

> Appliquer les détails fins de typographie, de géométrie, de couleur, d'animation et d'interaction qui font la différence entre une interface correcte et une interface soignée.

## Description

Ce skill apprend à l'IA 29 concepts de finition d'interface, chacun avec une règle, une façon de l'appliquer en CSS/UI et l'erreur typique :

- **Typographie** : longueur de ligne, interlignage (leading), approche (tracking), crénage (kerning), hauteur d'x (x-height), veuves et orphelines (widow), chiffres tabulaires (tabular numbers).
- **Géométrie, icônes et tactile** : centre optique, rayons concentriques (concentric radius), épaisseur d'icône assortie au texte (matched icon weight), zone tactile (touch target), zone sûre (safe area), viewport dynamique (`svh`/`lvh`/`dvh`).
- **Couleur, surfaces et profondeur** : palettes OKLCH, dégradés OKLCH, bordures alpha (alpha borders), bords masqués (masked edges), profondeur en mode sombre (dark mode depth).
- **Animation** : animation liée à son origine, animation interruptible, cascade (stagger), transition d'élément partagé, échange d'icône flouté (blurred icon swap).
- **Interaction et état** : affordance, combobox, mise à jour optimiste, divulgation progressive, décalage de mise en page (layout shift).

Il se termine par un workflow construction/relecture avec gravité P0/P1/P2 et une checklist finale. Un concept n'est appliqué que si la situation existe dans l'écran.

Se déclenche quand tu polis un composant, audites des détails d'UI, ou qu'un écran « sonne faux » sans qu'on sache pourquoi.

## Dépendances

Aucune. Se combine avec `design-without-ai-tells` (direction et signes à éviter) : celui-ci décide de l'allure, `interface-craft` règle les détails.

## Installation

**Claude Code**

```bash
mkdir -p ~/.claude/skills/interface-craft
cp SKILL.md ~/.claude/skills/interface-craft/
```

Pour un seul projet : `.claude/skills/interface-craft/`.

**Windows (PowerShell)**

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills\interface-craft"
Copy-Item SKILL.md "$HOME\.claude\skills\interface-craft"
```

**Cursor** : copier dans `~/.cursor/skills/interface-craft/` ou `.cursor/skills/interface-craft/`.

**Autre IA** : coller le contenu de `SKILL.md` dans les instructions personnalisées.

## Effets

- Impose des valeurs concrètes : 44px de zone tactile, 45–75 caractères par ligne, 30–60 ms de stagger, 150–250 ms d'animation d'interface.
- Fait utiliser `tabular-nums`, `text-wrap: balance/pretty`, `env(safe-area-inset-*)`, `oklch()` et `linear-gradient(in oklch, …)`, `transform-origin`, View Transitions, `mask-image`, `dvh/svh`.
- Impose la formule du rayon concentrique (rayon extérieur = rayon intérieur + padding), des bordures en alpha plutôt qu'en gris opaque, et une élévation par la luminosité en mode sombre.
- Interdit les animations bloquantes et les éléments qui bougent sans action de l'utilisateur.
- En relecture, rapporte : concept, emplacement, problème, correction, avec gravité.

## Fichiers

| Fichier | Rôle |
|---------|------|
| `SKILL.md` | Le skill : 29 concepts, workflow, gravités, checklist (en anglais, pour l'IA) |

## Crédits

- **Auteur** : Aurel, avec Claude (synthèse originale, skill créé pour ce repo).
- **Source** : principes établis de typographie, des guidelines Apple HIG, Material, WCAG 2.2, WAI-ARIA APG, et de la documentation web (CSS, View Transitions, Core Web Vitals). Concepts ajoutés (novembre 2026) recoupés avec : [Jakub Krehel, concentric border radius](https://jakub.kr/work/concentric-border-radius), [30 Seconds of Code, nested border radius](https://30secondsofcode.org/css/s/nested-border-radius), [MDN, color interpolation method](https://developer.mozilla.org/en-US/docs/Web/CSS/color-interpolation-method), [web.dev, viewport units](https://web.dev/blog/viewport-units), [Chrome, soft edge content fade](https://developer.chrome.com/docs/modern-web-guidance/guides/visual-design/soft-edge-content-fade), [Material, dark theme](https://m2.material.io/design/color/dark-theme), [GitLab, icons lighten up](https://about.gitlab.com/blog/hey-icons-lighten-up/) et [UI Skills, match icon stroke weight](https://www.ui-skills.com/playbook/match-icon-stroke-weight). Les chiffres précis (1,5 px / 2 px, pas de 4-6 % de luminosité, 150-200 ms) sont des points de départ issus d'une seule source, à vérifier. Aucun texte tiers copié.
- **Licence** : MIT.
- **Modifications** : création initiale (20 concepts), puis ajout de 9 concepts : rayons concentriques, bordures alpha, palettes et dégradés OKLCH, épaisseur d'icône assortie, bords masqués, échange d'icône flouté, profondeur en mode sombre, viewport dynamique.
