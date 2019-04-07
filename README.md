[![Statut Netlify](https://api.netlify.com/api/v1/badges/bbf28a84-4bdb-407b-a2fa-32628d27fa3d/deploy-status)](https://app.netlify.com/sites/eleventy-netlify-boilerplate/deploys)

# Eleventy Netlify Boilerplate

## Qu'est-ce que c'est ?

Un modèle simple pour créer un site web rapide et statique à l'aide du générateur de site statique [Eleventy](https://www.11ty.io/), avec [Netlify CMS](https://www.netlifycms.org/) intégré, prêt à être déployé en quelques clics sur [Netlify](https://www.netlify.com).

Utilisez-le comme un démarrage pour vos propres projets ou comme un moyen rapide pour commencer à construire des sites web avec Eleventy.

Basé sur le repo du [Blog de Base Eleventy](https://github.com/11ty/eleventy-base-blog) (voir là l'info supplémentaire sur l'usage d'Eleventy).

🔥 **Ce projet est mis en avant sur la [vitrine de modèles](https://templates.netlify.com/template/eleventy-netlify-boilerplate/) de Netlify** 🔥

## [Site de démo](https://eleventy-netlify-boilerplate.netlify.com//)

## Fonctionnalités

* Pages échantillons et blog avec support du tag
* Netlify CMS avec prévisualisation dans l'éditeur (merci  [@biilmann](https://github.com/biilmann)!)
* CSS 2kb minifiée, dans la ligne pour une restitution de page plus rapide
* Pre-builds et minimise votre HTML
* layout responsive CSS Grid, avec fallbacks (voir [Suppor Navigateur](#browser-support))
* Utilise les fichiers Markdown files pour le contenu
* Utilise les modèles Liquid et/ou Nunjucks pour le layout
* 100% Javascript framework free
* Optional pipeline for minified inline JS
* Continuous Deployment workflow via Netlify

## Vous voulez l'essayer dès maintenant ?

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/danurbanowicz/eleventy-netlify-boilerplate&stack=cms)

Clicking the button above will deploy a copy of the demo website to your Netlify
account (you can create an account during this process if you don't have one)
and everything needed for running the CMS:

* A new repository in your GitHub account with the code
* Full Continuous Deployment to Netlify's global CDN network
* Control users and access with Netlify Identity
* Manage content with Netlify CMS
* Process form data with Netlify Forms

### Authentification d'Installation

After deploying this project, Netlify Identity will add you as a CMS user and
will email you an invite. It is not necessary to accept this invite if you wish
to use an
[OAuth provider](https://www.netlify.com/docs/identity/#external-provider-login)
(e.g. Github) to manage authentication for your CMS.
It is recommended to use this method of authentication as it removes the need
for an email & password to log in to the CMS and is generally more secure. You
will need to add an OAuth provider in your Netlify app settings under
"Settings" > "Identity" > "External providers".

Once you've added an OAuth provider, navigate to `/admin` on your site, select your provider from the
list, and you should then be logged into your CMS. Cool huh?

Now you're all set, and you can start editing content!

## Gotchas

If you change the repo that was created at deploy time from public to private, you'll need to regenerate your token,
as the token generated using the deploy to Netlify button can only access public repositories. To
regenerate your token, head to "Settings" in your Netlify site dashboard, go to the "Identity"
section, then scroll to "Services" where you'll see an "Edit settings" button. Click that and you'll
see a text link to "Generate access token in GitHub".

If you need any help with setting up Netlify CMS, you can reach out to the Netlify team in the [Netlify CMS Gitter](https://gitter.im/netlify/netlifycms).

## Développement Local

### 1. Clonez ce repository :

```
git clone https://github.com/danurbanowicz/eleventy-netlify-boilerplate.git my-blog-name
```


### 2. Naviguez vers le répertoire 

```
cd my-blog-name
```

Specifically have a look at `.eleventy.js` to see if you want to configure any Eleventy options differently.

### 3. Installez les dépendances

```
npm install
```

### 4. Editez _data/metadata.json

This file contains your site title and author details.

### 5. Lancez Eleventy (construit le site)

```
npx eleventy
```

Or build automatically when a template changes:
```
npx eleventy --watch
```

Or in debug mode:
```
DEBUG=* npx eleventy
```

## Bug reports, feature requests, etc

This is an ongoing project and I welcome contributions. Feel free to submit a PR.

If you need any help with setting up Netlify CMS, you can reach out to the Netlify team in the [Netlify CMS Gitter](https://gitter.im/netlify/netlifycms).
