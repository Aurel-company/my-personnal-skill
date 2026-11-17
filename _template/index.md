# Nom du skill

> Une phrase qui résume ce que fait le skill.

## Description

À quoi sert le skill, dans quels cas l'IA le déclenche.

## Installation

Adapter selon l'outil.

**Claude Code**

```bash
# Copier SKILL.md et references/ dans :
#   ~/.claude/skills/<nom-du-skill>/        (global)
#   .claude/skills/<nom-du-skill>/          (projet)
mkdir -p ~/.claude/skills/<nom-du-skill>
cp -r SKILL.md references ~/.claude/skills/<nom-du-skill>/
```

**Windows (PowerShell)**

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills\<nom-du-skill>"
Copy-Item SKILL.md, references -Recurse "$HOME\.claude\skills\<nom-du-skill>"
```

**Cursor**

```bash
# Copier dans ~/.cursor/skills/<nom-du-skill>/ ou .cursor/skills/<nom-du-skill>/
```

**Autre IA** : copier le contenu de `SKILL.md`, puis `references/index.md` et les fiches utiles, dans les instructions personnalisées de l'outil.

## Effets

Ce que le skill change dans le comportement de l'IA :

- Effet 1
- Effet 2

## Fichiers

| Fichier | Rôle |
|---------|------|
| `SKILL.md` | Le noyau du skill : règles, workflow, checks |
| `references/index.md` | Index des ressources (listes, catalogues, valeurs) |
| `references/*.md` | Les ressources, mises à jour sans toucher à `SKILL.md` |

## Crédits

- **Auteur(s)** : nom(s)
- **Source** : lien vers le repo ou la page d'origine
- **Licence** : MIT / autre / non précisée
- **Modifications** : indiquer si j'ai adapté le skill
