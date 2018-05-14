# Objectifs

* Un développeur doit pouvoir appeler un _cloud service_ (ZetaPush ou custom) et avoir une réponse en retour.
* Un développeur doit pouvoir développer son code métier dans des _custom cloud services_.
* Un développeur doit pouvoir utiliser l'autocomplétion de son IDE pour l'aider dans ses appels aux _cloud services_.
* Un développeur doit avoir accès depuis son IDE à la documentation des _cloud services_.
* Un développeur doit pouvoir écouter les évènements des _cloud services_.

Les profils ainsi que le vocabulaire utilisés sont définis dans [le readme](./README.md#vocabulaire).



# Pré-requis

* J'ai un compte sur ZetaPush
* J'ai une application front qui est prête à utiliser les _cloud services_. (Projet initialisé, dépendances installées, éventuellement la configuration de saisie)
* Nous utilisons le **Avengers Chat** comme cas d'usage (Chat temps réel)



# <a name="parcours-1"></a> Parcours 1 : Je développe sur mon environement local une application front avec ZetaPush sans _custom cloud service_

## Schéma

![Développement avec seulement les _cloud services_ ZetaPush](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/archi-dev-front-zp-service-only.html)

## User Stories


### [P01-DEV01] ETQ dev front j'utilise un _cloud service_ et j'ai une réponse en retour

_GIVEN_

* Je suis en cours de développement de mon _Avengers Chat_
* J'ai importé le _cloud service_ `UserService` qui me permet de gérer des utilisateurs
* J'ai accès à `UserService` via l'objet `userService`
* J'ai une _cloud function_ qui me permet de créer des utilisateurs : `createUser()`
* Je souhaite créer un utilisateur depuis mon code front
* J'écris le code suivant :

  ```javascript
  /**
   * I call the "createUser()" cloud function with many parameters.
   * "userService" is a UserService
   */
  this.userService.createUser({
    firstname: "Peter",
    lastname: "Parker",
    lastname: "Spider-Man"
  })
  .then((newUser) => {
    console.log(`new user created : ${newUser.username}`);
  })
  .catch((error) => {
    console.error(`Error to create new user : ${error.message}`);
  });


  /**
   *  Other syntaxe to call a cloud function
   */
  const newUser = await this.userService.createUser({
    firstname: "Peter",
    lastname: "Parker",
    lastname: "Spider-Man"
  });
  ```

_WHEN_

* Lorsque j'appelle ma _cloud function_ `createUser` via le _cloud service_ `UserService` et que tout s'est bien passé

_THEN_

* L'appel au service ZetaPush se fait de manière asynchrone et une réponse est renvoyée
* La réponse renvoyée est sous la forme d'une promesse
* La réponse est renvoyée dans le `.then()`


---


### [P01-DEV02] ETQ dev front j'utilise un _cloud service_ et j'ai une erreur en retour

_GIVEN_

* Je suis en cours de développement de mon _Avengers Chat_
* J'ai importé le _cloud service_ `UserService` qui me permet de gérer des utilisateurs
* J'ai accès à `UserService` via l'objet `userService`
* J'ai une _cloud function_ qui me permet de créer des utilisateurs : `createUser()`
* Je souhaite créer un utilisateur depuis mon code front
* J'écris le code suivant :

  ```javascript
  /**
   * I call the "createUser()" cloud function with many parameters.
   * "userService" is a UserService
   */
  this.userService.createUser({
    firstname: "Peter",
    lastname: "Parker",
    lastname: "Spider-Man"
  })
  .then((newUser) => {
    console.log(`new user created : ${newUser.username}`);
  })
  .catch((error) => {
    console.error(`Error to create new user : ${error.message}`);
  });


  /**
   *  Other syntaxe to call a cloud function
   */
  const newUser = await this.userService.createUser({
    firstname: "Peter",
    lastname: "Parker",
    lastname: "Spider-Man"
  });
  ```

_WHEN_

* Lorsque j'appelle ma _cloud function_ `createUser` via le _cloud service_ `UserService` et qu'une erreur est survenue

_THEN_

* L'appel au service ZetaPush se fait de manière asynchrone et une réponse est renvoyée
* La réponse renvoyée est sous la forme d'une promesse
* Comme il y a eu un dysfonctionnement, une erreur est renvoyée dans la partie `.catch()`
* L'objet d'erreur renvoyé comporte 2 paramètres : `tag` qui est un identifiant unique pour cette erreur et `message` qui est une description plus précise de cette erreur.


---


### [P01-DEV03] ETQ dev front j'écoute les évènements d'un _cloud service_

_GIVEN_

* Je suis en cours de développement de mon _Avengers Chat_
* J'ai importé le _cloud service_ `UserService` qui me permet de gérer des utilisateurs
* J'ai accès à `UserService` via l'objet `userService`
* J'ai une _cloud function_ qui me permet de créer des utilisateurs : `createUser()`
* Je souhaite écouter l'évènement de la création d'utilisateur
* J'écris le code suivant pour écouter les évènements de création d'utilisateurs :

```javascript
this.userService.onCreateUser = user => {
  console.log(`My new Avenger is : ${user.username}`);
};
```

_WHEN_

* Lorsqu'un nouvel utilisateur est créé sur mon application

_THEN_

* L'évènement `onCreateUser` est appelé et l'action résultante est exécutée
* Dans notre exemple, `My new Avenger is : "name"` est affiché dans sortie console

#### Précisions

Afin d'écouter les évènements d'une _cloud function_ précise, il faut écouter l'évènement suivant la syntaxe suivante :

* "on" + _nameCloudFunction_ en camelCase

Les évènements sont envoyés seulement à l'utilisateur qui appelle la _cloud function_.


---


### [P01-DEV04] ETQ dev front j'utilise l'autocompletion de mon IDE (VSCode) pour découvrir et utiliser les _cloud services_

_GIVEN_

* J'utilise Visual Studio Code comme IDE
* Je suis en cours de développement de mon _Avengers Chat_
* J'ai importé le _cloud service_ `UserService` qui me permet de gérer des utilisateurs
* J'ai accès à `UserService` via l'objet `userService`
* J'ai différentes _cloud functions_ disponibles au sein de mon _cloud service_ : `createUser()` / `createOrganization()` / `getUser()`

_WHEN_

* Lorsque je commence à écrire mon appel au _cloud service_ : `this.userService.create`

_THEN_

* L'autocompletion me propose les différentes _cloud functions_ auquels j'ai accès en fonction de ma saisie :
  * `this.userService.createUser()`
  * `this.userService.createOrganization()`
* La _cloud function_ `getUser()` ne correspond pas et n'est donc pas affichée


---


### [P01-DEV05] ETQ dev front j'ai accès à la documentation des _cloud services_ depuis mon IDE (VSCode)

_GIVEN_

* J'utilise Visual Studio Code comme IDE
* Je suis en cours de développement de mon _Avengers Chat_
* J'ai importé le _cloud service_ `UserService` qui me permet de gérer des utilisateurs
* J'ai accès à `UserService` via l'objet `userService`
* J'ai différentes _cloud functions_ disponibles au sein de mon _cloud service_ : `createUser()` / `createOrganization()` / `getUser()`

_WHEN_

* Lorsque je commence à écrire mon appel au _cloud service_ : `this.userService.create`

_THEN_

* L'autocomplétion s'affiche pour me proposer les différentes _cloud functions_ auquel j'ai accès en fonction de ma saisie
* Au sein de la pop-up d'autocomplétion, je peux cliquer sur un lien `view documentation` qui va me rediriger (Toujours dans la pop-up) sur la liste des _cloud functions_ pour ce _cloud service_
* Je peux naviguer au sein de la documentation dans la pop-up, en utilisant différents liens.
* Pour chaque _cloud function_ il y a son nom, sa description, ses paramètres entrants et son retour



# <a name="parcours-2"></a> Parcours 2 : Je développe sur mon environement local une application avec ZetaPush et des _custom cloud services_

## Schéma

![Développement avec seulement les services ZetaPush](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/archi-dev-front-with-custom-service.html)

## User Stories



### [P02-DEV01] ETQ dev full-stack je développe sur mon environement local mon code métier dans une _custom cloud function_

_GIVEN_

* Je suis en cours de développement de mon _Avengers Chat_
* Je souhaite réaliser mon code métier et le déployer côté back
* Je souhaite créer un _custom cloud service_ nommé `AvengersService` qui va me permettre de réaliser le code métier de mon chat
* Dans un premier temps je veux seulement ajouter une _cloud function_ à mon _custom cloud service_ qui est `attackWithRandomSkill()` qui va me permettre de lancer une attaque aléatoire en fonction du personnage (chaque Avenger a plusieurs compétences possibles)

_WHEN_

* Lorsque j'écris mon _custom cloud service_ selon cette syntaxe :

  ```javascript
  /**
   *  This class gathers the cloud functions for my own custom cloud service
   *  Each method is a cloud function
   */
  class AvengersService {

  /**
   *  Function to print that an Avenger do a random attack
   */
  attackWithRandomSkill(avengerName) {
    // Get the Avengers
    const avenger = this.userService.getUserByLogin({login: avengerName}):

    // Get a random power of this Avenger
    const superpower = avenger.superpowers[Math.floor(Math.random()*avenger.superpowers.length)];

    // Print that we attack with a random skill !
    print(`${avengerName} attacks with ${superpower} !!!`);

    return superpower;
  }
}
  ```

_THEN_

* Mon _custom cloud service_ est complet (pour le moment)
* Il n'est pas utilisable en l'état, il faut le déployer avec la CLI : `zeta push --server-only`
* Une fois le _custom cloud service_ déployé, ce dernier est appelable au même titre qu'un _cloud service_ avec la syntaxe :

  ```javascript
  /**
   *  "avengersService" is an instance of AvengersService
   */
  this.avengersService.attackWithRandomSkill("Spider-Man");
  ```

- Un listener d'évènement est automatiquement créé pour chaque _cloud function_, ici nous pouvons écouter la création de jeu avec :

  ```javascript
  /**
   *  "avengersService" is an instance of AvengersService
   *  We assume that the attackWithRandomSkill() cloud function return a string
   */
  this.avengersService.attackWithRandomSkill = superpower => {
    console.log(`The Avenger attacks with the skill : ${superpower} !!`);
  };
  ```


---


### [P02-DEV02] ETQ dev full-stack j'utilise un _custom cloud service_ et j'ai une réponse en retour

_GIVEN_

* Je suis en cours de développement de mon _Avengers Chat_
* J'ai importé le _custom cloud service_ `AvengersService` qui me permet de gérer un jeu
* J'ai accès à `AvengersService` via l'objet `avengersService`
* J'ai une _cloud function_ qui me permet de faire une attaque d'Avenger aléatoire (en fonction du personnage) : `attackWithRandomSkill()`
* Je souhaite lancer une attaque avec un Avenger particulier côté front
* J'écris le code suivant :

  ```javascript
  /**
   * I call the "attackWithRandomSkill()" cloud function with an username.
   * "avengersService" is a AvengersService instance
   */
  this.avengersService.attackWithRandomSkill("Spider-Man")
    /**
     *  The cloud function call return a promise. In the "then" part we have the response
     */
    .then(superpower => {
      console.log(`The Avenger attacks with the skill : ${superpower} !!`);
    })
    /**
     *  The cloud function call return a promise. In the "catch" part we have the error
     */
    .catch(error => {
      console.errror(`Failed to launch an attack with this Avenger : ${error.message}`);
    });
  ```

_WHEN_

* Lorsque j'appelle ma _cloud function_ `attackWithRandomSkill` via le _custom cloud service_ `AvengersService` et que tout s'est bien passé

_THEN_

* L'appel au service ZetaPush se fait de manière asynchrone et une réponse est renvoyée
* La réponse renvoyée est sous la forme d'une promesse
* La réponse est renvoyée dans le `.then()`

---


### [P02-DEV03] ETQ dev full-stack j'utilise un _custom cloud service_ et j'ai une erreur en retour

_GIVEN_

* Je suis en cours de développement de mon _Avengers Chat_
* J'ai importé le _custom cloud service_ `AvengersService` qui me permet de gérer un jeu
* J'ai accès à `AvengersService` via l'objet `avengersService`
* J'ai une _cloud function_ qui me permet de faire une attaque d'Avenger aléatoire (en fonction du personnage) : `attackWithRandomSkill()`
* Je souhaite lancer une attaque avec un Avenger particulier côté front
* J'écris le code suivant :

  ```javascript
  /**
   * I call the "attackWithRandomSkill()" cloud function with an username.
   * "avengersService" is a AvengersService instance
   */
  this.avengersService.attackWithRandomSkill("Spider-Man")
    /**
     *  The cloud function call return a promise. In the "then" part we have the response
     */
    .then(superpower => {
      console.log(`The Avenger attacks with the skill : ${superpower} !!`);
    })
    /**
     *  The cloud function call return a promise. In the "catch" part we have the error
     */
    .catch(error => {
      console.errror(`Failed to launch an attack with this Avenger : ${error.message}`);
    });
  ```

_WHEN_

* Lorsque j'appelle ma _cloud function_ `attackWithRandomSkill` via le _custom cloud service_ `AvengersService` et qu'une erreur est survenue

_THEN_

* L'appel au service ZetaPush se fait de manière asynchrone et une réponse est renvoyée
* La réponse renvoyée est sous la forme d'une promesse
* Comme il y a eu un dysfonctionnement, une erreur est renvoyée dans la partie `.catch()`
* L'objet d'erreur renvoyé comporte 2 paramètres : `tag` qui est un identifiant unique pour cette erreur et `message` qui est une description plus précise de cette erreur.


---


### [P02-DEV04] ETQ dev full-stack j'écoute les évènements d'un _custom cloud service_

_GIVEN_

* Je suis en cours de développement de mon _Avengers Chat_
* J'ai importé le _custom cloud service_ `AvengersService` qui me permet de gérer un jeu
* J'ai accès à `AvengersService` via l'objet `avengersService`
* J'ai une _cloud function_ qui me permet de faire une attaque d'Avenger aléatoire (en fonction du personnage) : `attackWithRandomSkill()`
* Je souhaite écouter l'évènement d'attaque d'un Avenger
* J'écris le code suivant pour écouter les évènements d'attaque :

```javascript
this.avengersService.onAttackWithRandomSkill = superpower => {
  console.log(`The Avenger attacks with the skill : ${superpower} !!`);
};
```

_WHEN_

* Lorsqu'une attaque est lancée par un Avenger

_THEN_

* L'évènement `onAttackWithRandomSkill` est appelé et l'action résultante est exécutée
* Dans notre exemple, `The Avenger attacks with the skill : "superpower" !!` est affiché dans sortie console

#### Précisions

Afin d'écouter les évènements d'une _cloud function_ précise, il faut écouter l'évènement suivant la syntaxe suivante :

* "on" + _nameCloudFunction_ en camelCase

Les évènements sont envoyés seulement à l'utilisateur qui appelle la _cloud function_.


---


### [P02-DEV05] ETQ dev full-stack j'utilise l'autocompletion de mon IDE (VSCode) pour découvrir et utiliser mes _custom cloud services_

_GIVEN_

* J'utilise Visual Studio Code comme IDE
* Je suis en cours de développement de mon _Avengers Chat_
* J'ai importé le _custom cloud service_ `AvengersService` qui me permet de gérer un jeu
* J'ai accès à `AvengersService` via l'objet `avengersService`
* J'ai différentes _cloud functions_ disponibles au sein de mon _custom cloud service_ : `attackWithRandomSkill()` / `attackWithSpecificSkill()` / `getHealthAvenger()`

_WHEN_

* Lorsque je commence à écrire mon appel au _custom cloud service_ : `this.avengersService.attack`

_THEN_

* L'autocompletion me propose les différentes _cloud functions_ auquels j'ai accès en fonction de ma saisie :
  * `this.avengersService.attackWithRandomSkill()`
  * `this.avengersService.attackWithSpecificSkill()`
* La _cloud function_ `getHealthAvenger()` ne correspond pas et n'est donc pas affichée


---


### [P02-DEV06] ETQ dev full-stack j'ai accès à la documentation de mes _custom cloud services_ depuis mon IDE (VSCode)

_GIVEN_

* J'utilise Visual Studio Code comme IDE
* Je suis en cours de développement de mon _Avengers Chat_
* J'ai importé le _custom cloud service_ `AvengersService` qui me permet de gérer un jeu
* J'ai accès à `AvengersService` via l'objet `avengersService`
* J'ai différentes _cloud functions_ disponibles au sein de mon _custom cloud service_ : `attackWithRandomSkill()` / `attackWithSpecificSkill()` / `getHealthAvenger()`

_WHEN_

* Lorsque je commence à écrire mon appel au _custom cloud service_ : `this.avengersService.attack`

_THEN_

* L'autocomplétion s'affiche pour me proposer les différentes _cloud functions_ auquel j'ai accès en fonction de ma saisie
* Au sein de la pop-up d'autocomplétion, je peux cliquer sur un lien `view documentation` qui va me rediriger (Toujours dans la pop-up) sur la liste des _cloud functions_ pour ce _cloud service_
* Je peux naviguer au sein de la documentation dans la pop-up, en utilisant différents liens.
* Pour chaque _cloud function_ il y a son nom, sa description, ses paramètres entrants et son retour
