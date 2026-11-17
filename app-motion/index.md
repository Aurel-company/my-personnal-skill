# app-motion

> Concevoir et relire l'animation d'une app pour maximiser l'UX : règles de motion concrètes, principes d'animation de Disney adaptés à l'interface, et lois d'UX.

## Description

Ce skill apprend à l'IA à concevoir le mouvement d'une app comme un outil au service de l'utilisateur : **feedback**, **orientation**, **continuité**, **attention**, et seulement en dernier **plaisir**. Tout y est une **recommandation, pas une obligation** : les valeurs sont des points de départ, et chaque écart doit être justifié en une ligne.

Il rassemble trois ensembles de concepts :

- **17 règles de motion UI** : ease-out pour les entrées, menus déroulants à 150–250 ms, stagger de 30 ms sur les lignes de liste, scale 0,97 à l'appui, étirement de 12 % des boutons mobiles, stagger quand les détails se posent, arcs pour les déplacements d'objets, pulse pour confirmer un succès, ease-in-out pour les déplacements, popovers à 0,95, entrer depuis le déclencheur et sortir vers lui, pas de rebond sur l'UI du quotidien, pas d'interpolation quand l'élément est tenu, sorties 20 % plus courtes, chevauchement ancien/nouvel état, masques pour révéler et changer de couleur.
- **12 principes d'animation** adaptés : squash & stretch, anticipation, staging, pose to pose, follow through, slow in & slow out, arcs, action secondaire, timing snappy, exagération du feedback, solid drawing (3D), appeal.
- **7 lois d'UX** : Fitts (grandes zones de clic), Hick, Miller, Doherty, Postel, Jakob, et la fréquence d'usage.

Le point d'entrée du workflow est la **fréquence d'usage** : plus une interaction est fréquente, moins elle a de mouvement. Le noyau (`SKILL.md`) ne garde que le workflow et le format de relecture. La fiche de valeurs et les recettes par composant (bouton, menu, popover, modale, switch, liste, toast, thème, page, drag) sont dans `references/`, avec un index : on peut les enrichir sans toucher au noyau.

Se déclenche quand tu ajoutes, règles ou audites de l'animation dans une app, ou quand le mouvement paraît lent, bruyant, rebondissant ou générique.

## Dépendances

Aucun appel obligatoire. Renvois souples vers `interface-craft` (détails : origine, interruptible, stagger, éléments partagés), `apple-design` (mouvement fluide et physique) et `design-without-ai-tells` (fade-in partout).

## Installation

**Claude Code**

```bash
mkdir -p ~/.claude/skills/app-motion
cp -r SKILL.md references ~/.claude/skills/app-motion/
```

Pour un seul projet : `.claude/skills/app-motion/`.

**Windows (PowerShell)**

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills\app-motion"
Copy-Item SKILL.md, references -Recurse "$HOME\.claude\skills\app-motion"
```

**Cursor** : copier `SKILL.md` et `references/` dans `~/.cursor/skills/app-motion/` ou `.cursor/skills/app-motion/`.

**Autre IA** : coller `SKILL.md`, puis `references/index.md` et les fichiers de `references/` utiles, dans les instructions personnalisées.

## Effets

- Fait choisir le budget de mouvement selon la fréquence d'usage avant toute animation.
- Exige un but (feedback, orientation, continuité, attention, plaisir) : sans but, pas d'animation.
- Donne des valeurs de départ : 150–250 ms, stagger 30 ms, scale 0,97 à l'appui, 0,95 pour un popover, étirement 12 %, sorties 20 % plus courtes.
- Impose des garde-fous : animations interruptibles, `transform`/`opacity`, tokens partagés, `prefers-reduced-motion`.
- En relecture, rapporte : élément, comportement actuel, recommandation, bénéfice UX, avec distinction « à corriger » / « à améliorer ».

## Fichiers

| Fichier | Rôle |
|---------|------|
| `SKILL.md` | Le noyau : workflow, budget selon la fréquence d'usage, relecture, checks (en anglais, pour l'IA) |
| `references/index.md` | Index des ressources : à mettre à jour quand on en ajoute une |
| `references/cheat-sheet.md` | Fiche de valeurs de départ par situation |
| `references/component-recipes.md` | Recettes par composant |
| `references/ui-motion-rules.md` | 17 règles de motion UI avec valeurs, code et cas où s'en passer |
| `references/disney-principles.md` | 12 principes d'animation traduits pour l'interface |
| `references/ux-laws.md` | 7 lois d'UX et leurs conséquences sur le mouvement |

## Crédits

- **Auteur** : Aurel, avec Claude (synthèse originale, skill créé pour ce repo ; liste de concepts fournie par Aurel).
- **Source** : les 12 principes de l'animation (Ollie Johnston et Frank Thomas, *The Illusion of Life*, 1981), les lois d'UX (Jon Yablonsky, [lawsofux.com](https://lawsofux.com/)), et la documentation web sur les transitions CSS, les View Transitions et `offset-path`. Les valeurs chiffrées sont des points de départ courants, à tester sur ton produit. Aucun texte tiers copié.
- **Licence** : MIT.
- **Modifications** : fiche de valeurs et recettes par composant déplacées de `SKILL.md` vers `references/` (texte inchangé), ajout de `references/index.md`.
