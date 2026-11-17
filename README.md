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
    ├── SKILL.md     # Le noyau du skill : règles, workflow, checks
    └── references/  # Les ressources (listes, catalogues, valeurs, recettes)
        ├── index.md # Index des ressources : mis à jour sans toucher à SKILL.md
        └── ...      # Un fichier par catégorie ou par idée
```

## Ajouter un skill

1. Copier `_template/` vers un nouveau dossier au nom clair (ex. `product-design`).
2. Remplir `index.md` (description, installation, effets, crédits).
3. Écrire `SKILL.md` (le noyau) et mettre toute liste de ressources dans `references/`, avec un `references/index.md`.
4. Ajouter une ligne dans [`index.md`](index.md) à la racine.

## Règles

- Un dossier = un skill.
- `SKILL.md` = noyau stable ; `references/` = ressources faciles à mettre à jour.
- Les crédits sont obligatoires : auteur(s), source, licence quand elle existe.
- Pour un skill tiers, respecter sa licence et pointer vers la source d'origine.
