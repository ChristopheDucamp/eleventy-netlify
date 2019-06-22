---
title: les commentaires de troll en comics sans ?
date: 2019-03-07T00:00:00.000Z
summary: >-
  Zach a participé avec joie au dernier indiewebcamp. Fan de générateur de sites
  statiques et de polices de caractères, j'envisage d'étudier et traduire son
  post du 7 juin "Fender Snarky Comments in ComicSans". Son site personnel
  motorisé par Eleventy est en outre un modèle d'implémentation du système de
  webmentions.
tags:
  - post
  - commentaires
  - comicsans
  - eleventy
---
[Source du post en cours d'étude](https://www.zachleat.com/web/snarky/)

J'aie eu le plaisir de participer à un [IndieWebCamp](https://indieweb.org/) avant la merveilleuse conférence  [Beyond Tellerrand](https://beyondtellerrand.com/) il y a quelques semaines et je continue encore à [buzzer](https://twitter.com/zachleat/status/1127489938448977920) de l'expérience.

Je ne parviens pas à vraiment exprimer ce que fut pour moi l’importance de cette expérience. Une antithèse à la course des médias sociaux, IndieWebCamp était une salle remplie d'esprits semblables qui s'intéressent au Web et à leurs propres sites Web et hébergent leur propre contenu. Cela ressemblait aux jours de Google Reader, lorsque tout le monde bloguait et écrivait sur ses propres sites. Je ne sais pas si vous pouvez le dire, mais j'ai adoré. Si vous avez la chance d'assister à l'un de ces événements, sautez dessus (je veux vraiment en organiser un à Omaha 👀).

## WEBMENTIONS, DISQUS, WORDPRESS

Lors de l'événement, j'ai pu installer un exemple fonctionnel de [webmentions](https://indieweb.org/Webmention) sur mon propre site web personnel. J'avais déjà eu [une copie statique des mes vieux commentaires Disqus que j'avais exporté](https://www.zachleat.com/web/disqus-import/) (qui comprenaient des copies de vieux commentaires Wordpress que j'avais importé dans Disqus 😎).

Les webmentions sont rendues possibles pour les sites web statiques quand vous utilisez [webmention.io](https://webmention.io/), un service pour se connecter aux entrées entrantes. Un autre service, [Bridgy](https://brid.gy/), crawle les sites de réseaux sociaux pour les citations de mon site et envoie celles-ci automatiquement sur webmention.io.

Si je vous ai déjà perdu, heureusement [Max Böck a écrit un magnifique tutoriel pour savoir comment faire ça en utilisant Eleventy](https://mxb.dev/blog/using-webmentions-on-static-sites/) (sont site est aussi merveilleux). Max a créé un  [projet de démarrage `eleventy-webmentions`](https://github.com/maxboeck/eleventy-webmentions) qui contient tout le code pour ça. Espérons que nous pourrons également intégrer ce type de contenu fusionné et intégré dans l'upstream `eleventy-base-blog`.

Vous pouvez voir un exemple du fonctionnement des webmentions sur mon site dans l'un de mes articles de blog récents:  [Google Fonts is Adding `font-display`](https://www.zachleat.com/web/google-fonts-display/#webmentions).


## ANALYSE DE SENTIMENT

Hosting my own content and comments allows me to be a bit more creative with it. So I decided to take this a step further and have [a little fun](https://twitter.com/zachleat/status/1132727088031653891) with negative comments.

First, how do we find out if a comment is negative? Let’s try to use [Natural, a plugin on npm](https://www.npmjs.com/package/natural). I added a Liquid filter to my [Eleventy configuration file](https://www.11ty.io/docs/config/) to analyze text and spit out a sentiment value. `0` is neutral, `< 0` is negative, and `> 0` is positive. Note that this natural language processing isn’t 100% (sometimes I’ll get a false positive) but this is just a fun demo on my site.
    
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

And then in my Liquid template, I use this integer value to add a `static-comments-reply-salty` class:

```    
{% assign sentiment = webmention.content.text | getSentimentValue %}
<li class="static-comments-reply{% if sentiment < 0 %} static-comments-reply-salty{% endif %}">
        …
    

And then in my stylesheet, I use this class to opt-into a lovely stack of Comic Sans, Chalkboard, and of course a fantasy fallback for kicks:
    
```
.static-comments-reply-salty {    font-family: Comic Sans MS, Chalkboard SE, fantasy;}


As extra credit, I also used the [`random-case` plugin](https://www.npmjs.com/package/random-case) to `mODifY tHe TeXt` (at [David Darnes excellent recommendation](https://twitter.com/DavidDarnes/status/1132732852196511744)).

## HOW DOES IT LOOK?

This was taken from a real comment on my site.

### AVANT :

  1. ![](https://www.gravatar.com/avatar/38e4a1731159a21bbce9890693c81380?d=mm&s=60)

### Jeez Louise DISQUS

_22 Feb 2015 at 12:03PM_

Hey man, you need to fix this or take it down. Don't you see how many people are complaining that it doesn't work?

### APRÈS :

  1. ![](https://www.gravatar.com/avatar/38e4a1731159a21bbce9890693c81380?d=mm&s=60)

### Jeez Louise DISQUS

_22 Feb 2015 at 12:03PM_

heY mAN, yOu nEEd TO fix ThIs Or TaKE IT Down. don'T YoU SeE hOw MAnY PeOplE arE cOmPlaIning thAt iT DOEsN't WorK?

This isn’t intended to be a hot-take on Comic Sans. Instead it’s meant to change the tone of the negativity to make it sound like a clown is yelling at a kid’s birthday party.

  



