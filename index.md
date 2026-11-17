# Sommaire des skills

Liste de tous les skills du repo. Chaque entrée renvoie vers l'`index.md` du skill.

| Skill | Description | Origine |
|-------|-------------|---------|
| [apple-design](apple-design/index.md) | Interfaces fluides et mouvement physique façon Apple, pour le web | Emil Kowalski |
| [grilling](grilling/index.md) | Interview impitoyable pour éprouver un plan, une décision ou une idée (base des deux autres) | Matt Pocock |
| [grill-me](grill-me/index.md) | Interview impitoyable pour affiner un plan, sans rien écrire (appelle grilling) | Matt Pocock |
| [grill-with-docs](grill-with-docs/index.md) | Interview impitoyable qui crée aussi la doc (ADR, glossaire) ; appelle grilling et domain-modeling | Matt Pocock |
| [design-without-ai-tells](design-without-ai-tells/index.md) | Concevoir ou relire une interface sans les signes « fait par IA » ; catalogue, workflow et audit | perso (synthèse de sources 2026) |
| [responsive-web-app](responsive-web-app/index.md) | Responsive d'app web : contraintes, construction et vérifications, de 320 px au desktop | perso (synthèse de sources 2026) |
| [interface-craft](interface-craft/index.md) | Détails fins d'interface : typographie, tactile, OKLCH, surfaces, animation, interaction (28 concepts, en ressources) | perso |
| [creative-design](creative-design/index.md) | Pousser un design vers la créativité : bibliothèque d'idées (21 fonds créatifs) et recherche web | perso |
| [app-motion](app-motion/index.md) | Animation d'app pour maximiser l'UX : 17 règles de motion, 12 principes Disney, 7 lois d'UX | perso |

## Interconnexions

Qui appelle qui. **Appel** = une étape du workflow appelle le skill avec l'outil Skill ; **souple** = simple renvoi, chargé seulement si la situation se présente. Pas de boucle : un appel est ignoré si le skill est déjà chargé dans la conversation (garde « si pas déjà chargé »), ce qui permet des appels dans les deux sens à des étapes différentes. Détail dans la section `Skill links` de chaque `SKILL.md`.

| De | Vers | Type | Quand |
|----|------|------|-------|
| interface-craft | design-without-ai-tells | **Appel** | *Building* avant d'appliquer les concepts (direction), puis en relecture finale (signes restants) |
| interface-craft | app-motion | souple | Un concept de la section Motion s'applique (budget selon la fréquence d'usage) |
| interface-craft | responsive-web-app | souple | Safe area, `dvh`, zones tactiles : la question dépasse le détail |
| design-without-ai-tells | interface-craft | **Appel** | Audit P2 « craft » : appliquer les corrections |
| design-without-ai-tells | creative-design | **Appel** | La question pré-livraison n°1 échoue : élargir les pistes |
| design-without-ai-tells | responsive-web-app | souple | Socle « layout téléphone » |
| creative-design | design-without-ai-tells | **Appel** | Checks avant livraison : l'idée n'est pas un défaut de second ordre |
| creative-design | interface-craft | souple | OKLCH, lisibilité, animation de l'effet |
| app-motion | interface-craft | souple | Détails d'animation (origine, interruptible, stagger) |
| app-motion | apple-design | souple | Gestes, drag, mouvement physique |
| responsive-web-app | interface-craft | souple | Détails tactiles (safe area, `dvh`, cibles) |
| responsive-web-app | design-without-ai-tells | souple | Style visuel, que ce skill ne décide pas |

`apple-design` n'a aucun lien sortant (skill tiers).

## Légende

- **Origine** : `perso` si je l'ai créé, sinon le nom de l'auteur ou de la source.

## Ajouter une entrée

```md
| [nom-du-skill](nom-du-skill/index.md) | Courte description | perso / auteur |
```
