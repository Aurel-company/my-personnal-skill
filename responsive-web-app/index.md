# responsive-web-app

> Construire, relire ou corriger le responsive d'une app web (tableaux de bord, formulaires, tableaux, navigation), du téléphone de 320 px au desktop.

## Description

Ce skill apprend à l'IA à faire un responsive **correct**, pas seulement joli sur trois tailles d'écran :

1. **Décider les contraintes** avant le code : largeur minimale, modes de saisie (tactile, souris, clavier), cas de contenu extrêmes, structure par taille, composants qui ont besoin de container queries.
2. **Construire** dans un ordre précis : fondations, mise en page intrinsèque, typographie fluide, comportement du viewport mobile, saisie tactile, composants (navigation, tableaux, formulaires, modales, images), accessibilité liée au responsive.
3. **Vérifier** avec une liste concrète : 320 px, zoom 400 %, scan de débordement horizontal, contenu extrême, espacement du texte, cibles tactiles, clavier virtuel, appareils réels.

Principes : mobile-first guidé par le contenu, intrinsèque d'abord (flex, grid, `clamp()`), requêtes ensuite, ne jamais bloquer les réglages de l'utilisateur (zoom, orientation), diagnostiquer le débordement au lieu de le masquer.

Se déclenche quand tu parles de responsive, de mise en page mobile, de breakpoints, de container queries, de scroll horizontal, de `100vh`, de zones sûres, de clavier virtuel, de cibles tactiles ou de reflow WCAG.

## Dépendances

Aucun appel obligatoire. Renvois souples vers `interface-craft` (détails tactiles : safe area, `dvh`, cibles), `design-without-ai-tells` (style visuel, que ce skill ne décide pas) et `web-to-mobile-app` (quand tu veux une vraie app mobile, pas du responsive). Se combine aussi avec un skill de design produit (parcours, états) et un contrôle d'accessibilité plus large.

## Installation

**Claude Code** (global, disponible dans tous les projets)

```bash
mkdir -p ~/.claude/skills/responsive-web-app
cp -r SKILL.md references ~/.claude/skills/responsive-web-app/
```

Pour un seul projet, copier dans `.claude/skills/responsive-web-app/` à la racine du projet.

**Sous Windows (PowerShell)**

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills\responsive-web-app"
Copy-Item SKILL.md, references -Recurse "$HOME\.claude\skills\responsive-web-app"
```

**Cursor** : copier `SKILL.md` et `references/` dans `~/.cursor/skills/responsive-web-app/` (ou `.cursor/skills/responsive-web-app/` dans le projet).

**Autre IA** : coller `SKILL.md` puis `references/responsive-checklist.md` dans les instructions personnalisées de l'outil.

Utilisation : automatique, ou à la main avec `/responsive-web-app`.

## Effets

- Fait écrire les contraintes (plage d'écrans, saisie, contenu extrême, structure) avant le premier code.
- Impose des règles : pas de `user-scalable=no`, pas de `100vh` pour les pleines hauteurs, pas de `vw` seul pour le texte, pas de `overflow-x: hidden` sur `body` pour cacher un bug.
- Couvre les bugs classiques : `100vw` qui déborde, enfants flex sans `min-width: 0`, pistes de grid sans `minmax(0, 1fr)`, zones sûres iOS, zoom iOS sur les champs à moins de 16 px, survol collé sur tactile, clavier virtuel qui masque une barre fixe.
- Donne des patterns par composant : navigation (barre du bas, rail, sidebar), tableaux (défilement, cartes, colonnes prioritaires), formulaires, images (`srcset`, `aspect-ratio`).
- Relie le responsive à WCAG : reflow à 320 px, espacement du texte, orientation, cibles de 24 px (44 px visés).
- Distingue ce qui est sourcé (W3C, web.dev, Chrome) de ce qui est du jugement (navigation, formulaires, modales).
- En relecture, rapporte : élément, condition où ça casse, cause, correction, classés par gravité.

## Fichiers

| Fichier | Rôle |
|---------|------|
| `SKILL.md` | Le skill : règles, workflow en 3 étapes, vérifications (en anglais, pour l'IA) |
| `references/responsive-checklist.md` | Checklist complète avec code, sources numérotées, jugement signalé |
| `references/sources.md` | Sources de la recherche, dates, fiabilité, limites |

## Crédits

- **Auteur** : Aurel, avec Claude (synthèse originale, skill créé pour ce repo).
- **Sources principales** : [Chrome for Developers](https://developer.chrome.com/docs/modern-web-guidance/guides/css/responsive-design), [web.dev](https://web.dev/articles/baseline-in-action-container-queries), [W3C WCAG 2.2](https://www.w3.org/WAI/WCAG22/Understanding/reflow.html), [OpenReplay](https://blog.openreplay.com/5-mobile-web-papercuts-fixes/), [Smashing Magazine](https://www.smashingmagazine.com/2021/04/css-overflow-issues/), [Polypane](https://polypane.app/blog/strategies-for-dealing-with-horizontal-overflows/), [UXPin](https://www.uxpin.com/studio/blog/mobile-navigation-examples/) et d'autres, détaillées dans `references/sources.md`.
- **Licence** : aucun texte des sources n'est copié ; seules les recommandations sont reprises et recoupées.
- **Limites connues** : modale vs plein écran non sourcé (jugement), support Safari d'`interactive-widget` non vérifié, pages MDN anglaises non lues pour `touch-action`, `scrollbar-gutter`, `text-wrap`.
- **Modifications** : sans objet, c'est une création.
