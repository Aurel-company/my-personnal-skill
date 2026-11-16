# apple-design

> L'approche d'Apple pour les interfaces fluides et le mouvement « physique », traduite pour le web.

## Description

Ce skill apprend à l'IA à concevoir et relire des interfaces web qui ressemblent aux interfaces Apple : réponse instantanée, manipulation directe, animations à ressort (springs) interruptibles, inertie, matériaux translucides et typographie soignée. Le contenu vient des conférences WWDC d'Apple, surtout *Designing Fluid Interfaces* (WWDC 2018).

Il se déclenche quand on construit ou relit :

- des interfaces pilotées par gestes (drag, swipe, sheets) ;
- des animations à ressort et des transitions interruptibles ;
- des matériaux translucides et de la profondeur ;
- la typographie (optical sizing, tracking, leading) ;
- le `prefers-reduced-motion` et les fondations de design (feedback, cohérence spatiale, retenue).

Au premier appel sans question précise, le skill répond d'une seule phrase pour dire qu'il est prêt, puis attend ta question.

## Installation

**Claude Code** (global, disponible dans tous les projets)

```bash
mkdir -p ~/.claude/skills/apple-design
cp SKILL.md ~/.claude/skills/apple-design/SKILL.md
```

Pour un seul projet, copier dans `.claude/skills/apple-design/` à la racine du projet.

**Sous Windows (PowerShell)**

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills\apple-design"
Copy-Item SKILL.md "$HOME\.claude\skills\apple-design\SKILL.md"
```

**Cursor** : copier `SKILL.md` dans `~/.cursor/skills/apple-design/` (ou `.cursor/skills/apple-design/` dans le projet).

**Autre IA** : coller le contenu de `SKILL.md` dans les instructions personnalisées de l'outil.

Ensuite, appeler le skill avec `/apple-design` ou laisser l'IA le charger seule quand la tâche s'y prête.

## Effets

Une fois le skill chargé, l'IA :

- répond sur le pointer-down plutôt qu'au relâchement, et traque la latence ;
- suit le doigt 1:1 pendant un drag, avec feedback continu ;
- rend les animations interruptibles et reprend la vitesse du geste (velocity handoff) ;
- préfère les springs aux durées fixes, et projette l'inertie vers où va le geste ;
- gère les limites en rubber-band, avec des chemins d'aller-retour symétriques ;
- applique les matériaux translucides, le retour multimodal (mouvement, son, haptique) et la typographie optique ;
- respecte `prefers-reduced-motion` et l'accessibilité.

## Fichiers

| Fichier | Rôle |
|---------|------|
| `SKILL.md` | Le skill (17 sections et un aide-mémoire final), copie fidèle de l'original |
| `LICENSE` | Licence MIT d'origine, à conserver avec le skill |

## Crédits

- **Auteur** : [Emil Kowalski](https://github.com/emilkowalski)
- **Source** : https://github.com/emilkowalski/skills/tree/main/skills/apple-design
- **Version copiée** : commit `64eb3de` du repo `emilkowalski/skills`
- **Licence** : MIT (© 2026 Emil Kowalski), voir `LICENSE`
- **Contenu d'origine** : conférences WWDC d'Apple, surtout *Designing Fluid Interfaces* (WWDC 2018)
- **Modifications** : aucune, le fichier `SKILL.md` est identique à l'original
