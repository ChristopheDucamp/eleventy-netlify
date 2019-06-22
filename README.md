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

[![Déployer vers Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/danurbanowicz/eleventy-netlify-boilerplate&stack=cms)

Cliquer sur le bouton au-dessous déploiera une copie du site web de démo sur votre compte Netlify (vous pouvez créer un compte durant ce processus si vous n'en avez pas déjà un) et tout ce qui est exigé pour faire fonctionner le CMS : 

* Un nouveau dépôt dans votre compte GitHub avec le code 
* Un Déploiement Complet Continu sur le réseau global CDN de Netlify
* Le contrôle des utilisateurs et l'accès à l'Identité Netlify
* La gestion de contenu avec le CMS Netlify
* Les formulaires de traitement de données avec Netlify Forms

### Authentification d'Installation

Après avoir déployé ce projet, Netlify Identity vous ajoutera comme un utilisateur du CMS et vous enverra une invitation.
Il n'est pas nécessaire d'accepter cette inviation si vous souhaitez utiliser un [fournisseur OAuth](https://www.netlify.com/docs/identity/#external-provider-login)
(par ex. Github) pour gérer l'authentification à votre CMS.
Il est recommandé d'utiliser cette méthode d'authentification car elle retire le besoin d'avoir un e-mail et un mot de passe pour se connecter au CMS et elle est plus sécurisée. Vous devrez ajouter un fournisseur OAuth dans vos réglages de l'app Netlify sous 
"Settings" > "Identity" > "External providers".

Une fois votre fournisseur OAuth ajouté, naviguer vers `/admin` sur votre site, sélectionnez votre fournisseur à partir de la liste, et vous devriez être ensuite connecté à votre CSM. Cool non ?

Maintenant que tout est paramétré, vous pouvez commencer à modifier le contenu ! 

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
