# Objectifs

* Un développeur front doit pouvoir mocker les appels serveurs lors de ses tests.
* Un développeur full-stack doit pouvoir tester unitairement son code serveur.
* Un développeur doit pouvoir tester (test d'intégration ou test fonctionnel) son code avec un contexte d'exécution propre entre chaque test.
* Un développeur doit pouvoir spécifier dans son test, l'état dans lequel se trouve son application avant l'exécution du test.

# Objectifs à plus long terme

* Un développeur doit pouvoir exécuter ses tests en parallèle

# Pré-requis

* J'utilise mon éditeur de texte ou IDE préféré.
* J'ai une application front existante créée avec mon framework préféré et initialisé avec ZetaPush.
* J'utilise mon framework de test préféré. Dans les exemples de syntaxe, nous utiliserons _Mocha_.

# Contextes

Dans cette section nous allons spécifier différents contextes que nous allons utiliser tout au loin de nos User Stories dans la section _GIVEN_.

# <a name="parcours-1"></a> Parcours 1 : Je développe une application front avec ZetaPush sans service custom

## User Stories

### ETQ dev je mock un appel à un service ZetaPush

_GIVEN_

* J'ai une application front de développée
* J'ai l'ensemble des dépendances nécessaires à l'utilisation de ZetaPush dans mon application front
* Mon application utilise le cloud service `users` qui me permet de gérer mes utilisateurs
* Je souhaiter tester mon code front, qui me permet de créer un utilisateur, pour ceci je mock l'appel à la cloud function `createUser()` suivant cette syntaxe :

  ```javascript
  var assert = require("assert");

  /**
   *    Test to check if a new user is correctly added to the array of all users
   */
  describe("Users", function() {
    describe("#checkUserAdded()", function() {
      it("User should be in allUsers array", async function() {
        /**
         *  Call the "UsersService" that is a cloud service to manage users.
         *  Here we create a new user (An ID is returned for each created user).
         */
        const newUser = await this.usersService
          .createUser({
            firstname: "Jean",
            lastname: "Martin"
          })
          /**
           *   We mock the call of our cloud service to return a specific object
           */
          .mock({ firstname: "Jean", lastname: "Martin", id: "7682164" });

        /**
         *  Function used front-side to handle the created users.
         *  Inter alia the function add the new user in the 'allUsers' array.
         */
        processNewUser(newUser);

        /**
         *  We add an assertion to check if the user is correctly added in 'allUsers' array.
         */
        assert.notEqual(allUsers.indexOf(newUser.id), -1);
      });
    });
  });
  ```

_WHEN_

* Lorsque je lance l'exécution de mon test

_THEN_

* L'appel à la cloud function ne se fait pas, un objet prédéfini est renvoyé en réponse
* Pour le code front, le mock de la cloud function est complètement transparent, le comportement (d'un point de vue front) est le même hormis la réponse renvoyée.

### ETQ dev je souhaite pouvoir appliquer à mon test un état de mon application précédemment sauvegardé

_GIVEN_

* J'ai une application front de développée
* J'ai l'ensemble des dépendances nécessaires à l'utilisation de ZetaPush dans mon application front
* Mon application utilise le cloud service `users` qui me permet de gérer mes utilisateurs
* Je souhaite donner un état particulier à mon application côté back. Pour ceci je spécifie un snapshot de mon application.
* Je souhaiter tester mon code front, qui me permet de créer un utilisateur, pour ceci je mock l'appel à la cloud function `createUser()` suivant cette syntaxe :

  ```javascript
  var assert = require("assert");

  /**
   *    Test to check if a new user is correctly added to the array of all users
   */
  describe("Users", function() {
    describe("#checkUserAdded()", function() {
      it("User should be in allUsers array", async function() {
        /**
         *    I specify the name of my snapshot. For this, I use the "setSnapshotName()" cloud function from the Utils cloud service.
         */
        await this.utilsService.setSnapshotName("3-users-already-created");

        /**
         *  Call the "UsersService" that is a cloud service to manage users.
         *  Here we create a new user (An ID is returned for each created user).
         */
        const newUser = await this.usersService.createUser({
          firstname: "Jean",
          lastname: "Martin"
        });

        /**
         *  Function used front-side to handle the created users.
         *  Inter alia the function add the new user in the 'allUsers' array.
         */
        processNewUser(newUser);

        /**
         *  We add an assertion to check if the user is correctly added in 'allUsers' array.
         */
        assert.notEqual(allUsers.indexOf(newUser.id), -1);
      });
    });
  });
  ```

_WHEN_

* Lorsque je lance l'exécution de mon test

_THEN_

* Mon test s'est lancé en prenant en compte l'état de mon application précédemment spécifié, ici un état où 3 utilisateurs sont déjà créés dans mon application côté back.
* On peut spécifier l'état de l'application de 3 manières :
  * this.utilsService.setSnapshotName(name-of-remote-snapshot);
  * this.utilsService.setSnapshotFile(path/to/local/snap);
  * this.utilsService.setToScratch();

### ETQ dev je teste mon application dans un environnement vierge

_GIVEN_

* J'ai une application front de développée
* J'ai l'ensemble des dépendances nécessaires à l'utilisation de ZetaPush dans mon application front
* Mon application utilise le cloud service `users` qui me permet de gérer mes utilisateurs
* Je souhaite que mon application soit en un état "neuf" pour le côté back.
* Je souhaiter tester mon code front, qui me permet de créer un utilisateur, pour ceci je mock l'appel à la cloud function `createUser()` suivant cette syntaxe :

  ```javascript
  var assert = require("assert");

  /**
   *    Test to check if a new user is correctly added to the array of all users
   */
  describe("Users", function() {
    describe("#checkUserAdded()", function() {
      it("User should be in allUsers array", async function() {
        /**
         *    I specify that I want to use a clean environment. For this, I use the "setToScratch()" cloud function from the Utils cloud service.
         */
        await this.utilsService.setToScratch();

        /**
         *  Call the "UsersService" that is a cloud service to manage users.
         *  Here we create a new user (An ID is returned for each created user).
         */
        const newUser = await this.usersService.createUser({
          firstname: "Jean",
          lastname: "Martin"
        });

        /**
         *  Function used front-side to handle the created users.
         *  Inter alia the function add the new user in the 'allUsers' array.
         */
        processNewUser(newUser);

        /**
         *  We add an assertion to check if the user is correctly added in 'allUsers' array.
         */
        assert.notEqual(allUsers.indexOf(newUser.id), -1);
      });
    });
  });
  ```

_WHEN_

* Lorsque je lance l'exécution de mon test

_THEN_

* Mon test s'est lancé en prenant en compte que mon application côté back est vierge.
* On peut spécifier l'état de l'application de 3 manières :
  * this.utilsService.setSnapshotName(name-of-remote-snapshot);
  * this.utilsService.setSnapshotFile(path/to/local/snap);
  * this.utilsService.setToScratch();

# <a name="parcours-2"></a> Parcours 2 : Je développe une application avec ZetaPush et des services customs

## User Stories

### ETQ dev full-stack je teste un service custom

_GIVEN_

* J'ai une application front de développée
* J'ai l'ensemble des dépendances nécessaires à l'utilisation de ZetaPush dans mon application front
* J'ai l'ensemble des dépendances nécessaires pour créer un custom cloud service
* J'ai le custom cloud service de créé et de déployé nommé _HealthDataManager_ et qui comporte la cloud function _pushNewHealthData()_
* Je souhaite tester unitairemenent le fonctionnement de _pushNewHealthData()_
* J'ai écris le test unitaire suivant :

  ```javascript
  /**
   *    Test to check if "pushNewHealthData()" is correctly working
   */
  describe("HealthData", function() {
    describe("#checkPushNewHealthData()", function() {
      it("The cloud function should return a specific object", async function() {
          /**
          * I specify the wanted object when we call the "pushNewHealthData" cloud function
          */
          const wantedResponse = { type: "heart", unit: "bpm", state: "added", value: "78"};

        /**
         *  We call our cloud function from our custom cloud service "HealthDataManager"
         */
         const response = this.healthDataManager.pushNewHealthData({
             type: "heart",
             value: "78"
         });

         /**
          * Check if the response is equal to wanted response
          */
        assert.equal(response, wantedResponse);
  ```

_WHEN_

* Lorsque je lance l'exécution de mon test

_THEN_

* Je reçois en réponse le retour de mon test conformément au framework utilisé
