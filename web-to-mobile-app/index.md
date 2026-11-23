# web-to-mobile-app

> Transposer une app web en vraie app mobile (iOS et Android), pas en site responsive, avec un workflow validé étape par étape et un contrat qui garde le fil.

## Description

Ce skill guide l'IA pour faire d'une app web une app mobile à part entière, en huit étapes, chacune validée avant de passer à la suite :

0. **Cadrage** : lecture du code web, plateformes cibles, stack mobile, création du contrat.
1. **Inventaire et tri des features** : un tableau avec ce que fait chaque feature et un verdict (garder, adapter, remplacer, retirer, ajouter). Pour chaque adaptation, le problème mobile précis et une solution.
2. **Architecture de navigation** : un graphe Mermaid complet, chaque écran typé (onglet, écran de pile, modale, bottom sheet, drawer, dialog) et chaque lien annoté par son interaction (tap, swipe, long press, deep link, push).
3. **Grilling design et artefact** (optionnel) : un maximum de questions, puis l'artefact de design.
4. **Conventions iOS et Android** : seulement celles qui s'appliquent, avec ce qui est commun et ce qui diverge.
5. **États** : chargement, vide, erreur, hors ligne, permission refusée, session expirée, onboarding, mise à jour forcée.
6. **Relecture du contrat** et résumé simple.
7. **Implémentation par vagues** d'agents, le contrat servant de spécification unique.

Le **contrat** (`docs/mobile-transposition/CONTRACT.md` dans le projet) est un fichier temporaire où chaque décision validée est écrite. L'IA le relit au début de chaque étape, ce qui évite de perdre le fil, même sur une longue conversation ou une nouvelle session. Une retouche sur une étape passée met à jour le contrat et signale les étapes impactées.

Se déclenche quand tu parles de porter, transposer ou refaire ton app web en app mobile, de version iOS ou Android, de React Native ou Flutter à partir d'une app existante.

## Dépendances

Appels obligatoires (avec la garde « si pas déjà chargé ») : `grilling` et `design-without-ai-tells` à l'étape 3. Renvois souples vers `responsive-web-app` (si tu veux en fait du responsive), `interface-craft`, `app-motion` et `apple-design`.

## Installation

**Claude Code** (global, disponible dans tous les projets)

```bash
mkdir -p ~/.claude/skills/web-to-mobile-app
cp -r SKILL.md references ~/.claude/skills/web-to-mobile-app/
```

Pour un seul projet, copier dans `.claude/skills/web-to-mobile-app/` à la racine du projet.

**Sous Windows (PowerShell)**

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills\web-to-mobile-app"
Copy-Item SKILL.md, references -Recurse "$HOME\.claude\skills\web-to-mobile-app"
```

**Cursor** : copier `SKILL.md` et `references/` dans `~/.cursor/skills/web-to-mobile-app/` (ou `.cursor/skills/web-to-mobile-app/` dans le projet).

**Autre IA** : coller `SKILL.md` puis `references/index.md` et les fiches utiles dans les instructions personnalisées de l'outil.

Utilisation : automatique, ou à la main avec `/web-to-mobile-app`.

## Effets

- Impose un workflow à étapes avec validation explicite, sans sauter d'étape.
- Tient un contrat écrit dans le projet, relu à chaque étape, avec statuts et journal des changements.
- Part du code web réel pour l'inventaire, et justifie chaque adaptation par un problème mobile précis.
- Produit un graphe de navigation typé et vérifie que chaque feature a un écran et chaque écran un retour.
- Distingue ce qui est commun aux deux plateformes de ce qui doit suivre iOS ou Android.
- Définit les états de chaque écran et ceux de l'app entière.
- Termine par un résumé clair et une proposition d'implémentation par vagues d'agents.
- En relecture, rapporte : écran ou feature, problème, règle, correction, classés P0, P1, P2.

## Fichiers

| Fichier | Rôle |
|---------|------|
| `SKILL.md` | Le noyau : règles, workflow en 8 étapes, format de relecture, checks (en anglais, pour l'IA) |
| `references/index.md` | Index des ressources, avec l'étape où chacune sert |
| `references/contract-template.md` | Modèle du contrat |
| `references/feature-triage.md` | Verdicts, questions de décision, cas d'adaptation courants |
| `references/web-to-native-patterns.md` | Équivalent natif de chaque pattern web |
| `references/navigation-graph.md` | Notation Mermaid du graphe, règles, exemple |
| `references/design-grilling.md` | Banque de questions pour le grilling design |
| `references/platform-conventions.md` | Conventions iOS et Android |
| `references/states.md` | États par écran et états globaux |
| `references/implementation-waves.md` | Découpage en vagues et règles pour les agents |
| `references/sources.md` | Sources et fiabilité |

## Crédits

- **Auteur** : Aurel, avec Claude (création pour ce repo).
- **Sources principales** : [Apple Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/), [Material Design 3](https://m3.material.io/), [Android Developers](https://developer.android.com/), détaillées dans `references/sources.md`.
- **Licence** : aucun texte des sources n'est copié ; seules les recommandations sont reprises.
- **Limites connues** : le tri des features, la table web vers natif, la notation du graphe et le découpage en vagues relèvent du jugement. Les règles des plateformes et des stores évoluent chaque année : vérifier les pages officielles avant de s'appuyer sur un détail.
- **Modifications** : sans objet, c'est une création.
