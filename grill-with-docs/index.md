# grill-with-docs

> Interview impitoyable qui crée aussi la documentation au fil de l'eau : ADR et glossaire. Elle passe par les skills `grilling` et `domain-modeling`.

## Description

Version **avec état** pour les bases de code. C'est la même interview que `grill-me`, mais l'IA laisse une trace écrite pendant la discussion : décisions d'architecture (ADR) et glossaire du domaine. Le fichier ne contient qu'une ligne, qui demande à l'IA d'appeler les skills `grilling` et `domain-modeling`. Le comportement vient de ces deux skills.

Le skill est marqué `disable-model-invocation: true` : l'IA ne le lance jamais seule, c'est toi qui le déclenches.

À lancer à la main avec `/grill-with-docs`.

## Dépendances

**`grilling` et `domain-modeling` sont obligatoires** : `grill-with-docs` ne fait que les appeler.

- `grilling` est dans ce repo : `../grilling/`.
- `domain-modeling` est du même auteur (Matt Pocock) mais n'est pas encore dans ce repo. Sans lui, la partie documentation ne fonctionne pas.

## Installation

**Claude Code** (global, disponible dans tous les projets)

```bash
mkdir -p ~/.claude/skills/grill-with-docs
cp SKILL.md ~/.claude/skills/grill-with-docs/SKILL.md
```

Pour un seul projet, copier dans `.claude/skills/grill-with-docs/` à la racine du projet. Installe aussi `grilling` et `domain-modeling` au même endroit.

**Sous Windows (PowerShell)**

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills\grill-with-docs"
Copy-Item SKILL.md "$HOME\.claude\skills\grill-with-docs\SKILL.md"
```

**Cursor** : copier `SKILL.md` dans `~/.cursor/skills/grill-with-docs/` (ou `.cursor/skills/grill-with-docs/` dans le projet).

**Autre IA** : coller le contenu de `SKILL.md`, de `grilling/SKILL.md` et de `domain-modeling` dans les instructions personnalisées de l'outil, puisque `grill-with-docs` seul ne contient qu'un renvoi.

**Tout le pack d'un coup** (méthode de l'auteur, dépendances comprises) : `npx skills@latest add mattpocock/skills`

## Effets

- Lance une session d'interview complète via `grilling`.
- Documente le domaine au fil de la discussion via `domain-modeling` : glossaire et ADR.
- Laisse une trace écrite dans le repo du projet, contrairement à `grill-me`.

## Fichiers

| Fichier | Rôle |
|---------|------|
| `SKILL.md` | Le skill (un simple appel à `grilling` et `domain-modeling`), copie fidèle de l'original |
| `LICENSE` | Licence MIT d'origine, à conserver avec le skill |

## Crédits

- **Auteur** : [Matt Pocock](https://github.com/mattpocock) ([AI Hero](https://www.aihero.dev))
- **Source** : https://github.com/mattpocock/skills/tree/main/skills/engineering/grill-with-docs
- **Version copiée** : commit `5863806` du repo `mattpocock/skills`
- **Licence** : MIT (© 2026 Matt Pocock), voir `LICENSE`
- **Modifications** : aucune, le fichier `SKILL.md` est identique à l'original
