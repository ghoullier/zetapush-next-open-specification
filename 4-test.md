# Objectifs

* Un développeur front doit pouvoir mocker les appels serveurs lors de ses tests.
* Un développeur full-stack doit pouvoir tester unitairement son code serveur.
* Un développeur doit pouvoir tester (test d'intégration ou test fonctionnel) son code avec un contexte d'exécution propre entre chaque test.
* Un développeur doit pouvoir spécifier dans son test, l'état dans lequel se trouve son application avant l'exécution du test.

# Objectifs à plus long terme

* Un développeur doit pouvoir exécuter ses tests en parallèle

---

# Pré-requis

* J'utilise mon éditeur de texte ou IDE préféré.
* J'ai une application front qui est prête à utiliser les cloud services. (Projet initialisé, dépendances installées, éventuellement la configuration de saisie)
* J'utilise mon framework de test préféré. Dans les exemples de syntaxe, nous utiliserons _Mocha_.

---

# <a name="parcours-1"></a> Parcours 1 : Je développe une application front avec ZetaPush sans _custom cloud service_

## User Stories

---

### ETQ dev je mock un appel à un _cloud service_

_GIVEN_

* J'ai une application front de développée
* J'ai importé le _cloud service_ `UsersService` qui me permet de gérer des utilisateurs
* J'ai accès à `UsersService` via l'objet `usersService`
* Je souhaiter tester mon code front, qui me permet de créer un utilisateur, pour ceci je mock l'appel à la _cloud function_ `createUser()` suivant cette syntaxe :

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

* L'appel à la cloud function ne se fait pas, un objet prédéfini est renvoyé en réponse (dans l'exemple : `{ firstname: "Jean", lastname: "Martin", id: "7682164" }`)
* Pour le code front, le mock de la _cloud function_ est complètement transparent, le comportement (d'un point de vue front) est le même hormis la réponse renvoyée.

---

### ETQ dev je souhaite pouvoir appliquer à mon test un état de mon application précédemment sauvegardé

_GIVEN_

* J'ai une application front de développée
* J'ai importé le _cloud service_ `UsersService` qui me permet de gérer des utilisateurs
* J'ai accès à `UsersService` via l'objet `usersService`
* J'ai importé le _cloud service_ `UtilsService` qui me permet d'utiliser des _cloud functions_ utilitaires de ZetaPush
* J'ai accès à `UtilsService` via l'objet `utilsService`
* Je souhaite donner un état particulier à mon application côté back. Pour ceci je spécifie un snapshot de mon application.
* Je souhaiter tester mon code front, qui me permet de créer un utilisateur, pour ceci je mock l'appel à la _cloud function_ `createUser()` suivant cette syntaxe :

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
  * `this.utilsService.setSnapshotName(name-of-remote-snapshot);`
  * `this.utilsService.setSnapshotFile(path/to/local/snap);`
  * `this.utilsService.setToScratch();`

---

### ETQ dev je teste mon application dans un environnement vierge

_GIVEN_

* J'ai une application front de développée
* J'ai importé le _cloud service_ `UsersService` qui me permet de gérer des utilisateurs
* J'ai accès à `UsersService` via l'objet `usersService`
* J'ai importé le _cloud service_ `UtilsService` qui me permet d'utiliser des _cloud functions_ utilitaires de ZetaPush
* J'ai accès à `UtilsService` via l'objet `utilsService`
* Je souhaite que mon application soit en un état vierge pour le côté back.
* Je souhaiter tester mon code front, qui me permet de créer un utilisateur, pour ceci je mock l'appel à la _cloud function_ `createUser()` suivant cette syntaxe :

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
  * `this.utilsService.setSnapshotName(name-of-remote-snapshot);`
  * `this.utilsService.setSnapshotFile(path/to/local/snap);`
  * `this.utilsService.setToScratch();`

# <a name="parcours-2"></a> Parcours 2 : Je développe une application avec ZetaPush et des _custom cloud services_

## User Stories


---

### ETQ dev full-stack je teste un _custom cloud service_

_GIVEN_

* J'ai une application front de développée
* J'ai un _custom cloud service_ de créé et de déployé nommé `HealthDataManager` et qui comporte la _cloud function_ `pushNewHealthData()`
* Je souhaite tester unitairement le fonctionnement de `pushNewHealthData()`
* J'ai écrit le test unitaire suivant :

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
* Les éventuelles actions réalisées côté back sont effectives sur l'application (Pas de contexte neuf de spécifié)

---

### ETQ dev full-stack je teste un _custom cloud service_ dans un nouveau contexte

_GIVEN_

* J'ai une application front de développée
* J'ai un _custom cloud service_ de créé et de déployé nommé `HealthDataManager` et qui comporte la _cloud function_ `pushNewHealthData()`
* Je souhaite tester unitairement le fonctionnement de `pushNewHealthData()`
* Je souhaite que les actions côté serveur n'affecte pas mon application et que j'exécute mon application dans un nouveau contexte "jetable"
* J'ai importé le _cloud service_ `UtilsService` qui me permet d'utiliser des _cloud functions_ utilitaires de ZetaPush
* J'ai accès à `UtilsService` via l'objet `utilsService`
* J'ai écrit le test unitaire suivant :

  ```javascript
  /**
   *    Test to check if "pushNewHealthData()" is correctly working
   */
  describe("HealthData", function() {
    describe("#checkPushNewHealthData()", function() {
      it("The cloud function should return a specific object", async function() {
          /**
          * I specify that I use a new context to execute my test
          */
          await this.utilsService.workInDisposableContext();

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
* Le test s'est exécuté dans un contexte neuf et jetable
* Les éventuelles actions réalisées côté back n'ont pas affecté l'application