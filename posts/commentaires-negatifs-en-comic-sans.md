---
title: Afficher les commentaires de troll en Comic Sans
date: 2019-03-07T00:00:00.000Z
summary: >-
  Zach est le créateur d'Elevante (le générateur qui motorise ce blog) et a participé avec joie au dernier indiewebcamp. Fan de générateur de sites statiques comme de polices de caractères, j'envisage d'étudier et traduire son post du 7 juin "Fender Snarky Comments in ComicSans" plus qu'inspirant pour designer et habiller les futures webmentions. Son site personnel motorisé par Eleventy est en outre un modèle du genre pour ce qui concerne l'implémentation du système de webmentions.
tags:
  - post
  - commentaires
  - comicsans
  - eleventy
---
[Source du post en cours d'étude](https://www.zachleat.com/web/snarky/)

J'ai eu le plaisir de participer à un [IndieWebCamp](https://indieweb.org/) avant la merveilleuse conférence  [Beyond Tellerrand](https://beyondtellerrand.com/) il y a quelques semaines et je continue encore à [buzzer](https://twitter.com/zachleat/status/1127489938448977920) de l'expérience.

Je ne parviens pas à vraiment exprimer ce que fut pour moi l’importance de cette expérience. Une antithèse à la course des médias sociaux, IndieWebCamp était une salle remplie d'esprits semblables qui s'intéressent au Web et à leurs propres sites Web et hébergent leur propre contenu. Cela ressemblait aux jours de Google Reader, lorsque tout le monde bloguait et écrivait sur ses propres sites. Je ne sais pas si vous pouvez le dire, mais j'ai adoré. Si vous avez la chance d'assister à l'un de ces événements, sautez dessus (je veux vraiment en organiser un à Omaha 👀).

## WEBMENTIONS, DISQUS, WORDPRESS

Lors de l'événement, j'ai pu installer un exemple fonctionnel de [webmentions](https://indieweb.org/Webmention) sur mon propre site web personnel. J'avais déjà eu [une copie statique des mes vieux commentaires Disqus que j'avais exporté](https://www.zachleat.com/web/disqus-import/) (qui comprenaient des copies de vieux commentaires Wordpress que j'avais importé dans Disqus 😎).

Les webmentions sont rendues possibles pour les sites web statiques quand vous utilisez [webmention.io](https://webmention.io/), un service pour se connecter aux entrées entrantes. Un autre service, [Bridgy](https://brid.gy/), crawle les sites de réseaux sociaux pour les citations de mon site et envoie celles-ci automatiquement sur webmention.io.

Si je vous ai déjà perdu, heureusement [Max Böck a écrit un magnifique tutoriel pour savoir comment faire ça en utilisant Eleventy](https://mxb.dev/blog/using-webmentions-on-static-sites/) (sont site est aussi merveilleux). Max a créé un  [projet de démarrage `eleventy-webmentions`](https://github.com/maxboeck/eleventy-webmentions) qui contient tout le code pour ça. Espérons que nous pourrons également intégrer ce type de contenu fusionné et intégré dans l'upstream `eleventy-base-blog`.

Vous pouvez voir un exemple du fonctionnement des webmentions sur mon site dans l'un de mes articles de blog récents:  [Google Fonts is Adding `font-display`](https://www.zachleat.com/web/google-fonts-display/#webmentions).


## ANALYSE DE SENTIMENT

L'hébergement de mon propre contenu et de mes commentaires me permet d'être un peu plus créatif avec ce contenu. J'ai donc décidé d'aller un peu plus loin et de [m'amuser un peu](https://twitter.com/zachleat/status/1132727088031653891).

Tout d'abord, comment trouver si un commentaire est négatif ? Essayons d'utiliser [Natural, un plugin sur npm](https://www.npmjs.com/package/natural). J'ai ajouté un filtre Liquid à mon [fichier de configuration Eleventy](https://www.11ty.io/docs/config/) pour analyser le texte et cracher une valeur sentiment. `0` est neutre, `< 0` est négatif, et `> 0` est positif. Notez que ce traitement de langage naturel n'est pas fiable à 100% (parfois, je reçois un faux positif) mais c'est juste une démo amusante sur mon site.
    
```
const Natural = require('natural');
const analyze = new Natural.SentimentAnalyzer("English", Natural.PorterStemmer, "afinn");
module.exports = function(eleventyConfig) 
   {  
       eleventyConfig.addLiquidFilter("getSentimentValue", function(content) 
     {        
      if( content ) {            
      const tokenizer = new Natural.WordTokenizer();
      return analyze.getSentiment(tokenizer.tokenize(content));
}     
     return 0;    
  });
};
```

Ensuite dans mon template Liquid, j'utilise cette valeur entière pour l'ajouter à une classe `static-comments-reply-salty` :

```    
{% assign sentiment = webmention.content.text | getSentimentValue %}
<li class="static-comments-reply{% if sentiment < 0 %} static-comments-reply-salty{% endif %}">``
    

Et pour finir dans ma feuille de style, j'utilise cette classe pour ajouter une joli couche de Comic Sans, Chalkboard, et bien sûr un fallback fantasy pour les coups :
    
```
.static-comments-reply-salty {    
         font-family: Comic Sans MS, Chalkboard SE, fantasy;
}


Comme crédit supplémentaire, j'ai aussi utilisé le [plugin `random-case`](https://www.npmjs.com/package/random-case) pour `mODifEr lE TeXte` (sur l'excellente recommdantation de [David Darnes](https://twitter.com/DavidDarnes/status/1132732852196511744)).

## À QUOI ÇA RESSEMBLE ? 

Ceci a été pris à partir d'un véritable commentaire sur mon site.

### AVANT :

![](https://www.gravatar.com/avatar/38e4a1731159a21bbce9890693c81380?d=mm&s=60)

### Jeez Louise DISQUS

_22 Feb 2015 at 12:03PM_

Hey man, you need to fix this or take it down. Don't you see how many people are complaining that it doesn't work?

### APRÈS :

![](https://www.gravatar.com/avatar/38e4a1731159a21bbce9890693c81380?d=mm&s=60)

### Jeez Louise DISQUS

_22 Feb 2015 at 12:03PM_

heY mAN, yOu nEEd TO fix ThIs Or TaKE IT Down. don'T YoU SeE hOw MAnY PeOplE arE cOmPlaIning thAt iT DOEsN't WorK?

Ceci n’est pas destiné à défoncer le Comic Sans. Au lieu de cela, la police est censée changer le ton de la négativité pour donner l’impression qu’un clown est en train de crier à la fête d’anniversaire d’un enfant.  



