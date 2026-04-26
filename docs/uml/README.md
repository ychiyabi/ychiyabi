# Diagrammes UML Mermaid

Cette section regroupe les diagrammes UML du projet au format **Mermaid** ainsi que leurs rendus **SVG** afin de pouvoir :

- les versionner facilement dans Git
- les relire en texte brut
- les convertir ensuite en image pour le rapport Word

## Fichiers disponibles

- [`use-case.md`](./use-case.md) et `use-case.mmd` : diagramme de cas d'utilisation global
- [`class-diagram.md`](./class-diagram.md) et `class-diagram.mmd` : diagramme de classes du domaine principal
- [`sequence-diagram.md`](./sequence-diagram.md), `sequence-auth.mmd`, `sequence-ml.mmd` : diagrammes de sequence representatifs
- `*.svg` : rendus dessines exportes depuis Mermaid

## Conseils d'utilisation

- les fichiers `.mmd` servent de source Mermaid brute
- les fichiers `.svg` sont les diagrammes dessines avec des lignes de relation visibles
- Pour inserer les diagrammes dans le rapport, vous pouvez :
  - soit utiliser directement les SVG generes
  - soit modifier les `.mmd` puis regenerer les SVG
- Les diagrammes ont ete alignes sur l'etat actuel du projet `stock-api`, `stock-web` et `stock-mobile`.
