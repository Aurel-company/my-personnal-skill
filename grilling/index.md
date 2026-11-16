# grilling

> Interview impitoyable pour éprouver un plan, une décision ou une idée. C'est le skill de base de la famille « grill ».

## Description

L'IA interroge l'utilisateur sans relâche jusqu'à un accord partagé. Elle construit un **arbre de décisions** (chaque décision débouche sur d'autres) et le parcourt par **tours** :

- elle pose en un seul tour toutes les questions dont les prérequis sont déjà réglés ;
- chaque question est numérotée et accompagnée de la réponse recommandée par l'IA, formulée pour qu'un « oui » l'accepte ;
- elle attend tes réponses avant le tour suivant.

Les **faits** (fichiers, outils, environnement) sont cherchés par l'IA elle-même via des sous-agents : elle ne te les demande jamais. Les **décisions** restent les tiennes. La session se termine quand plus aucune branche n'est à explorer, et l'IA n'agit qu'après ta confirmation.

Le skill se déclenche seul quand tu veux éprouver ton raisonnement, ou quand tu emploies une formule du type « grill me ».

## Dépendances

Aucune. C'est le skill que `grill-me` et `grill-with-docs` appellent : installe-le avec eux.

## Installation

**Claude Code** (global, disponible dans tous les projets)

```bash
mkdir -p ~/.claude/skills/grilling
cp SKILL.md ~/.claude/skills/grilling/SKILL.md
```

Pour un seul projet, copier dans `.claude/skills/grilling/` à la racine du projet.

**Sous Windows (PowerShell)**

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills\grilling"
Copy-Item SKILL.md "$HOME\.claude\skills\grilling\SKILL.md"
```

**Cursor** : copier `SKILL.md` dans `~/.cursor/skills/grilling/` (ou `.cursor/skills/grilling/` dans le projet).

**Autre IA** : coller le contenu de `SKILL.md` dans les instructions personnalisées de l'outil.

**Tout le pack d'un coup** (méthode de l'auteur) : `npx skills@latest add mattpocock/skills`

Utilisation : automatique, ou à la main avec `/grilling`.

## Effets

- Pose les questions par tours numérotés, chacune avec une réponse recommandée.
- Explore l'arbre de décisions branche par branche, sans rien supposer en silence.
- Cherche elle-même les faits dans l'environnement via des sous-agents.
- N'agit pas avant ta confirmation d'un accord partagé.

## Fichiers

| Fichier | Rôle |
|---------|------|
| `SKILL.md` | Le skill, copie fidèle de l'original |
| `LICENSE` | Licence MIT d'origine, à conserver avec le skill |

## Crédits

- **Auteur** : [Matt Pocock](https://github.com/mattpocock) ([AI Hero](https://www.aihero.dev))
- **Source** : https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling
- **Version copiée** : commit `5863806` du repo `mattpocock/skills`
- **Licence** : MIT (© 2026 Matt Pocock), voir `LICENSE`
- **Modifications** : aucune, le fichier `SKILL.md` est identique à l'original
