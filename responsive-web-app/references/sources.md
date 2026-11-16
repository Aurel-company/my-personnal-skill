# Sources de la recherche

Recherche faite le 2026-11-16, en deux passes. Le contenu est une **synthèse originale** : aucune phrase n'est copiée, seules les recommandations sont reprises. Les numéros correspondent aux renvois `[n]` de [responsive-checklist.md](responsive-checklist.md). Les éléments sans numéro dans la checklist sont du **jugement** (convention de praticiens ou connaissance générale), pas des faits sourcés.

## Sources primaires (les plus fiables)

| # | Source | Date | Apport |
|---|---|---|---|
| 1 | [Responsive design, Chrome for Developers](https://developer.chrome.com/docs/modern-web-guidance/guides/css/responsive-design) | non datée | `clamp()`, jamais `vw` seul, max ≤ 2,5 × min, `dvh`/`svh`, `aspect-ratio`, container queries |
| 2 | [Container queries and units in action, web.dev](https://web.dev/articles/baseline-in-action-container-queries) | 23 oct. 2025 | Media vs container queries, `cqi`, `lh`/`rlh`, pièges des conteneurs |
| 8 | [Prepare for viewport resize behavior changes, Chrome](https://developer.chrome.com/blog/viewport-resize-behavior) | non datée | `interactive-widget` : `resizes-visual`, `resizes-content`, `overlays-content` |
| 10 | [WCAG 2.2, Reflow (1.4.10)](https://www.w3.org/WAI/WCAG22/Understanding/reflow.html) et [Target Size Minimum (2.5.8)](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html) | W3C | 320 px / 256 px, exceptions, cibles 24 px et recommandation 44 px |
| 15 | [Responsive images, web.dev](https://web.dev/learn/images/prescriptive) | non datée | `srcset`, `sizes`, `<picture>` pour l'art direction |

## Sources secondaires (conseils de praticiens)

| # | Source | Auteur | Date | Apport |
|---|---|---|---|---|
| 3 | Même article que [2] (renvoi utilisé pour le choix media query / container query) | web.dev | 23 oct. 2025 | Voir [2] |
| 4 | [Overflow Issues In CSS](https://www.smashingmagazine.com/2021/04/css-overflow-issues/) | Smashing Magazine | 2021 | Enfants flex et taille minimale du contenu, `min-width: 0` |
| 5 | [Strategies for dealing with horizontal overflows](https://polypane.app/blog/strategies-for-dealing-with-horizontal-overflows/) | Polypane | non datée | `100vw` et barre de défilement, `stretch` |
| 6 | [Finding and fixing unintended body overflow](https://www.cloudspress.com/finding-and-fixing-unintended-body-overflow/) et [100vw and the horizontal overflow…](https://destroytoday.com/blog/100vw-and-the-horizontal-overflow-you-probably-didnt-know-about) | Cloudspress, Destroy Today | non datées | Diagnostic du débordement, `min-width: 0` sur le bon élément |
| 7 | [5 Mobile Web Papercuts (and How to Fix Them)](https://blog.openreplay.com/5-mobile-web-papercuts-fixes/) | OpenReplay Team | 5 avr. 2026 | `100vh`/`svh`, zones sûres, zoom iOS à 16 px, `overscroll-behavior`, cibles 44 px, émulation DevTools |
| 9 | [touch-action: manipulation, Can I use](https://caniuse.com/mdn-css_properties_touch-action_manipulation), [scrollbar-gutter](https://reference.hyper-text.org/css/propaty/scrollbar-gutter), [text-wrap](https://reference.hyper-text.org/css/propaty/text-wrap/) | Can I use, hyper-text.org | non datées | Références secondaires, pages MDN anglaises non lues |
| 11 | [Detecting Hover-Capable Devices](https://css-irl.info/detecting-hover-capable-devices/) et résultats d'une recherche sur `hover` / `pointer` | CSS-IRL et autres | non datées | `@media (hover: hover)`, `pointer: coarse`, `any-hover`, appareils hybrides |
| 12 | [Mobile Navigation Design: 8 Types, Examples & Best Practices (2026)](https://www.uxpin.com/studio/blog/mobile-navigation-examples/) et [Basic Patterns For Mobile Navigation](https://shop.smashingmagazine.com/2017/05/basic-patterns-mobile-navigation/) | UXPin, Smashing Magazine | 2026 et 2017 | Barre d'onglets 3 à 5 éléments, rail sur tablette, hamburger pour le secondaire |
| 13 | [UX And HTML5: Let's Help Users Fill In Your Mobile Form](https://www.smashingmagazine.com/2018/08/ux-html5-mobile-form-part-1/) et guides de formulaires mobiles de vendeurs | Smashing Magazine et autres | 2018 et plus récent | Une colonne, libellés au-dessus, `inputmode`, étapes courtes |
| 14 | [Accessible Front-End Patterns For Responsive Tables](https://smashingmagazine.com/2022/12/accessible-front-end-patterns-responsive-tables-part2/), [Responsive tables, Sizzy](https://sizzy.co/blog/responsive-tables) | Smashing Magazine, Sizzy | 2022 et non datée | Défilement, empilement en cartes, colonnes prioritaires, lignes dépliables |
| 16 | Résumés secondaires de WCAG 1.4.12 (espacement du texte), 1.3.4 (orientation) et 1.4.4 (taille du texte) | Divers | non datées | Seuils d'espacement du texte, verrouillage d'orientation |

## Limites

- **Modale ou page plein écran** sur mobile : la recherche n'a rien donné de sourcé. Le point est du jugement dans la checklist.
- Les patterns de **navigation** et de **formulaires** viennent de blogs UX. Certains chiffres de vendeurs de formulaires n'ont pas été vérifiés.
- Support navigateur de `interactive-widget` : Chrome 108+ et Firefox 132+ d'après les sources ; **Safari non vérifié**.
- Pour `touch-action`, `scrollbar-gutter` et `text-wrap`, les pages MDN anglaises n'ont pas été lues.
- Seuils WCAG 1.4.12, 1.3.4 : issus de résumés secondaires, à vérifier sur les documents W3C avant toute affirmation de conformité.
- Les breakpoints de navigation cités (1024 et 768 px) sont une suggestion d'une source, pas une norme.
