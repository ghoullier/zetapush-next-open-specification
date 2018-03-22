
# Objectifs

- Un développeur doit pouvoir appeler un service (ZetaPush ou custom) et avoir une promesse en retour.
- Un développeur doit pouvoir développer son code métier dans des services custom.
- Un développeur doit pouvoir utiliser l'autocomplétion de son IDE pour l'aider dans le développement ou les appels de service ZetaPush.
- Un développeur doit avoir accès depuis son IDE à la documentation des services ZetaPush.
- Un développeur doit pouvoir associer une callback à un service ZetaPush pour être notifié des différents évènements.


Les profils utilisés sont définis dans [commun.md](./commun.md).

***

# Pré-requis

- J'ai un compte sur ZetaPush
- J'ai une application front qui est configurée pour utiliser ZetaPush


## Schéma

![Développement](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/dev-front-interaction-services-zetapush.html)

### Explications
  
  - Depuis son environnement local, le développeur modifie son application en agissant sur la partie front et les appels aux services (ZetaPush ou custom)
  - Le développeur peut créer son code métier, soit à travers `console.zetapush.com`, soit par du développement local. Il le déploie ensuite au sein de son application

***

# <a name="parcours-1"></a> Parcours 1 : Je développe une application front avec ZetaPush sans service custom

## Schéma

![Développement avec seulement les services ZetaPush](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/archi-dev-front-zp-service-only.html)

## User Stories

***

### ETQ dev front je souhaite utiliser les services ZetaPush et avoir une promesse en retour

*GIVEN*
  - J'ai importé la dépendance nécessaire pour appeler un service ZetaPush
  - J'ai un objet `zpService` qui me permet d'appeler les services ZetaPush
  - J'écris mon appel à un service ZetaPush, avec comme retour une promesse :
  
  ```javascript
  this.zpService.createUser({ login, password})
    .then((user) => {
    console.log('UserCreated', user);
  })
    .catch((err) => {
    console.error('ErrorCreateUser', err);
  })
  ```

*WHEN*
  - Lorsque j'exécute mon appel au service ZetaPush

*THEN*
  - L'appel au service ZetaPush se fait et une promesse est renvoyée
  - En absence d'erreur le resultat passe dans `.then()`, sinon l'erreur est renvoyée dans `.catch()`

***

###  ETQ dev front je souhaite utiliser l'autocompletion de mon IDE pour découvrir et utiliser les services ZetaPush

*GIVEN*
  - J'ai importé la dépendance nécessaire pour appeler un service ZetaPush
  - J'ai un objet `zpService` qui me permet d'appeler les services ZetaPush
  - Je souhaite appeler un service ZetaPush, pour créer un utilisateur par exemple

*WHEN*
  - Lorsque je commence à écrire mon appel au service ZetaPush : `this.zpService.create`

*THEN*
  - L'autocompletion me propose les différents services auquels je peux accèder en fonction de ma saisie :
    * this.zpService.createUser()
    * this.zpService.createOrganization()
    * this.zpService.createRoom()
    * ...

***

### ETQ dev front je souhaite écouter les évènements d'un service ZetaPush en ajoutant une callback

*GIVEN*
  - J'ai importé la dépendance nécessaire pour appeler un service ZetaPush
  - J'ai un objet `zpService` qui me permet d'appeler les services ZetaPush et d'écouter les évènements
  - Je souhaite écouter les évènements d'un service ZetaPush
  - J'ajoute une callback sur un évènement, par exemple :

  ```javascript
  this.zpService.onUserCreated = (user) => {
    console.log(`User created : ${user.name}`);
  };
  ```

*WHEN*
  - Lorsqu'un nouvel utilisateur est créé sur mon application

*THEN*
  - Ma callback associée à `onUserCreated` est appelée. Dans l'exemple, l'utilisateur créé est affiché

***

### ETQ dev front je souhaite avoir accès à la documentation des services ZetaPush depuis mon IDE

*GIVEN*
  - J'ai importé la dépendance nécessaire pour appeler un service ZetaPush
  - J'ai un objet `zpService` qui me permet d'appeler les services ZetaPush
  - Je souhaite me renseigner sur un service ZetaPush
  - J'utilise l'autocompletion pour afficher les différents services auquels j'ai accès

*WHEN*
  - Lorsqu'un service est en surbrillance dans mon IDE avec l'autocompletion

*THEN*
  - La documentation du service concerné est affiché dans l'IDE avec son nom, sa description, ses paramètres entrants et son retour

***

# <a name="parcours-2"></a> Parcours 2 : Je développe une application avec ZetaPush et des services custom

## Schéma

![Développement avec seulement les services ZetaPush](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/archi-dev-front-with-custom-service.html)


## User Stories

***

### ETQ dev je souhaite développer mon code métier dans un service custom

*GIVEN*
  - J'ai importé les dépendances nécessaires pour créer un service custom
  - J'écris mon service custom, exemple :

  ```javascript
  function createGame({name: string}): Promise<any> {
    ...
  }
  ```

*WHEN*
  - Lorsque je publie mon service custom dans mon application

*THEN*
  - Mon service custom est accessible depuis la plateforme au même titre qu'un service ZetaPush
  - Je peux l'appeler avec la syntaxe : 
  
  ```javascript
  this.zpService.createGame({ name })
  .then((game) => {
    console.log(`GameCreated : ${game.name}`);
  })
  .catch((err) => {
    console.error(`ErrorCreateGame : ${err}`);
  })
  ```
  - Un évènement peut être écouté lorsqu'un appel à ce service est fait avec la syntaxe :
  
  ```javascript
  this.zpService.onCreateGame = (result) => {
    console.log(`CreateGameEvent : ${result}`);
  }
  ```

***

### ETQ dev je souhaite utiliser mes services custom et avoir une promesse en retour

*GIVEN*
  - J'ai importé la dépendance nécessaire pour appeler un service ZetaPush
  - J'ai un objet `zpService` qui me permet d'appeler les services ZetaPush
  - J'ai déjà créé un service custom, exemple : `createGame()`
  - Mon service custom a été déployé sur ZetaPush
  - J'ai écrit l'appel à mon service custom :

  ```javascript
  this.zpService.createGame({ name})
    .then((game) => {
    console.log('gameCreated', game);
  })
    .catch((err) => {
    console.error('ErrorCreateGame', err);
  })
  ```

*WHEN*
  - Lorsque j'exécute mon appel à mon service custom

*THEN*
  - L'appel au service custom se fait et une promesse est renvoyée
  - En absence d'erreur le resultat passe dans `.then()`, sinon l'erreur est renvoyée dans `.catch()`


***


###  ETQ dev je souhaite utiliser l'autocompletion de mon IDE pour découvrir et utiliser mes services custom

*GIVEN*
  - J'ai importé la dépendance nécessaire pour appeler un service ZetaPush ou custom déployés
  - J'ai un objet `zpService` qui me permet d'appeler les services ZetaPush ou custom déployés
  - Je souhaite appeler un service custom, `createGame()` par exemple

*WHEN*
  - Lorsque je commence à écrire mon appel au service ZetaPush : `this.zpService.create`

*THEN*
  - L'autocompletion me propose les différents services auquels je peux accèder en fonction de ma saisie :
    * this.zpService.createUser()
    * this.zpService.createGame()
    * this.zpService.createOrganization()
    * this.zpService.createRoom()
    * ...
  - L'autocompletion ne fait pas de distinction entre un service ZetaPush ou un service custom déployé


***

### ETQ dev je souhaite écouter les évènements d'un service custom en ajoutant une callback

*GIVEN*
  - J'ai importé la dépendance nécessaire pour appeler un service ZetaPush ou un service custom déployé
  - J'ai un objet `zpService` qui me permet d'appeler les services ZetaPush ou un service custom déployé et d'écouter les évènements
  - Je souhaite écouter les évènements d'un service custom que j'ai créé
  - Le service custom est déployé sur mon application
  - J'ajoute une callback sur un évènement, par exemple :

  ```javascript
  this.zpService.onCreateGame = (result) => {
    console.log(`GameCreatedEvent : ${result}`);
  };
  ```

*WHEN*
  - Lorsque le service custom appelé, `createGame()` dans l'exemple

*THEN*
  - Ma callback associée (`onCreateGame` dans l'exemple) est appelée.
***

### ETQ dev je souhaite avoir accès à la documentation de mes services custom depuis mon IDE

*GIVEN*
  - J'ai importé la dépendance nécessaire pour appeler un service ZetaPush ou un service custom déployé
  - J'ai un objet `zpService` qui me permet d'appeler les services ZetaPush ou un service custom déployé
  - Je souhaite me renseigner sur un service custom que j'ai créé
  - Mon service custom est déployé sur mon application
  - J'utilise l'autocompletion pour afficher les différents services auquels j'ai accès

*WHEN*
  - Lorsqu'un service est en surbrillance dans mon IDE avec l'autocompletion

*THEN*
  - La documentation du service concerné est affiché dans l'IDE avec son nom, sa description, ses paramètres entrants et son retour
  - L'affichage de la documentation et de l'autocompletion ne fait aucune distinction entre un service ZetaPush ou un service custom (Fonctionnellement parlant, un service custom peut être annoté pour plus de clarté)
  - La documentation du service custom se base sur les commentaires et types lors de la création de ce service

***


# <a name="parcours-3"></a> Parcours 3 : Mon équipe développe une application front avec ZetaPush sans services custom

## Schéma

TODO

## User Stories

TODO

### ETQ équipe de dev front, nous souhaitons utiliser les services ZetaPush


***

# <a name="parcours-4"></a> Parcours 4 : Mon équipe développe une application avec ZetaPush et des services custom

## Schéma

TODO

## User Stories

TODO

### ETQ équipe de dev front, nous souhaitons utiliser les services custom ZetaPush

  


