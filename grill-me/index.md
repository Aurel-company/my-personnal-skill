# grill-me

> Interview impitoyable pour affiner un plan ou un design, sans rien écrire. Elle passe par le skill `grilling`.

## Description

Version **sans état** de l'interview, pour tout ce qui n'est pas du code : un plan, une idée, une décision. Le fichier ne contient qu'une ligne, qui demande à l'IA d'appeler le skill `grilling`. Tout le comportement vient donc de `grilling`.

Le skill est marqué `disable-model-invocation: true` : l'IA ne le lance jamais seule, c'est toi qui le déclenches.

À lancer à la main avec `/grill-me`.

## Dépendances

**`grilling` est obligatoire** : `grill-me` ne fait que l'appeler. Installe aussi `../grilling/`.

## Installation

**Claude Code** (global, disponible dans tous les projets)

```bash
mkdir -p ~/.claude/skills/grill-me
cp SKILL.md ~/.claude/skills/grill-me/SKILL.md
```

Pour un seul projet, copier dans `.claude/skills/grill-me/` à la racine du projet. Installe aussi `grilling` au même endroit.

**Sous Windows (PowerShell)**

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills\grill-me"
Copy-Item SKILL.md "$HOME\.claude\skills\grill-me\SKILL.md"
```

**Cursor** : copier `SKILL.md` dans `~/.cursor/skills/grill-me/` (ou `.cursor/skills/grill-me/` dans le projet).

**Autre IA** : coller le contenu de `SKILL.md` ET celui de `grilling/SKILL.md` dans les instructions personnalisées de l'outil, puisque `grill-me` seul ne contient qu'un renvoi.

**Tout le pack d'un coup** (méthode de l'auteur) : `npx skills@latest add mattpocock/skills`

## Effets

- Lance une session d'interview complète via `grilling`.
- Ne crée aucun fichier : tout reste dans la conversation.

## Fichiers

| Fichier | Rôle |
|---------|------|
| `SKILL.md` | Le skill (un simple appel à `grilling`), copie fidèle de l'original |
| `LICENSE` | Licence MIT d'origine, à conserver avec le skill |

## Crédits

- **Auteur** : [Matt Pocock](https://github.com/mattpocock) ([AI Hero](https://www.aihero.dev))
- **Source** : https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me
- **Version copiée** : commit `5863806` du repo `mattpocock/skills`
- **Licence** : MIT (© 2026 Matt Pocock), voir `LICENSE`
- **Modifications** : aucune, le fichier `SKILL.md` est identique à l'original
