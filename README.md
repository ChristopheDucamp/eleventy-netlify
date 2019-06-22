[![Statut Netlify](https://api.netlify.com/api/v1/badges/bbf28a84-4bdb-407b-a2fa-32628d27fa3d/deploy-status)](https://app.netlify.com/sites/eleventy-netlify-boilerplate/deploys)

# Paquet de Code Eleventy Netlify

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

Si vous changez le repo qui a été créé au moment du déploiement de public vers privé, vous devrez regénérer votre token, car le token généré en utilisant le bouton Netlify ne peut accéder qu'à des repos publics. Pour regenérer votre token, rendez-vous dans les "Settings" de votre tableau de bord Netlify, et allez sur la section "Identity", puis descendez vers "Services" où vous verrez un bouton "Edit settings". Cliquez dessus et vous verre un lien texte pour "Generate access token in GitHub".

Si vous avez besoin de toute aide pour paramtétrer le CMS Netlify, vous pouvez joindre l'équipe Netlify dans le gitter CMS](https://gitter.im/netlify/netlifycms).

## Développement Local

### 1. Clonez ce repository :

```
git clone https://github.com/danurbanowicz/eleventy-netlify-boilerplate.git mon-nom-de-blog
```


### 2. Naviguez vers le répertoire 

```
cd mon-nom-de-blog
```

Jetez un oeil spécifiquement sur `.eleventy.js` pour voir si vous voulez configurer différemment toutes les options Eleventy.

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

Ou construisez automatiquement quand un template est modifié :
```
npx eleventy --watch
```

Ou en mode debug :
```
DEBUG=* npx eleventy
```

## Rapports de Bug, demandes de fonctionnalités, etc

Ceci est un projet en cours et les contributions sont bienvenues. Sentez-vous libre de proposer une PR.

Si vous avez besoin de toute aide pour paramtétrer le CMS Netlify, vous pouvez joindre l'équipe Netlify dans le gitter CMS](https://gitter.im/netlify/netlifycms).
