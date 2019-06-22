---
title: Construire mon blog à partir de zéro en utilisant Eleventy
date: 2019-06-22T17:00:00.000Z
summary: 


tags:
  - post
  - indieweb
  - eleventy
---

La ligne de commande vous stresse ? Vous avez les yeux qui piquent une fois de plus a avoir confondu les messages d'erreur et une syntaxe non intuitive ? Ne vous inquiétez pas, c'est monnaie courante. Si vous passez un peu de temps à apprendre à utiliser la ligne de commande, vous pourrez en apprendre davantage sur ces sentiments et débloquer un nouveau niveau de productivité.

Eleventy est un générateur de site statique adapté aux débutants qui s'exécute sur une invite de commande et son utilisation vous rendra plus productif. (*Un générateur de site statique est un programme qui combine des modèles et des données pour créer du HTML.)*  Aujourd'hui, nous allons utiliser Eleventy pour créer un site Web de blog permettant de rédiger notre contenu dans Markdown.

## Project Highlights [#](https://www.filamentgroup.com/lab/build-a-blog/#project-highlights)

Before we dive in, let me tell you a little bit about Eleventy’s project goals.

Eleventy is flexible. It wants to work with your project’s directory structure.

Eleventy is fast. Eleventy includes a [benchmark with 10,000 templates](https://github.com/11ty/eleventy-benchmark) (12KB each, 120MB total) that runs in about 17 seconds. That’s 1.7ms per template.

Eleventy doesn’t lock you into one specific template language. Out of the box, Eleventy works with HTML, Markdown, Liquid, Nunjucks, Handlebars, Mustache, EJS, HAML, and JavaScript files. You can use one or more of these. You can mix them together.

Eleventy is gently iterative. You can migrate your existing content slowly over to use Eleventy. You can use Eleventy to migrate your content to a new template language, one template at a time.

It’s being used by [lots of cool sites](https://www.11ty.io/docs/sites/), including the very site you’re reading right now ([filamentgroup.com](https://www.filamentgroup.com/)) and the site for [Google’s V8 project](https://v8.dev/).

## Installation [#](https://www.filamentgroup.com/lab/build-a-blog/#installation)

But before we get too far along we need to have Node installed. Node comes as an installable program you can [download from the web](https://nodejs.org/en/). Bask in the safety of this GUI installer and comfortably click through each wizard step with confidence.

Before we lull ourselves into a false sense of security, let’s hop on this bull and ride. We need to open our terminal, command line, or command prompt window. On a Mac this means finding the `Terminal.app` (usually in `/Applications/Utilities/Terminal.app`) and opening it. On Windows this is called `cmd.exe` (found in the Start Menu under `Start > Program Files > Accessories > Command Prompt`).

Make sure Node is installed correctly by running `node --version`. Eleventy requires Node 8. You’ll know if you have Node 8 or higher if the first number after the `v` is greater than or equal to 8. For example, if `node --version` returns `v8.11.3`, you have Node 8.

To install Eleventy, you’ll need to enter the following command in your command prompt and press enter to execute it:
    
    npm install -g @11ty/eleventy

_Read more about [installing locally in a project instead of globally](https://www.11ty.io/docs/local-installation/)_

## Running Eleventy for the First Time [#](https://www.filamentgroup.com/lab/build-a-blog/#running-eleventy-for-the-first-time)

The simplest thing that Eleventy can help you do is transform a markdown file into HTML. Make a new directory for our project called `eleventy-intro`…
    
    mkdir eleventy-intro
    cd eleventy-intro
    

…and create a new file called `blog-post.md`. Save the following contents in `blog-post.md`:
    
    # This is my Title  
      
    This is a paragraph of text.

Now you can run Eleventy:
    
    eleventy
    
    Writing _site/blog-post/index.html from ./blog-post.md.
    Processed 1 file in 0.13 seconds
    

## Make it Valid HTML [#](https://www.filamentgroup.com/lab/build-a-blog/#make-it-valid-html)

We’ve successfully transformed a markdown file into HTML. Congratulations! But if we open that file `_site/blog-post/index.html`to see our HTML output—it’s not valid HTML.
    
    <h1>This is my Title</h1>  
    <p>This is a paragraph of text.</p>

To make it valid without adding a bunch of junk inside of our markdown file, let’s add an [Eleventy layout](https://www.11ty.io/docs/layouts/). This will wrap a template with other stuff.

Save these contents into `_includes/layout.liquid`:
    
    <!doctype html>  
    <html lang="en">  
        <head>  
            <meta charset="utf-8">  
            <title>My Blog</title>  
        </head>  
        <body>  
            <h1>{{ pageTitle }}</h1>  
      
            {{ content }}  
        </body>  
    </html>

If this is the first time you’ve seen a `liquid` template and are not familiar with the syntax, you may want to take a second and head over to the [Shopify Liquid documentation](https://shopify.github.io/liquid/) to learn more. There is one main idea on display here: Double curly braces are used to output a variable (e.g. `{{ pageTitle }}`).

In our layout example we use `{{ content }}` to denote where our markdown template content will go.

Now we need to tell our `blog-post.md` file to use the layout. Let’s add something to the top of our file to do just that:
    
    ---  
    layout: layout.liquid  
    ---  
    # This is my Title  
      
    This is a paragraph of text.

This section between (and including) the two `---` marks is called [YAML Front Matter](https://www.11ty.io/docs/data-frontmatter/). It’s a way to write data into our template file that can be used by Liquid templates. If you’ve used Jekyll this may look familiar.

The `layout` key tells Eleventy to look for files inside of the `_includes`folder to wrap around the content of the template. Specifically, we want our blog post to use the `_includes/layout.liquid` file as a wrapper layout.

Now, let’s move our title text into our `pageTitle` front matter so that it can be used in our layout file. Now our `blog-post.md` looks like this:
    
    ---  
    layout: layout.liquid  
    pageTitle: This is my Title  
    ---  
    This is a paragraph of text.

Let’s run Eleventy again to generate our output:
    
    eleventy

Open the output file at `_site/blog-post/index.html` to see what happened:
    
    <!doctype html>  
    <html lang="en">  
        <head>  
            <meta charset="utf-8">  
            <title>My Blog</title>  
        </head>  
        <body>  
            <h1>This is my Title</h1>  
            <p>This is a paragraph of text.</p>  
        </body>  
    </html>

## Apply Changes Automatically [#](https://www.filamentgroup.com/lab/build-a-blog/#apply-changes-automatically)

It will be tiring to re-run Eleventy every time we make a change. Let’s use `--serve` to run a hot-reloading local web server that will apply our changes automatically when you save.
    
    eleventy --serve

Your command prompt will tell you what URL to navigate to but the default is: [`http://localhost:8080/blog-post/`](http://localhost:8080/blog-post/)

Try editing our `blog-post.md` file and saving it. Eleventy will run automatically _and_ the browser window will refresh automatically when it’s done.

## Let’s make a Blog! [#](https://www.filamentgroup.com/lab/build-a-blog/#let%E2%80%99s-make-a-blog!)

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

### Finish with a Home Page [#](https://www.filamentgroup.com/lab/build-a-blog/#finish-with-a-home-page)

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
    <html lang="en">  
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

## Put it on the web! [#](https://www.filamentgroup.com/lab/build-a-blog/#put-it-on-the-web!)

You can use Netlify to very quickly put this on the web. Register and/or Log in to [`app.netlify.com`](https://app.netlify.com/) and drag and drop our `_site` folder onto the web browser window to upload the contents live to the web!

It happens almost instantly.

Check out our [simple blog demo](https://modest-colden-60bed7.netlify.com/) on Netlify.

## Go forth and Eleventy [#](https://www.filamentgroup.com/lab/build-a-blog/#go-forth-and-eleventy)

Read more at the [official Eleventy documentation](https://www.11ty.io/docs/).

But most importantly, don’t forget to send us a link to your new blog! Hit us up on Twitter [@filamentgroup](https://twitter.com/filamentgroup) with any feedback!

  

