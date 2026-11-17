# Règles Claude pour ce repo

## Workflow Git (obligatoire)

- **Ne jamais pusher sur `main` directement**, y compris pour un petit changement ou un fix de typo.
- **Une branche par skill travaillé**, nommée `skill/<nom-du-skill>` (ex. `skill/product-design`). Pour un changement hors skill (README, index, template, règles), utiliser `chore/<sujet>` ou `docs/<sujet>`.
- Toujours partir d'un `main` à jour : `git checkout main && git pull`, puis créer la branche.
- Pousser la branche, puis ouvrir une **Pull Request** vers `main` (`gh pr create`).
- **Merger toujours en squash and merge** (`gh pr merge --squash --delete-branch`). Jamais de merge commit ni de rebase merge.
- Le titre de la PR devient le message du commit squashé : le rédiger clairement (ex. `Add skill: product-design`).

## Conventions du repo

- Un dossier = un skill, nommé en kebab-case, avec un `index.md` (description, installation, effets, crédits).
- Partir de `_template/` pour créer un nouveau skill.
- **`SKILL.md` = le noyau, `references/` = les ressources.** `SKILL.md` ne contient que les règles, le workflow, le format de relecture et les checks. Toute liste (concepts, bonnes pratiques, animations, valeurs, recettes, catalogue) va dans `<skill>/references/`, pour qu'on puisse la mettre à jour sans toucher au noyau.
- Chaque `references/` a un `index.md` qui liste chaque ressource (une ligne, son fichier, sa gravité si pertinent). `SKILL.md` pointe vers cet index, jamais vers le détail d'un concept : ajouter une ressource = ajouter un bloc/fichier + une ligne d'index, sans éditer `SKILL.md`.
- Quand on déplace du contenu vers `references/`, le texte est déplacé tel quel (pas de réécriture, pas de perte).
- Les commandes d'installation de l'`index.md` du skill doivent copier `references/` en plus de `SKILL.md` (`cp -r SKILL.md references …`).
- Toute nouvelle entrée de skill est ajoutée à `index.md` à la racine dans la même PR.
- Les crédits (auteurs, source, licence) sont obligatoires pour chaque skill.
