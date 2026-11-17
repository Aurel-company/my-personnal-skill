# interface-craft

> Appliquer les détails fins de typographie, de géométrie, de couleur, d'animation et d'interaction qui font la différence entre une interface correcte et une interface soignée.

## Description

Ce skill apprend à l'IA 28 concepts de finition d'interface, chacun avec une règle, une façon de l'appliquer en CSS/UI et l'erreur typique :

- **Typographie** : longueur de ligne, interlignage (leading), approche (tracking), crénage (kerning), hauteur d'x (x-height), veuves et orphelines (widow), chiffres tabulaires (tabular numbers).
- **Géométrie, icônes et tactile** : centre optique, rayons concentriques (concentric radius), épaisseur d'icône assortie au texte (matched icon weight), zone tactile (touch target), zone sûre (safe area), viewport dynamique (`svh`/`lvh`/`dvh`).
- **Couleur, surfaces et profondeur** : palettes OKLCH, dégradés OKLCH, bordures alpha (alpha borders), bords masqués (masked edges), profondeur en mode sombre (dark mode depth).
- **Animation** : animation liée à son origine, animation interruptible, cascade (stagger), transition d'élément partagé, échange d'icône flouté (blurred icon swap).
- **Interaction et état** : affordance, combobox, mise à jour optimiste, divulgation progressive, décalage de mise en page (layout shift).

Le noyau (`SKILL.md`) ne contient que le workflow construction/relecture et la checklist finale. Les concepts vivent dans `references/`, avec un index qui donne pour chacun la gravité P0/P1/P2 : on peut en ajouter ou en modifier sans toucher au noyau. Un concept n'est appliqué que si la situation existe dans l'écran.

Se déclenche quand tu polis un composant, audites des détails d'UI, ou qu'un écran « sonne faux » sans qu'on sache pourquoi.

## Dépendances

Appelle `design-without-ai-tells` (appel obligatoire : direction avant de construire, vérification des signes « IA » en fin de relecture) : celui-ci décide de l'allure, `interface-craft` règle les détails. Renvois souples vers `app-motion` (budget d'animation) et `responsive-web-app` (questions responsive plus larges). Si un de ces skills n'est pas installé, `interface-craft` continue sans : les installer à côté pour profiter des liens.

## Installation

**Claude Code**

```bash
mkdir -p ~/.claude/skills/interface-craft
cp -r SKILL.md references ~/.claude/skills/interface-craft/
```

Pour un seul projet : `.claude/skills/interface-craft/`.

**Windows (PowerShell)**

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills\interface-craft"
Copy-Item SKILL.md, references -Recurse "$HOME\.claude\skills\interface-craft"
```

**Cursor** : copier `SKILL.md` et `references/` dans `~/.cursor/skills/interface-craft/` ou `.cursor/skills/interface-craft/`.

**Autre IA** : coller `SKILL.md`, puis `references/index.md` et les fichiers de catégorie utiles, dans les instructions personnalisées.

## Effets

- Impose des valeurs concrètes : 44px de zone tactile, 45–75 caractères par ligne, 30–60 ms de stagger, 150–250 ms d'animation d'interface.
- Fait utiliser `tabular-nums`, `text-wrap: balance/pretty`, `env(safe-area-inset-*)`, `oklch()` et `linear-gradient(in oklch, …)`, `transform-origin`, View Transitions, `mask-image`, `dvh/svh`.
- Impose la formule du rayon concentrique (rayon extérieur = rayon intérieur + padding), des bordures en alpha plutôt qu'en gris opaque, et une élévation par la luminosité en mode sombre.
- Interdit les animations bloquantes et les éléments qui bougent sans action de l'utilisateur.
- En relecture, rapporte : concept, emplacement, problème, correction, avec gravité.

## Fichiers

| Fichier | Rôle |
|---------|------|
| `SKILL.md` | Le noyau : règles, workflow construction/relecture, checklist finale (en anglais, pour l'IA) |
| `references/index.md` | Index des 28 concepts : cas d'usage et gravité P0/P1/P2 |
| `references/typography.md` | 7 concepts de typographie |
| `references/geometry-icons-touch.md` | 6 concepts de géométrie, icônes et tactile |
| `references/color-surfaces.md` | 5 concepts de couleur, surfaces et profondeur |
| `references/motion.md` | 5 concepts d'animation |
| `references/interaction-state.md` | 5 concepts d'interaction et d'état |

Pour ajouter un concept : un bloc `## Concept` (Rule / Apply / Failure) dans le fichier de la bonne catégorie, puis une ligne dans `references/index.md`. `SKILL.md` ne change pas.

## Crédits

- **Auteur** : Aurel, avec Claude (synthèse originale, skill créé pour ce repo).
- **Source** : principes établis de typographie, des guidelines Apple HIG, Material, WCAG 2.2, WAI-ARIA APG, et de la documentation web (CSS, View Transitions, Core Web Vitals). Concepts ajoutés (novembre 2026) recoupés avec : [Jakub Krehel, concentric border radius](https://jakub.kr/work/concentric-border-radius), [30 Seconds of Code, nested border radius](https://30secondsofcode.org/css/s/nested-border-radius), [MDN, color interpolation method](https://developer.mozilla.org/en-US/docs/Web/CSS/color-interpolation-method), [web.dev, viewport units](https://web.dev/blog/viewport-units), [Chrome, soft edge content fade](https://developer.chrome.com/docs/modern-web-guidance/guides/visual-design/soft-edge-content-fade), [Material, dark theme](https://m2.material.io/design/color/dark-theme), [GitLab, icons lighten up](https://about.gitlab.com/blog/hey-icons-lighten-up/) et [UI Skills, match icon stroke weight](https://www.ui-skills.com/playbook/match-icon-stroke-weight). Les chiffres précis (1,5 px / 2 px, pas de 4-6 % de luminosité, 150-200 ms) sont des points de départ issus d'une seule source, à vérifier. Aucun texte tiers copié.
- **Licence** : MIT.
- **Modifications** : création initiale (20 concepts), puis ajout de 9 concepts : rayons concentriques, bordures alpha, palettes et dégradés OKLCH, épaisseur d'icône assortie, bords masqués, échange d'icône flouté, profondeur en mode sombre, viewport dynamique. Les concepts ont ensuite été déplacés de `SKILL.md` vers `references/` (texte inchangé) ; le décompte corrigé est de 28 concepts (et non 29).
