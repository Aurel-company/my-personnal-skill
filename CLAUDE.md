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
- Toute nouvelle entrée de skill est ajoutée à `index.md` à la racine dans la même PR.
- Les crédits (auteurs, source, licence) sont obligatoires pour chaque skill.
