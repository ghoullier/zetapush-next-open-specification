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
* Nous allons utiliser _sinon.js_ pour réaliser dans mocks et des stubs dans nos tests.
* Le cas d'usage de nos Users Stories sera un chat temps réel entre des personnages Avengers.

---

# <a name="parcours-1"></a> Parcours 1 : Je développe une application front avec ZetaPush sans _custom cloud service_

## User Stories

---

### ETQ dev je mock un appel à un _cloud service_

_GIVEN_

* Je suis en cours de développement de mon _Avengers Chat_
* J'ai importé le _cloud service_ `UserService` qui me permet de gérer des utilisateurs
* J'ai importé le _cloud service_ `SearchService` qui me permet de sauvegarder dans un moteur de recherche des données
* J'ai accès à `UserService` via l'objet `userService`
* J'ai accès à `SearchService` via l'objet `searchService`
* Je souhaiter tester mon code front, qui me permet de créer un _Avenger_ pour ceci je mock mes différents appels aux _Cloud Services_ pour tester uniquement mon code front
* J'ai une fonction côté front qui intègre ma logique métier :

```javascript
addAvengers(avenger) {
  // Create a new user using the UserService Cloud Service
  const newUser = await this.userService.createUser({
    "username": avenger.name, // This field will be displayed in the chat
    "firstname": avenger.realIdentity.firstname,
    "lastname": avenger.realIdentity.lastname
  });

  // Add the id of the created user in our Avenger
  avenger.id = newUser.id;

  // Store the Avengers in search engine to get it from his superpowers
  for (let superpower of avenger.superpowers) {
    // We only ask to store the data, we don't use the response
    this.searchService.index({ type: "avengers", index: "avengers-by-superpowers", "id": newUser.id+'-'+superpower.name, "data": { superpower: superpower.name, avenger: avenger}});
  }
  return avenger
}
```

* Nous utilisons _sinon.js_ pour tester mocker les appels aux _Cloud Services_.


  ```javascript
  var assert = require("assert");
  var sinon = require("sinon");

  /**
   *    Test to check if a new user is correctly added to the array of all users
   */
  describe("Users", function() {
    describe("#checkUserAdded()", function() {
      it("User should be in allUsers array", async function() {

        /**
         *  Use Add stub on UserService and SearchService to avoid call to Cloud Services
         */
        const createUserStub = sinon.stub(this.userService, "createUser");
        createUserStub.withArgs({username: "Spiderman", firstname: "Peter", lastname: "Parker"}).returns({username: "Spiderman", firstname: "Peter", lastname: "Parker", id: "7682164"});
        // We only mock SearchService because we don't care about the result
        const searchMock = sinon.mock(this.searchService);

        /**
         *  We call our function to add a new Avengers
         */
        addAvenger({
          name: "Spiderman", 
          realIdentity: {firstname: "Peter", lastname: "Parker", profession: "freelance photographer"},
          superpowers: ["web-shooters", "spider-sense"]);
        });

        /**
         *  We check if the avenger is correctly added in the search engine
         */
        searchMock.expects("index").twice();

        /**
         *  Ensure that we have the correct ID
         */
        assert.notNull(avenger.id);
    });
  });
  ```

_WHEN_

* Lorsque je lance l'exécution de mon test

_THEN_

* L'appel à la cloud function ne se fait pas, un objet prédéfini est renvoyé en réponse conformément à l'utilisation de _sinon.js_
* Pour le code front, le mock de la _cloud function_ est complètement transparent, le comportement (d'un point de vue front) est le même hormis la réponse renvoyée.

---

### ETQ dev je souhaite pouvoir appliquer à mon test un état de mon application précédemment sauvegardé

_GIVEN_

* Je suis en cours de développement de mon _Avengers Chat_
* J'ai importé le _cloud service_ `UserService` qui me permet de gérer des utilisateurs
* J'ai importé le _cloud service_ `SearchService` qui me permet de sauvegarder dans un moteur de recherche des données
* J'ai accès à `UserService` via l'objet `userService`
* J'ai accès à `SearchService` via l'objet `searchService`
* J'ai importé le _cloud service_ `UtilsService` qui me permet d'utiliser des _cloud functions_ utilitaires de ZetaPush
* J'ai accès à `UtilsService` via l'objet `utilsService`
* Je souhaite donner un état particulier à mon application côté back. Pour ceci je spécifie un snapshot de mon application.
* Je souhaiter tester mon code front, qui me permet de créer un _Avenger_ pour ceci je mock mes différents appels aux _Cloud Services_ pour tester uniquement mon code front
* J'ai un état précédent de mon application sauvegardé côté back, que je peux retrouver avec le nom `3-avengers-already-created`
* J'ai une fonction côté front qui intègre ma logique métier :

```javascript
addAvengers(avenger) {
  // Create a new user using the UserService Cloud Service
  const newUser = await this.userService.createUser({
    "username": avenger.name, // This field will be displayed in the chat
    "firstname": avenger.realIdentity.firstname,
    "lastname": avenger.realIdentity.lastname
  });

  // Add the id of the created user in our Avenger
  avenger.id = newUser.id;

  // Store the Avengers in search engine to get it from his superpowers
  for (let superpower of avenger.superpowers) {
    // We only ask to store the data, we don't use the response
    this.searchService.index({ type: "avengers", index: "avengers-by-superpowers", "id": newUser.id+'-'+superpower.name, "data": { superpower: superpower.name, avenger: avenger}});
  }
  return avenger
}
```


* Nous utilisons _sinon.js_ pour tester mocker les appels aux _Cloud Services_.


  ```javascript
  var assert = require("assert");
  var sinon = require("sinon");

  /**
   *    Test to check if a new user is correctly added to the array of all users
   */
  describe("Users", function() {
    describe("#checkUserAdded()", function() {
      it("User should be in allUsers array", async function() {

        /**
         *    I specify the name of my snapshot. For this, I use the "setSnapshotName()" cloud function from the Utils cloud service.
         */
        await this.utilsService.setSnapshotName("3-avengers-already-created");


        /**
         *  Use Add stub on UserService and SearchService to avoid call to Cloud Services
         */
        const createUserStub = sinon.stub(this.userService, "createUser");
        createUserStub.withArgs({username: "Spiderman", firstname: "Peter", lastname: "Parker"}).returns({username: "Spiderman", firstname: "Peter", lastname: "Parker", id: "7682164"});
        // We only mock SearchService because we don't care about the result
        const searchMock = sinon.mock(this.searchService);

        /**
         *  We call our function to add a new Avengers
         */
        addAvenger({
          name: "Spiderman", 
          realIdentity: {firstname: "Peter", lastname: "Parker", profession: "freelance photographer"},
          superpowers: ["web-shooters", "spider-sense"]);
        });

        /**
         *  We check if the avenger is correctly added in the search engine
         */
        searchMock.expects("index").twice();

        /**
         *  Ensure that we have the correct ID
         */
        assert.notNull(avenger.id);
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

* Je suis en cours de développement de mon _Avengers Chat_
* J'ai importé le _cloud service_ `UserService` qui me permet de gérer des utilisateurs
* J'ai importé le _cloud service_ `SearchService` qui me permet de sauvegarder dans un moteur de recherche des données
* J'ai accès à `UserService` via l'objet `userService`
* J'ai accès à `SearchService` via l'objet `searchService`
* J'ai importé le _cloud service_ `UtilsService` qui me permet d'utiliser des _cloud functions_ utilitaires de ZetaPush
* J'ai accès à `UtilsService` via l'objet `utilsService`
* Je souhaite donner un état particulier à mon application côté back. Pour ceci je spécifie un snapshot de mon application.
* Je souhaiter tester mon code front, qui me permet de créer un _Avenger_ pour ceci je mock mes différents appels aux _Cloud Services_ pour tester uniquement mon code front
* Je souhaite revenir à un état précédent de mon application, où la plateforme côté back est vierge
* J'ai une fonction côté front qui intègre ma logique métier :

```javascript
addAvengers(avenger) {
  // Create a new user using the UserService Cloud Service
  const newUser = await this.userService.createUser({
    "username": avenger.name, // This field will be displayed in the chat
    "firstname": avenger.realIdentity.firstname,
    "lastname": avenger.realIdentity.lastname
  });

  // Add the id of the created user in our Avenger
  avenger.id = newUser.id;

  // Store the Avengers in search engine to get it from his superpowers
  for (let superpower of avenger.superpowers) {
    // We only ask to store the data, we don't use the response
    this.searchService.index({ type: "avengers", index: "avengers-by-superpowers", "id": newUser.id+'-'+superpower.name, "data": { superpower: superpower.name, avenger: avenger}});
  }
  return avenger
}
```


* Nous utilisons _sinon.js_ pour tester mocker les appels aux _Cloud Services_.


  ```javascript
  var assert = require("assert");
  var sinon = require("sinon");

  /**
   *    Test to check if a new user is correctly added to the array of all users
   */
  describe("Users", function() {
    describe("#checkUserAdded()", function() {
      it("User should be in allUsers array", async function() {

        /**
         *    I specify that I want to go to state "from scratch" of my application
         */
        await this.utilsService.setToScratch();


        /**
         *  Use Add stub on UserService and SearchService to avoid call to Cloud Services
         */
        const createUserStub = sinon.stub(this.userService, "createUser");
        createUserStub.withArgs({username: "Spiderman", firstname: "Peter", lastname: "Parker"}).returns({username: "Spiderman", firstname: "Peter", lastname: "Parker", id: "7682164"});
        // We only mock SearchService because we don't care about the result
        const searchMock = sinon.mock(this.searchService);

        /**
         *  We call our function to add a new Avengers
         */
        addAvenger({
          name: "Spiderman", 
          realIdentity: {firstname: "Peter", lastname: "Parker", profession: "freelance photographer"},
          superpowers: ["web-shooters", "spider-sense"]);
        });

        /**
         *  We check if the avenger is correctly added in the search engine
         */
        searchMock.expects("index").twice();

        /**
         *  Ensure that we have the correct ID
         */
        assert.notNull(avenger.id);
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


# <a name="parcours-2"></a> Parcours 2 : Je développe une application avec ZetaPush et des _custom cloud services_

## User Stories


---

### ETQ dev full-stack je teste un _custom cloud service_

_GIVEN_

* Je suis en cours de développement de mon _Avengers Chat_
* J'ai importé le _cloud service_ `UserService` qui me permet de gérer des utilisateurs
* J'ai accès à `UserService` via l'objet `userService`
* J'ai un _custom cloud service_ de créé et de déployé nommé `AvengersService` et qui comporte la _cloud function_ `attackWithRandomSkill()` :

```javascript
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



* Je souhaite tester unitairement le fonctionnement de `attackWithRandomSkill()`
* J'ai écrit le test unitaire suivant :

  ```javascript
  /**
   *    Test to check if "attackWithRandomSkill()" is correctly working
   */
  describe("HealthData", function() {
    describe("#checkAttackWithRandomSkill()", function() {
      it("The cloud function should return a specific object", async function() {


        /**
         *  I create one Avenger
         */
        addAvenger({
          name: "Spiderman", 
          realIdentity: {firstname: "Peter", lastname: "Parker", profession: "freelance photographer"},
          superpowers: ["web-shooters", "spider-sense"]);
        });

        /**
         *  I attack with this user
         */
        const resultAttack = attackWithRandomSkill("Spiderman");
        


         /**
          * Check if the response is not null
          */
        assert.notNull(resultAttack);
  ```

_WHEN_

* Lorsque je lance l'exécution de mon test

_THEN_

* Je reçois en réponse le retour de mon test conformément au framework utilisé
* Les éventuelles actions réalisées côté back sont effectives sur l'application (Pas de contexte neuf de spécifié)

---

### ETQ dev full-stack je teste un _custom cloud service_ dans un nouveau contexte

_GIVEN_

* Je suis en cours de développement de mon _Avengers Chat_
* J'ai importé le _cloud service_ `UserService` qui me permet de gérer des utilisateurs
* J'ai accès à `UserService` via l'objet `userService`
* J'ai importé le _cloud service_ `UtilsService` qui me permet d'utiliser des _cloud functions_ utilitaires de ZetaPush
* J'ai accès à `UtilsService` via l'objet `utilsService`
* Je souhaite que les actions côté serveur n'affecte pas mon application et que j'exécute mon application dans un nouveau contexte "jetable"
* J'ai un _custom cloud service_ de créé et de déployé nommé `AvengersService` et qui comporte la _cloud function_ `attackWithRandomSkill()` :

```javascript
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



* Je souhaite tester unitairement le fonctionnement de `attackWithRandomSkill()`
* J'ai écrit le test unitaire suivant :

  ```javascript
  /**
   *    Test to check if "attackWithRandomSkill()" is correctly working
   */
  describe("HealthData", function() {
    describe("#checkAttackWithRandomSkill()", function() {
      it("The cloud function should return a specific object", async function() {
        /**
         * I specify that I use a new context to execute my test
         */
        await this.utilsService.workInDisposableContext();

        /**
         *  I create one Avenger
         */
        addAvenger({
          name: "Spiderman", 
          realIdentity: {firstname: "Peter", lastname: "Parker", profession: "freelance photographer"},
          superpowers: ["web-shooters", "spider-sense"]);
        });

        /**
         *  I attack with this user
         */
        const resultAttack = attackWithRandomSkill("Spiderman");
        


         /**
          * Check if the response is not null
          */
        assert.notNull(resultAttack);
  ```

_WHEN_

* Lorsque je lance l'exécution de mon test

_THEN_

* Je reçois en réponse le retour de mon test conformément au framework utilisé
* Le test s'est exécuté dans un contexte neuf et jetable
* Les éventuelles actions réalisées côté back n'ont pas affecté l'application