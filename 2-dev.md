# Objectifs

* Un développeur doit pouvoir appeler un _cloud service_ (ZetaPush ou custom) et avoir une réponse en retour.
* Un développeur doit pouvoir développer son code métier dans des _custom cloud services_.
* Un développeur doit pouvoir utiliser l'autocomplétion de son IDE pour l'aider dans ses appels aux _cloud services_.
* Un développeur doit avoir accès depuis son IDE à la documentation des _cloud services_.
* Un développeur doit pouvoir écouter les évènements des _cloud services_.

Les profils ainsi que le vocabulaire utilisés sont définis dans [commun.md](./commun.md).

---

# Pré-requis

* J'ai un compte sur ZetaPush
* J'ai une application front qui est prête à utiliser les _cloud services_. (Projet initialisé, dépendances installées, éventuellement la configuration de saisie)

---

# <a name="parcours-1"></a> Parcours 1 : Je développe une application front avec ZetaPush sans _custom cloud service_

## Schéma

![Développement avec seulement les _cloud services_ ZetaPush](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/archi-dev-front-zp-service-only.html)

## User Stories

---

### ETQ dev front j'utilise un _cloud service_ et j'ai une réponse en retour

_GIVEN_

* J'ai mon application front qui est en cours de développement
* J'ai importé le _cloud service_ `UsersService` qui me permet de gérer des utilisateurs
* J'ai accès à `UsersService` via l'objet `usersService`
* J'ai une _cloud function_ qui me permet de créer des utilisateurs : `createUser()`
* Je souhaite créer un utilisateur depuis mon code front
* J'écris le code suivant :

  ```javascript
  /**
   * I call the "createUser()" cloud function with many parameters.
   * "usersService" is a UsersService
   */
  this.usersService
    .createUser({
      firstname: "Jean",
      lastname: "Martin",
      email: "jean-martin@zetapush.com"
    })
    /**
     *  The cloud function return a promise. In the "then" part we have the response
     */
    .then(createdUser => {
      console.log(`The user : ${createdUser.firstname} ${createdUser.lastname} is just created !`);
    })
    /**
     *  The cloud function return a promise. In the "catch" part we have the error
     */
    .catch(error => {
      console.errror(`Failed to create user : ${error.message}`);
    });
  ```

_WHEN_

* Lorsque j'appelle ma _cloud function_ `createUser` via le _cloud service_ `UsersService` et que tout s'est bien passé

_THEN_

* L'appel au service ZetaPush se fait de manière asynchrone et une réponse est renvoyée
* La réponse renvoyée est sous la forme d'une promesse
* La réponse est renvoyée dans le `.then()`

---

### ETQ dev front j'utilise un _cloud service_ et j'ai une erreur en retour

_GIVEN_

* J'ai mon application front qui est en cours de développement
* J'ai importé le _cloud service_ `UsersService` qui me permet de gérer des utilisateurs
* J'ai accès à `UsersService` via l'objet `usersService`
* J'ai une _cloud function_ qui me permet de créer des utilisateurs : `createUser()`
* Je souhaite créer un utilisateur depuis mon code front
* J'écris le code suivant :

  ```javascript
  /**
   * I call the "createUser()" cloud function with many parameters.
   * "usersService" is a UsersService
   */
  this.usersService
    .createUser({
      firstname: "Jean",
      lastname: "Martin",
      email: "jean-martin@zetapush.com"
    })
    /**
     *  The cloud function return a promise. In the "then" part we have the response
     */
    .then(createdUser => {
      console.log(`The user : ${createdUser.firstname} ${createdUser.lastname} is just created !`);
    })
    /**
     *  The cloud function return a promise. In the "catch" part we have the error
     */
    .catch(error => {
      console.errror(`Failed to create user : ${error.message}`);
    });
  ```

_WHEN_

* Lorsque j'appelle ma _cloud function_ `createUser` via le _cloud service_ `UsersService` et qu'une erreur est survenue

_THEN_

* L'appel au service ZetaPush se fait de manière asynchrone et une réponse est renvoyée
* La réponse renvoyée est sous la forme d'une promesse
* Comme il y a eu un dysfonctionnement, une erreur est renvoyée dans la partie `.catch()`
* L'objet d'erreur renvoyé comporte 2 paramètres : `tag` qui est un identifiant unique pour cette erreur et `message` qui est une description plus précise de cette erreur.

---

### ETQ dev front j'écoute les évènements d'un _cloud service_

_GIVEN_

* J'ai mon application front qui est en cours de développement
* J'ai importé le _cloud service_ `UsersService` qui me permet de gérer des utilisateurs
* J'ai accès à `UsersService` via l'objet `usersService`
* J'ai une _cloud function_ qui me permet de créer des utilisateurs : `createUser()`
* Je souhaite écouter l'évènement de la création d'utilisateur
* J'écris le code suivant pour écouter les évènements de création d'utilisateurs :

```javascript
this.usersService.onCreateUser = user => {
  console.log(`User created : ${user.name}`);
};
```

_WHEN_

* Lorsqu'un nouvel utilisateur est créé sur mon application

_THEN_

* L'évènement `onCreateUser` est appelé et l'action résultante est exécutée
* Dans notre exemple, `User created : "name"` est affiché dans sortie console

#### Précisions

Afin d'écouter les évènements d'une _cloud function_ précise, il faut écouter l'évènement suivant la syntaxe suivante :

* "on" + _nameCloudFunction_ en camelCase

Les évènements sont envoyés seulement à l'utilisateur qui appelle la _cloud function_.

---

### ETQ dev front j'utilise l'autocompletion de mon IDE (VSCode) pour découvrir et utiliser les _cloud services_

_GIVEN_

* J'utilise Visual Studio Code comme IDE
* J'ai mon application front qui est en cours de développement
* J'ai importé le _cloud service_ `UsersService` qui me permet de gérer des utilisateurs
* J'ai accès à `UsersService` via l'objet `usersService`
* J'ai différentes _cloud functions_ disponibles au sein de mon _cloud service_ : `createUser()` / `createOrganization()` / `getUser()`

_WHEN_

* Lorsque je commence à écrire mon appel au _cloud service_ : `this.usersService.create`

_THEN_

* L'autocompletion me propose les différentes _cloud functions_ auquels j'ai accès en fonction de ma saisie :
  * `this.usersService.createUser()`
  * `this.usersService.createOrganization()`
* La _cloud function_ `getUser()` ne correspond pas et n'est donc pas affichée

---


### ETQ dev front j'ai accès à la documentation des _cloud services_ depuis mon IDE (VSCode)

_GIVEN_

* J'utilise Visual Studio Code comme IDE
* J'ai mon application front qui est en cours de développement
* J'ai importé le _cloud service_ `UsersService` qui me permet de gérer des utilisateurs
* J'ai accès à `UsersService` via l'objet `usersService`
* J'ai différentes _cloud functions_ disponibles au sein de mon _cloud service_ : `createUser()` / `createOrganization()` / `getUser()`

_WHEN_

* Lorsque je commence à écrire mon appel au _cloud service_ : `this.usersService.create`

_THEN_

* L'autocomplétion s'affiche pour me proposer les différentes _cloud functions_ auquel j'ai accès en fonction de ma saisie
* Au sein de la pop-up d'autocomplétion, je peux cliquer sur un lien `view documentation` qui va me rediriger (Toujours dans la pop-up) sur la liste des _cloud functions_ pour ce _cloud service_
* Je peux naviguer au sein de la documentation dans la pop-up, en utilisant différents liens.
* Pour chaque _cloud function_ il y a son nom, sa description, ses paramètres entrants et son retour

---

# <a name="parcours-2"></a> Parcours 2 : Je développe une application avec ZetaPush et des _custom cloud services_

## Schéma

![Développement avec seulement les services ZetaPush](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/archi-dev-front-with-custom-service.html)

## User Stories

---

### ETQ dev full-stack je développe mon code métier dans une _custom cloud function_

_GIVEN_

* J'ai mon application front qui est en cours de développement
* Je souhaite réaliser mon code métier et le déployer côté back
* Je souhaite créer un _custom cloud service_ nommé `GameService` qui va me permettre de gérer un jeu
* Dans un premier temps je veux seulement ajouter une _cloud function_ à mon _custom cloud service_ qui est `createGame()` qui va me permettre d'initialiser un jeu

_WHEN_

* Lorsque j'écris mon _custom cloud service_ selon cette syntaxe :

  ```javascript
  /**
   *  This class gathers the cloud functions for my own custom cloud service to manage a game
   *  Each method is a cloud function
   *  We extends with "CustomCloudService" to get special methods and say to ZetaPush that is a custom cloud service
   */
  class GameService extends CustomCloudService {

    /**
     * Cloud function to create a new game with a name
     */
    function createGame(name) {
      // ...
      // Some code
      // ...
    }
  }
  ```

_THEN_

* Mon _custom cloud service_ est complet (pour le moment)
* Il n'est pas utilisable en l'état, il faut le déployer avec la CLI : `zeta push --server-only`
* Une fois le _custom cloud service_ déployé, ce dernier est appelable au même titre qu'un _cloud service_ avec la syntaxe :

  ```javascript
  /**
   *  "gameService" is an instance of GameService
   */
  this.gameService.createGame("Avengers Game");
  ```

- Un listener d'évènement est automatiquement créé pour chaque _cloud function_, ici nous pouvons écouter la création de jeu avec :

  ```javascript
  /**
   *  "gameService" is an instance of GameService
   *  We assume that the createGame() cloud function return an objet with a 'name' parameter
   */
  this.gameService.onCreateGame = game => {
    console.log(`New game created : ${game.name}`);
  };
  ```

---

### ETQ dev full-stack j'utilise un _custom cloud service_ et j'ai une réponse en retour

_GIVEN_

* J'ai mon application front qui est en cours de développement
* J'ai importé le _custom cloud service_ `GameService` qui me permet de gérer un jeu
* J'ai accès à `GameService` via l'objet `gameService`
* J'ai une _cloud function_ qui me permet d'initialiser un jeu : `createGame()`
* Je souhaite initialiser un jeu depuis mon code front
* J'écris le code suivant :

  ```javascript
  /**
   * I call the "createGame()" cloud function with a name.
   * "gameService" is a GameService instance
   */
  this.gameService
    .createGame({
      name: "Avengers game"
    })
    /**
     *  The cloud function call return a promise. In the "then" part we have the response
     */
    .then(createdGame => {
      console.log(`The created game : ${createdGame.name} with the id : ${createdGame.id}, is just created !`);
    })
    /**
     *  The cloud function call return a promise. In the "catch" part we have the error
     */
    .catch(error => {
      console.errror(`Failed to create game : ${error.message}`);
    });
  ```

_WHEN_

* Lorsque j'appelle ma _cloud function_ `createGame` via le _custom cloud service_ `GameService` et que tout s'est bien passé

_THEN_

* L'appel au service ZetaPush se fait de manière asynchrone et une réponse est renvoyée
* La réponse renvoyée est sous la forme d'une promesse
* La réponse est renvoyée dans le `.then()`

---

### ETQ dev full-stack j'utilise un _custom cloud service_ et j'ai une erreur en retour

_GIVEN_

* J'ai mon application front qui est en cours de développement
* J'ai importé le _custom cloud service_ `GameService` qui me permet de gérer un jeu
* J'ai accès à `GameService` via l'objet `gameService`
* J'ai une _cloud function_ qui me permet d'initialiser un jeu : `createGame()`
* Je souhaite initialiser un jeu depuis mon code front
* J'écris le code suivant :

  ```javascript
  /**
   * I call the "createGame()" cloud function with a name.
   * "gameService" is a GameService instance
   */
  this.gameService
    .createGame({
      name: "Avengers game"
    })
    /**
     *  The cloud function call return a promise. In the "then" part we have the response
     */
    .then(createdGame => {
      console.log(`The created game : ${createdGame.name} with the id : ${createdGame.id}, is just created !`);
    })
    /**
     *  The cloud function call return a promise. In the "catch" part we have the error
     */
    .catch(error => {
      console.errror(`Failed to create game : ${error.message}`);
    });
  ```

_WHEN_

* Lorsque j'appelle ma _cloud function_ `createGame` via le _cloud service_ `GameService` et qu'une erreur est survenue

_THEN_

* L'appel au service ZetaPush se fait de manière asynchrone et une réponse est renvoyée
* La réponse renvoyée est sous la forme d'une promesse
* Comme il y a eu un dysfonctionnement, une erreur est renvoyée dans la partie `.catch()`
* L'objet d'erreur renvoyé comporte 2 paramètres : `tag` qui est un identifiant unique pour cette erreur et `message` qui est une description plus précise de cette erreur.

---

### ETQ dev full-stack j'écoute les évènements d'un _custom cloud service_

_GIVEN_

* J'ai mon application front qui est en cours de développement
* J'ai importé le _custom cloud service_ `GameService` qui me permet de gérer un jeu
* J'ai accès à `GameService` via l'objet `gameService`
* J'ai une _cloud function_ qui me permet d'initialiser un jeu : `creatGame()`
* Je souhaite écouter l'évènement de la création d'un jeu
* J'écris le code suivant pour écouter les évènements de création de jeu :

```javascript
this.usersService.onCreateGame = game => {
  console.log(`Game created : ${game.name}`);
};
```

_WHEN_

* Lorsqu'un nouveau jeu est créé sur mon application

_THEN_

* L'évènement `onCreateGame` est appelé et l'action résultante est exécutée
* Dans notre exemple, `Game created : "name"` est affiché dans sortie console

#### Précisions

Afin d'écouter les évènements d'une _cloud function_ précise, il faut écouter l'évènement suivant la syntaxe suivante :

* "on" + _nameCloudFunction_ en camelCase

Les évènements sont envoyés seulement à l'utilisateur qui appelle la _cloud function_.

---

### ETQ dev full-stack j'utilise l'autocompletion de mon IDE (VSCode) pour découvrir et utiliser mes _custom cloud services_

_GIVEN_

* J'utilise Visual Studio Code comme IDE
* J'ai mon application front qui est en cours de développement
* J'ai importé le _custom cloud service_ `GameService` qui me permet de gérer un jeu
* J'ai accès à `GameService` via l'objet `gameService`
* J'ai différentes _cloud functions_ disponibles au sein de mon _custom cloud service_ : `createGame()` / `createPlayer()` / `movePlayer()`

_WHEN_

* Lorsque je commence à écrire mon appel au _custom cloud service_ : `this.gameService.create`

_THEN_

* L'autocompletion me propose les différentes _cloud functions_ auquels j'ai accès en fonction de ma saisie :
  * `this.gameService.createGame()`
  * `this.gameService.createPlayer()`
* La _cloud function_ `movePlayer()` ne correspond pas et n'est donc pas affichée

---

### ETQ dev full-stack j'ai accès à la documentation de mes _custom cloud services_ depuis mon IDE (VSCode)

_GIVEN_

* J'utilise Visual Studio Code comme IDE
* J'ai mon application front qui est en cours de développement
* J'ai importé le _custom cloud service_ `GameService` qui me permet de gérer un jeu
* J'ai accès à `GameService` via l'objet `gameService`
* J'ai différentes _cloud functions_ disponibles au sein de mon _cloud service_ : `createGame()` / `createPlayer()` / `movePlayer()`

_WHEN_

* Lorsque je commence à écrire mon appel au _custom cloud service_ : `this.gameService.create`

_THEN_

* L'autocomplétion s'affiche pour me proposer les différentes _cloud functions_ auquel j'ai accès en fonction de ma saisie
* Au sein de la pop-up d'autocomplétion, je peux cliquer sur un lien `view documentation` qui va me rediriger (Toujours dans la pop-up) sur la liste des _cloud functions_ pour ce _cloud service_
* Je peux naviguer au sein de la documentation dans la pop-up, en utilisant différents liens.
* Pour chaque _cloud function_ il y a son nom, sa description, ses paramètres entrants et son retour

---