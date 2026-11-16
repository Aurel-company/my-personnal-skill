# interface-craft

> Appliquer les détails fins de typographie, de géométrie, de couleur, d'animation et d'interaction qui font la différence entre une interface correcte et une interface soignée.

## Description

Ce skill apprend à l'IA 20 concepts de finition d'interface, chacun avec une règle, une façon de l'appliquer en CSS/UI et l'erreur typique :

- **Typographie** : longueur de ligne, interlignage (leading), approche (tracking), crénage (kerning), hauteur d'x (x-height), veuves et orphelines (widow), chiffres tabulaires (tabular numbers).
- **Géométrie et tactile** : centre optique, zone tactile (touch target), zone sûre (safe area).
- **Couleur** : OKLCH.
- **Animation** : animation liée à son origine, animation interruptible, cascade (stagger), transition d'élément partagé.
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
- Fait utiliser `tabular-nums`, `text-wrap: balance/pretty`, `env(safe-area-inset-*)`, `oklch()`, `transform-origin`, View Transitions.
- Interdit les animations bloquantes et les éléments qui bougent sans action de l'utilisateur.
- En relecture, rapporte : concept, emplacement, problème, correction, avec gravité.

## Fichiers

| Fichier | Rôle |
|---------|------|
| `SKILL.md` | Le skill : 20 concepts, workflow, gravités, checklist (en anglais, pour l'IA) |

## Crédits

- **Auteur** : Aurel, avec Claude (synthèse originale, skill créé pour ce repo).
- **Source** : principes établis de typographie, des guidelines Apple HIG, Material, WCAG 2.2, WAI-ARIA APG, et de la documentation web (CSS, View Transitions, Core Web Vitals). Aucun texte tiers copié.
- **Licence** : MIT.
- **Modifications** : sans objet, c'est une création.
