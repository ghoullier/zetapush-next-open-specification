
# Objectifs

- Un développeur front doit pouvoir comprendre les services ZetaPush et leurs intéractions.

Les profils utilisés sont définis dans [commun.md](./commun.md).

***

# Pré-requis

- J'ai un compte sur ZetaPush
- J'ai une application front qui utilise le SDK ZetaPush

![Développement](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/dev-front-interaction-services-zetapush.html)

***

# <a name="parcours-1"></a> Parcours 1 : Je développe une application front avec ZetaPush sans service custom


## ETQ dev front je souhaite utiliser les services ZetaPush


*GIVEN*
  - J'ai un compte ZetaPush
  - J'ai une application connectée au SDK ZetaPush
  - J'ai un ficher monService.js qui expose des méthodes d'API pour mon application front 
  
*WHEN*
  - J'ajoute monService.js à mon App via la console zetapush
  - J'upload monService.js sur mon environment applicatif souhaiter

*THEN*
  - Je peux appeller les verbes d'API de mon service déployer depuis mon application front
  

***

# <a name="parcours-2"></a> Parcours 2 : Je développe une application avec ZetaPush et des services custom

## ETQ dev front je souhaite utiliser les services custom ZetaPush
  

*GIVEN*
  - J'ai un compte ZetaPush
  - J'ai une application connectée au SDK ZetaPush
  
*WHEN*
  - J'ajoute un service à mon App via la console zetapush
  - Je récupére le code d'API du service géneré et l'ajoute en dépendance de mon application front

*THEN*
  - Je peux appeller les verbes d'API du service que je vient de déclarer


***

# <a name="parcours-3"></a> Parcours 3 : Mon équipe développe une application front avec ZetaPush sans services custom

## ETQ équipe de dev front, nous souhaitons utiliser les services ZetaPush


  


***

# <a name="parcours-4"></a> Parcours 4 : Mon équipe développe une application avec ZetaPush et des services custom

## ETQ équipe de dev front, nous souhaitons utiliser les services custom ZetaPush

  


