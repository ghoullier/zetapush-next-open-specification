# Objectifs

- Un développeur front doit pouvoir utiliser les services ZetaPush dans son front.
- Un développeur full-stack doit pouvoir utiliser les services ZetaPush dans son front et coder son propre métier pour simplifier le développement de son/ses front(s).

Les profils utilisés sont définis dans [commun.md](./commun.md).

# Pré-requis

J'utilise mon éditeur de texte ou IDE préféré.
Je créé une nouvelle application front avec mon framework préféré (Angular, React, Vue, ...).


# <a name="parcours-1"></a> Parcours 1 : Je développe une application front avec ZetaPush sans service custom


## User stories

### ETQ dev front je créé ma première application from scratch avec les outils du standard du web


*GIVEN*
  - J'ai un gestionnaire de package installé (npm ou yarn par exemple)
  - J'ai un début d'application front (au moins le package.json)
  
*WHEN*
  - Lorsque j'ajoute la dépendance au SDK JavaScript ZetaPush, exemple:
  ```npm i --save zetapush-js```

*THEN*
  - Je peux dès à présent faire des appels sur ZetaPush
  - Un compte a été automatiquement créé pour moi avec un espace pour mon application
  - Je connais l'identifiant de mon application et les credentials ZetaPush
  - Mon application est configurée avec cet identifiant
  - Je suis alerté que l'application automatiquement créée sur ZetaPush est valable X jours
  - Je peux me connecter avec les credentials auto-générés par ZetaPush pour transformer mon application temporaire en application permanente et choisir mes vrais identifiants

### ETQ dev front je créé ma première application via la CLI

*GIVEN*
  - J'ai un gestionnaire de package installé (npm ou yarn par exemple)
  - J'ai installé la CLI ZetaPush (via npm ou yarn)

*WHEN*
  - Lorsque que j'initialise un nouveau projet front exemple:
  ```$> zeta new --front ```

*THEN*
  - J'ai une application front minimaliste avec package.json
  - Je peux dès à présent faire des appels sur ZetaPush
  - Un compte a été automatiquement créé pour moi avec un espace pour mon application
  - Je connais l'identifiant de mon application et les credentials ZetaPush
  - Mon application est configurée avec cet identifiant
  - Je suis alerté que l'application automatiquement créée sur ZetaPush est valable X jours
  - Je peux me connecter avec les credentials auto-générés par ZetaPush pour transformer mon application temporaire en application permanente et choisir mes vrais identifiants
- J'ai un exemple de service type hello_world() dans mon front 
### ETQ dev front je souhait ajouter des services ZetaPush à une application front existante

*GIVEN*
  - J'ai un gestionnaire de package installé (npm ou yarn par exemple)
  - Mon application front contient un package.json

*WHEN*
  - Lorsque que j'installe zetapush-js:
  ```npm i --save zetapush-js```

*THEN*
  - Je peux dès à présent faire des appels sur ZetaPush
  - Un compte a été automatiquement créé pour moi avec un espace pour mon application
  - Je connais l'identifiant de mon application et les credentials ZetaPush
  - Mon application est configurée avec cet identifiant
  - Je suis alerté que l'application automatiquement créée sur ZetaPush est valable X jours
  - Je peux me connecter avec les credentials auto-générés par ZetaPush pour transformer mon application temporaire en application permanente et choisir mes vrais identifiants


# <a name="parcours-2"></a> Parcours 2 : Je développe une application front avec ZetaPush avec service custom

## User stories

### ETQ dev front je créé ma première application from scratch avec les outils du standard du web

*GIVEN*
  - J'ai un gestionnaire de package installé (npm ou yarn par exemple)
  - J'ai un début d'application front (au moins le package.json)
  - J'ai un début d'application backend Node (au moins le package.json)
  
*WHEN*
  - Lorsque j'ajoute la dépendance au SDK JavaScript ZetaPush dans mon front, exemple:
  ```npm i --save zetapush-js```
  - Lorsque j'ajoute la dépendance au SDK Custom ZetaPush dans mon back, exemple:
  ```npm i --save zetapush-custom``` TODO: trouver mieux que ZetaPush-custom

*THEN*
  - Je peux dès à présent faire des appels sur ZetaPush
  - Un compte a été automatiquement créé pour moi avec un espace pour mon application
  - Je connais l'identifiant de mon application et les credentials ZetaPush
  - Mon application est configurée avec cet identifiant
  - Je suis alerté que l'application automatiquement créée sur ZetaPush est valable X jours
  - Je peux me connecter avec les credentials auto-générés par ZetaPush pour transformer mon application temporaire en application permanente et choisir mes vrais identifiants
  - Je peux créer des methodes dans mon back-end appelables via mon front.

### ETQ dev front je créé ma première application via la CLI

*GIVEN*
  - J'ai un gestionnaire de package installé (npm ou yarn par exemple)
  - J'ai installé la CLI ZetaPush (via npm ou yarn)
*WHEN*
  - Lorsque que j'init un nouveau projet, exemple:
  ```$> zeta new --front --custom ```

*THEN*
  - J'ai une application front minimaliste avec package.json
  - Je peux dès à présent faire des appels sur ZetaPush
  - Un compte a été automatiquement créé pour moi avec un espace pour mon application
  - Je connais l'identifiant de mon application et les credentials ZetaPush
  - Mon application est configurée avec cet identifiant
  - Je suis alerté que l'application automatiquement créée sur ZetaPush est valable X jours
  - Je peux me connecter avec les credentials auto-générés par ZetaPush pour transformer mon application temporaire en application permanente et choisir mes vrais identifiants
  - Je peux créer des méthodes dans mon back-end appelables via mon front.
  - J'ai une méthode "hello_world()" custom.
  - J'ai un appel de la méthode "hello_world()" dans le front

<!-- # Démarrage 


## Parcours 2

## Partir de zéro


## A partir d'une app front existante


# Tutos ?

# Getting started ? -->