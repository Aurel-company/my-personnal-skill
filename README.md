# my-personnal-skill

Ma bibliothèque personnelle de **skills pour IA** (Claude Code, Cursor, Codex, etc.) : ceux que j'utilise au quotidien et ceux que je crée moi-même.

## Intentions

- **Centraliser** tous mes skills au même endroit, versionnés et faciles à retrouver.
- **Documenter** chaque skill : à quoi il sert, comment l'installer, quels effets il a sur l'IA.
- **Créditer** correctement les auteurs : si un skill vient de quelqu'un d'autre, son nom et sa source sont indiqués.
- **Réinstaller vite** mon environnement sur une nouvelle machine ou un nouvel outil.
- **Partager** mes propres créations.

## Structure

```
my-personnal-skill/
├── README.md        # Ce fichier : les intentions du repo
├── index.md         # Sommaire de tous les skills
├── _template/       # Modèle à copier pour ajouter un skill
│   └── index.md
└── <nom-du-skill>/  # Un dossier par skill, nommé en kebab-case
    ├── index.md     # Explication, installation, effets, crédits
    ├── SKILL.md     # Le skill lui-même
    └── ...          # Autres fichiers .md du skill (références, exemples)
```

## Ajouter un skill

1. Copier `_template/` vers un nouveau dossier au nom clair (ex. `product-design`).
2. Remplir `index.md` (description, installation, effets, crédits).
3. Ajouter les fichiers `.md` du skill dans le dossier.
4. Ajouter une ligne dans [`index.md`](index.md) à la racine.

## Règles

- Un dossier = un skill.
- Les crédits sont obligatoires : auteur(s), source, licence quand elle existe.
- Pour un skill tiers, respecter sa licence et pointer vers la source d'origine.
