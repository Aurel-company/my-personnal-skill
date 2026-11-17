# design-without-ai-tells

> Concevoir ou relire une interface pour qu'elle ne ressemble pas à un produit généré par IA : repérer les signes, et surtout les remplacer par de vraies décisions.

## Description

Un design paraît « fait par IA » quand des **choix par défaut n'ont jamais été remplacés par des décisions**. Ce skill apprend à l'IA à :

1. **Décider avant de générer** : public, point de vue, polices, couleurs, forme, structure et ton, écrits avant tout code.
2. **Construire contre un catalogue** de signes à éviter, classés par catégorie (typographie, couleur, mise en page, composants, animation, images, texte, états, code).
3. **Auditer avant de livrer** avec des niveaux de gravité (P0 vu par tout le monde, P1 vu par les designers, P2 finition) et six questions finales.

Il insiste sur un piège : remplacer un signe par le défaut suivant (crème + terracotta, noir + vert acide, un mot d'accent dans le titre…) reste un signe. Un signe n'est pas une preuve : une bordure colorée qui code un statut ou une police choisie exprès sont légitimes.

Se déclenche quand tu construis ou relis un front et que le résultat doit paraître signé, spécifique et humain, ou quand tu parles de « slop IA », de dégradé violet, de page « template ».

## Dépendances

Appelle `interface-craft` (appel obligatoire à l'audit P2 : rayons concentriques, chiffres tabulaires, retour à la ligne des titres, alignement optique) et `creative-design` (appel obligatoire quand la direction est trop générique). Renvois souples vers `responsive-web-app` (socle téléphone) et `app-motion` (feedback animé utile). Se combine aussi avec un skill de design produit (parcours, états) et un détecteur automatique quand il y en a un. Si un skill lié n'est pas installé, `design-without-ai-tells` continue sans.

## Installation

**Claude Code** (global, disponible dans tous les projets)

```bash
mkdir -p ~/.claude/skills/design-without-ai-tells
cp -r SKILL.md references ~/.claude/skills/design-without-ai-tells/
```

Pour un seul projet, copier dans `.claude/skills/design-without-ai-tells/` à la racine du projet.

**Sous Windows (PowerShell)**

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills\design-without-ai-tells"
Copy-Item SKILL.md, references -Recurse "$HOME\.claude\skills\design-without-ai-tells"
```

**Cursor** : copier `SKILL.md` et `references/` dans `~/.cursor/skills/design-without-ai-tells/` (ou `.cursor/skills/design-without-ai-tells/` dans le projet).

**Autre IA** : coller `SKILL.md`, puis `references/index.md` et `references/ai-tells-catalog.md`, dans les instructions personnalisées de l'outil.

Utilisation : automatique, ou à la main avec `/design-without-ai-tells`.

## Effets

- Force un cadrage écrit (idéalement un `DESIGN.md`) avant la première ligne de code UI.
- Interdit d'inventer logos, clients, chiffres, témoignages ou photos d'équipe.
- Fait repérer et remplacer les signes : dégradés et lueurs, Inter non choisi, hero centré, cartes identiques, bordures colorées, glassmorphism, fade-in partout, emoji en icônes, mots creux, tirets cadratins, images IA, badges de builders.
- Couvre aussi la hiérarchie et le regroupement (un seul CTA principal, grouper par l'espacement, agrandir la fonctionnalité principale, supprimer badges décoratifs, pastilles de filtre et labels redondants) et les détails de finition (mono seulement si nécessaire, chiffres tabulaires, titres bien coupés, rayon intérieur = rayon extérieur − padding, alignement à l'œil).
- Fait vérifier le socle : contraste AA, focus, `prefers-reduced-motion`, mobile, formulaires qui fonctionnent.
- En relecture, rapporte chaque trouvaille ainsi : signe, emplacement, pourquoi il fait « IA », remplacement concret.

## Fichiers

| Fichier | Rôle |
|---------|------|
| `SKILL.md` | Le noyau : règles, workflow en 3 étapes, questions d'audit (en anglais, pour l'IA) |
| `references/index.md` | Index des ressources : signes principaux et ordre de correction P0/P1/P2 |
| `references/ai-tells-catalog.md` | Catalogue complet : signe, pourquoi il fait « IA », remplacement, gravité |
| `references/sources.md` | Sources de la recherche, dates, limites |

Pour ajouter un signe : une ligne dans la bonne section du catalogue (avec sa gravité), et au besoin dans les listes de `references/index.md`. `SKILL.md` ne change pas.

## Crédits

- **Auteur** : Aurel, avec Claude (synthèse originale, skill créé pour ce repo).
- **Sources** : articles et skills publiés en 2026, détaillés dans `references/sources.md`. Principaux : Developers Digest, Utsubo (Jocelyn Lecamus), 925Studios, Kosta Canatselis, et les skills open source [avoid-ai-design](https://github.com/funboy322/avoid-ai-design) (funboy322, MIT), [Anti-Slop Design](https://github.com/Ferousco-dev/anti-slop-design) (Feranmi, MIT) et [Hallmark](https://github.com/nutlope/hallmark) (Together AI, MIT).
- **Licence** : aucun texte des sources n'est copié ; seules les idées sont reprises et recoupées. Les licences des dépôts cités sont indiquées pour information.
- **Modifications** : création initiale, puis ajout de 9 signes au catalogue (badges et pastilles décoratifs, labels redondants, regroupement par l'espacement, CTA concurrents, mono décoratif, chiffres proportionnels, titres mal coupés, rayons imbriqués identiques, alignement par la boîte). Ces lignes sont taguées `[c]` (pratique établie) dans le catalogue. Les listes de signes principaux et l'ordre P0/P1/P2 ont ensuite été déplacés de `SKILL.md` vers `references/index.md` (texte inchangé).
