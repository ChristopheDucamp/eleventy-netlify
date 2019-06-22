---
title: Construire mon blog à partir de zéro en utilisant Eleventy
date: 2019-06-22T17:00:00.000Z
summary: Traduction en cours d'un tutoriel de prise en mains d'Eleventy à partir de zéro (sans passer par le déploiement automatique Netlify)
tags:
  - post
  - eleventy
---

La ligne de commande vous stresse ? Vous avez les yeux qui piquent une fois de plus a avoir confondu les messages d'erreur et une syntaxe non intuitive ? Ne vous inquiétez pas, c'est monnaie courante. Si vous passez un peu de temps à apprendre à utiliser la ligne de commande, vous pourrez en apprendre davantage sur ces sentiments et débloquer un nouveau niveau de productivité.

Eleventy est un générateur de site statique adapté aux débutants qui s'exécute sur une invite de commande et son utilisation vous rendra plus productif. (*Un générateur de site statique est un programme qui combine des modèles et des données pour créer du HTML.)*  Aujourd'hui, nous allons utiliser Eleventy pour créer un site Web de blog permettant de rédiger notre contenu dans Markdown.

## Project Highlights [#](https://www.filamentgroup.com/lab/build-a-blog/#project-highlights)


Avant de plonger, laissez-moi vous parler un peu des objectifs du projet Eleventy.

Eleventy est flexible. Il veut travailler avec la structure de répertoires de votre projet.

Eleventy est rapide. Eleventy inclut un [benchmark avec 10 000 modèles](https://github.com/11ty/eleventy-benchmark) (12 Ko chacun, 120 Mo au total) qui s'exécute en 17 secondes environ. Cela fait 1,7 ms par modèle.

Eleventy ne vous verrouille pas dans un langage spécifique de modèle. Eleventy fonctionne avec les fichiers HTML, Markdown, Liquid, Nunjucks, Handlebars, Mustache, EJS, HAML et JavaScript. Vous pouvez utiliser un ou plusieurs d'entre eux. Vous pouvez les mélanger ensemble.

Eleventy est doucement itératif. Vous pouvez migrer votre contenu existant lentement pour utiliser Eleventy. Eleventy vous permet de migrer votre contenu vers un nouveau langage de modèle, un modèle à la fois.

Il est utilisé actuellement par [beaucoup de sites cools](https://www.11ty.io/docs/sites/), y compris le site sur lequel vous me lisez en ce moment (NDT [filamentgroup.com](https://www.filamentgroup.com/)) et le site pour le [projet V8 de Google](https://v8.dev/).

## Installation [#](https://www.filamentgroup.com/lab/build-a-blog/#installation)

Mais avant d'aller plus loin, nous devons installer Node. Node est livré sous forme d'un programme installable que vous pouvez   [télécharger sur le web](https://nodejs.org/en/). Profitez de la sécurité de cet installateur graphique et cliquez confortablement sur chaque étape de l'assistant en toute confiance.

Avant de nous endormir dans un faux sentiment de sécurité, enfourchons ce taureau et partons. Nous devons ouvrir notre terminal, notre ligne de commande ou notre fenêtre d'invite de commande. Sur un Mac, cela signifie trouver le fichier `Terminal.app` (généralement dans `/Applications/Utilitaires/Terminal.app`) et l'ouvrir. Sous Windows, cela s'appelle `cmd.exe` (ça se trouve dans le menu Démarrer sous `Démarrer > Programmes > Accessoires> Invite de commandes`).

Assurez-vous que Node soit correctement installé en lançant `node --version`. Eleventy requiert Node 8. Vous saurez si vous avez Node 8 ou supérieur si le premier chiffre après le `v` est supérieur ou égal à 8. Par exemple, si `node --version` renvoie `v8.11.3`, vous avez Node 8.

Pour installer Eleventy, vous devrez entrer la commande suivante dans votre invite de commande et pressez sur la touche retour pour l'exécuter : 
    
    npm install -g @11ty/eleventy

_Pour en savoir plus sur l'[installation locale dans un projet au lieu de globalement](https://www.11ty.io/docs/local-installation/)_

## Faire tourner Eleventy pour la Première Fois [#](https://www.filamentgroup.com/lab/build-a-blog/#running-eleventy-for-the-first-time)

La chose la plus simple sur laquelle Eleventy peut vous aider, c'est de transformer un fichier markdown en HTML. Faites un nouveau répertoire pour notre projet appelé `eleventy-intro`…
    
    mkdir eleventy-intro
    cd eleventy-intro
    

…et créez un nouveau fichier appelé `blog-post.md`. Sauvegardez les contenus suivants dans `blog-post.md`:
    
    # Ceci est mon Titre
      
    Voici un paragraphe de texte.

Maintenant vous pouvez lancer Eleventy :
    
    eleventy
    
    Writing _site/blog-post/index.html from ./blog-post.md.
    Processed 1 file in 0.13 seconds
    

## Transformez-le en HTML Valide [#](https://www.filamentgroup.com/lab/build-a-blog/#make-it-valid-html)

Nous avons transformé avec succès un fichier markdown en HTML. Bravo ! Mais si nous ouvrons ce fichier `_site/blog-post/index.html` pour voir notre output HTML, ce n'est pas du HTML valide.
    
    <h1>Ceci est mon Titre</h1>  
    <p>Voici un paragraphe de texte.</p>

Pour qu'il soit valide sans ajouter un paquet de merde dans notre fichier markdwon, ajoutons un [layout Eleventy](https://www.11ty.io/docs/layouts/). Ceci emballabera un gabarit avec d'autres trucs.

Sauvegardons ces contenus à l'intérieur d'un fichier `_includes/layout.liquid`:
    
    <!doctype html>  
    <html lang="fr">  
        <head>  
            <meta charset="utf-8">  
            <title>Mon Blog</title>  
        </head>  
        <body>  
            <h1>{{ pageTitle }}</h1>  
      
            {{ content }}  
        </body>  
    </html>

Si c'est la première fois que vous voyez un template `liquid` et que vous n'êtes pas à l'aise avec la syntaxe, vous pourrez jeter un oeil sur la [documentation Shopify Liquid](https://shopify.github.io/liquid/) afin d'en savoir plus. Ceci est une idée principale ici : les doubles accolades sont utilisés pour générer une variable (par ex. `{{ pageTitle }}`).

Dans notre exemple de layout nous utilisons `{{ content }}` pour indiquer où ira notre contenu dans le template markdown.

Maintnenat nous devons dire à notre fichier `blog-post.md` d'utiliser le layout. Ajoutons quelque chose en haut de notre fichier pour faire simplement ça : 
    
    ---  
    layout: layout.liquid  
    ---  
    # Ceci est un mon Titre
      
    Voici un paragraphe de texte.

Cette section entre (et incluant) les deux marques `---` est appelée le [Front Matter YAML](https://www.11ty.io/docs/data-frontmatter/). C'est un moyen d'écrire des données dans notre fichier de modèle que les modèles de Liquid peuvent utiliser. Si vous avez utilisé Jekyll, cela peut vous paraître familier.

La clé `layout` indique à Eleventy de rechercher des fichiers dans le dossier `_includes` pour envelopper le contenu du modèle. Plus précisément, nous souhaitons que notre article de blog utilise le fichier `_includes/layout.liquid` comme enveloppe de layout.

Maintenant, déplaçons notre titre dans notre texte `pageTitle` afin qu’il puisse être utilisé dans notre fichier de présentation. Maintenant notre `blog-post.md` ressemble à ceci :
    
    ---  
    layout: layout.liquid  
    pageTitle: Ceci est mon Titre
    ---  
    Voici un paragraphe de texte.

Lançons de nouveau Eleventy pour génrer notre output :
    
    eleventy

Ouvrez le fichier output `_site/blog-post/index.html` pour voir ce qui s'est passé : 
    
    <!doctype html>  
    <html lang="fr">  
        <head>  
            <meta charset="utf-8">  
            <title>Mon Blog</title>  
        </head>  
        <body>  
            <h1>Ceci est mon Titre</h1>  
            <p>Voici un paragraphe de texte.</p>  
        </body>  
    </html>

## Appliquer Automatiquement les Changements [#](https://www.filamentgroup.com/lab/build-a-blog/#apply-changes-automatically)

It will be tiring to re-run Eleventy every time we make a change. Let’s use `--serve` to run a hot-reloading local web server that will apply our changes automatically when you save.
    
    eleventy --serve

Your command prompt will tell you what URL to navigate to but the default is: [`http://localhost:8080/blog-post/`](http://localhost:8080/blog-post/)

Try editing our `blog-post.md` file and saving it. Eleventy will run automatically _and_ the browser window will refresh automatically when it’s done.

## Produisons un Blog! [#](https://www.filamentgroup.com/lab/build-a-blog/#let%E2%80%99s-make-a-blog!)

Why not? We’re actually pretty close to making a simple blog! Let’s take it a little further, shall we? Let’s make a `posts` folder for our blog posts and move our `blog-post.md` file in there. Then add a `posts/posts.json` file with the following content:
    
    {  
        "layout": "layout.liquid"  
    }

Instead of requiring us to edit everything in our `posts` folder using YAML Front Matter, this data file will apply the data inside to all of the files in our `posts` folder. This will work for any `.json` file name that matches its parent folder name (e.g. `posts/posts.json` or `pictures/pictures.json`). Read more about [Template and Directory Data Files](https://www.11ty.io/docs/data-template-dir/). If you use both data files and front matter, any duplicate keys in the front matter will take precedence over the data file entries.

Now try making another blog post in `posts/blog-post-2.md`:
    
    ---  
    pageTitle: This is my other Title  
    ---  
    This is another paragraph of text.

Our `layout` is being applied from `posts/posts.json` so we don’t need that in our front matter any more. We do want a `pageTitle` though!

Is our server still applying changes automatically? If so, check out our new blog post at [`http://localhost:8080/posts/blog-post-2/`](http://localhost:8080/posts/blog-post-2/). Our old post should now live at [`http://localhost:8080/posts/blog-post/`](http://localhost:8080/posts/blog-post/).

### Finisson par une Page d'Accueil [#](https://www.filamentgroup.com/lab/build-a-blog/#finish-with-a-home-page)

Doing great so far. We have two blog posts. But if we go to the root of our site (`http://localhost:8080/`) there’s nothing there! Let’s add a home page that lists all of our lovely blog posts.

Open up your `posts/posts.json` and add a `tags` array to our posts data:
    
    {  
        "layout": "layout.liquid",  
        "tags": ["posts"]  
    }

Any time you use `tags`, Eleventy will make a new collection of all the pieces of content that use the same tag. Now our blog posts will be available as a collection, specifically under the data `collections.posts`. Read more about [Eleventy Collections](https://www.11ty.io/docs/collections/).

Let’s make an `index.html` to show you what I mean:
    
    ---  
    layout: layout.liquid  
    pageTitle: Welcome to my blog  
    ---  
    {% for post in collections.posts %}  
        <h2><a href="{{ post.url }}">{{ post.data.pageTitle }}</a></h2>  
        <em>{{ post.date | date: "%Y-%m-%d" }}</em>  
    {% endfor %}

  1. Front matter: We’re using the same `layout` and assigning a `pageTitle` used in the layout file.
  2. Iterate over our blog posts collection using the Liquid `for` tag (note the new syntax using `%`’s): `{% for post in collections.posts %}` Read more about [Liquid `for` tags](https://shopify.github.io/liquid/tags/iteration/#for).
  3. `post.url` has the URL string of each blog post entry.
  4. `post.data` has all the data (from all data sources including front matter and data files) used in each blog post (e.g. `post.data.pageTitle`)
  5. `post.date` has each blog post’s file creation date. (Read more about [Content Dates](https://www.11ty.io/docs/dates/))

This outputs the following:
    
    <!doctype html>  
    <html lang="fr">  
        <head>  
            <meta charset="utf-8">  
            <title>My Blog</title>  
        </head>  
        <body>  
            <h1>Welcome to my blog</h1>  
      
            <h2><a href="/posts/blog-post/">This is my Title</a></h2>  
            <em>2018-12-28</em>  
      
            <h2><a href="/posts/blog-post-2/">This is my Title 2</a></h2>  
            <em>2018-12-28</em>  
        </body>  
    </html>

You did it! It’s a blog!

To take this a bit further, check out the [`eleventy-base-blog` project](https://github.com/11ty/eleventy-base-blog), which is a full starter project for a blog site including RSS feeds, tag pages, syntax highlighting, custom markdown plugins, and more!

## Posons-le sur le web ! [#](https://www.filamentgroup.com/lab/build-a-blog/#put-it-on-the-web!)

You can use Netlify to very quickly put this on the web. Register and/or Log in to [`app.netlify.com`](https://app.netlify.com/) and drag and drop our `_site` folder onto the web browser window to upload the contents live to the web!

It happens almost instantly.

Check out our [simple blog demo](https://modest-colden-60bed7.netlify.com/) on Netlify.

## Go forth and Eleventy [#](https://www.filamentgroup.com/lab/build-a-blog/#go-forth-and-eleventy)

Read more at the [official Eleventy documentation](https://www.11ty.io/docs/).

But most importantly, don’t forget to send us a link to your new blog! Hit us up on Twitter [@filamentgroup](https://twitter.com/filamentgroup) with any feedback!

  

