---
title: Notes d'Implémentation
summary: Implémenter 
date: 2019-06-22
tags:
  - eleventy
  - statique
  - blog
  - post 
---

- `about/index.md` montre comment ajouter une page de contenu
- posts/ contient les articles de blog mais ils peuvent vivre dans n'importe quel répertoire. Vous n'avez besoin que d'ajouter le tag post pour qu'il soit rajouté à la collection
- Ajoutez le tag nav pour ajouter un template au niveau le plus  haut de navigation du site. Par exemple, ceci est utilisé sur  index.njk et about/index.md.
- Le contenu peut être dans n'importe quel format de modèle, (les posts de blog n'ont pas besoin par exemple d'être en markdown). Configurez vos modèles supporté dans `.eleventy.js -> templateFormats`.
- Parce css et png sont listés dans templateFormats mais ne sont pas types de template supportés, tous les fichiers avec ces extensions seront copiés sans modification à l'output (tout en conservant la structure du répertoire).
- Le template de feed d'article de blog est dans feed/feed.njk. C'est aussi un bon exemple d'utiliser dedans des fichiers globaux de data qui utilisen _data/metadata.json.

Cet exemple utilise trois layouts :
_includes/layouts/base.njk : la structure HTML au niveau le plus haut
_includes/layouts/home.njk: le template de page d'accueil (emballé dans base.njk)
_includes/layouts/post.njk: le template d'article de blog (emballé dans base.njk)
_includes/postlist.njk est un include Nunjucks et c'est un composant réutilisable utilisé pour affichier une liste de tous les posts. index.njk a un exemplle sur la façon de l'utiliser.