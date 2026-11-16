# creative-design

> Pousser un design vers plus de créativité : une bibliothèque d'idées créatives (21 fonds au départ) à consulter, plus une méthode de recherche web quand elle ne suffit pas.

## Description

Ce skill combine deux choses :

1. **Une bibliothèque de ressources** (`references/`) : une fiche par idée, avec l'effet visuel, quand l'utiliser ou l'éviter, comment la fabriquer (CSS, SVG, canvas, shader), la lisibilité, le coût, les associations et des mots-clés de recherche.
2. **Une méthode** (`SKILL.md`) : lire le brief, consulter la bibliothèque, chercher sur le web au besoin, pousser l'idée (combiner, contraindre, changer de médium ou d'échelle, soustraire, rendre réactif), proposer trois directions, construire, puis réinjecter les trouvailles dans la bibliothèque.

Idées de départ (fonds créatifs) : felt texture, fluted glass, water ripples, speckled graphite, single-hue landscapes, blueprint grids, halftone, grainy gradients, grass texture, dithered images, paper texture, contour lines, cloud sky, pixel mosaics, lens distortion, stippled gradients, square-dot grids, blurred photos, iridescent shapes, impressionist paintings, ASCII and pixels.

Se déclenche quand tu veux un rendu plus créatif ou distinctif, que tu cherches des idées ou de l'inspiration, qu'il te faut un fond ou une texture, ou qu'un design paraît plat ou « template ».

## Dépendances

Aucune. Se combine avec `design-without-ai-tells` (éviter les signes « IA ») et `interface-craft` (détails de finition : OKLCH, lisibilité, animation). La recherche web utilise l'outil de recherche de l'IA.

## Installation

**Claude Code**

```bash
mkdir -p ~/.claude/skills/creative-design
cp -r SKILL.md references ~/.claude/skills/creative-design/
```

Pour un seul projet : `.claude/skills/creative-design/`.

**Windows (PowerShell)**

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills\creative-design"
Copy-Item SKILL.md, references -Recurse "$HOME\.claude\skills\creative-design"
```

**Cursor** : copier `SKILL.md` et `references/` dans `~/.cursor/skills/creative-design/` ou `.cursor/skills/creative-design/`.

**Autre IA** : coller `SKILL.md`, puis `references/library-index.md` et les fiches utiles dans les instructions personnalisées.

## Effets

- Force à diverger : au moins trois directions avant de construire, dont une inattendue.
- Relie chaque technique au produit en une phrase, pour éviter la décoration gratuite.
- Impose le socle : contraste du texte, version de secours statique, `prefers-reduced-motion`, version mobile allégée.
- Cherche sur le web en suivant un protocole (requêtes, sources, licences) et ne copie ni œuvre ni code sans licence adaptée.
- Fait grossir la bibliothèque : les trouvailles vont dans `references/inbox.md`, puis sont promues en fiche.

## Fichiers

| Fichier | Rôle |
|---------|------|
| `SKILL.md` | Le skill : règles, workflow en 6 étapes, format des propositions (en anglais, pour l'IA) |
| `references/library-index.md` | Index des idées : ambiance, technique, coût, associations |
| `references/backgrounds/*.md` | Une fiche par idée de fond (21) |
| `references/research-protocol.md` | Protocole de recherche web : requêtes, sources, licences |
| `references/inbox.md` | Boîte d'entrée des nouvelles trouvailles à tester et promouvoir |

Pour étendre la bibliothèque : ajouter une fiche en copiant la structure d'une existante, puis une ligne dans `library-index.md`. D'autres catégories (typographie, mouvement, couleur, mise en page) peuvent avoir leur dossier à côté de `backgrounds/`.

## Crédits

- **Auteur** : Aurel, avec Claude (skill et fiches créés pour ce repo ; liste d'idées de départ fournie par Aurel).
- **Source** : techniques courantes du web (CSS, SVG, canvas, WebGL) et d'algorithmes classiques (halftone, dithering de Bayer et Floyd-Steinberg/Atkinson, stippling, marching squares). Aucun texte tiers copié.
- **Licence** : MIT.
- **Modifications** : sans objet, c'est une création.
