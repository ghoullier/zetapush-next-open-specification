# Objectifs

* Un développeur doit pouvoir appeler un service (ZetaPush ou custom) et avoir une réponse en retour.
* Un développeur doit pouvoir développer son code métier dans des services custom.
* Un développeur doit pouvoir utiliser l'autocomplétion de son IDE pour l'aider dans le développement ou les appels de service ZetaPush.
* Un développeur doit avoir accès depuis son IDE à la documentation des services ZetaPush.
* Un développeur doit pouvoir écouter les évènements des services ZetaPush.

Les profils utilisés sont définis dans [commun.md](./commun.md).

---

# Pré-requis

* J'ai un compte sur ZetaPush
* J'ai une application front qui est configurée pour utiliser ZetaPush

## Schéma

![Développement](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/dev-front-interaction-services-zetapush.html)

### Explications

* Depuis son environnement local, le développeur modifie son application en agissant sur la partie front et les appels aux services (ZetaPush ou custom)
* Le développeur peut créer son code métier, soit en utilisant un "starter" sur `console.zetapush.com`, soit par du développement local. Ensuite, quelque soit la manière, le développeur déploie son code métier sur la plateforme ZetaPush.

---

# <a name="parcours-1"></a> Parcours 1 : Je développe une application front avec ZetaPush sans service custom

## Schéma

![Développement avec seulement les services ZetaPush](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/archi-dev-front-zp-service-only.html)

## User Stories

---

### ETQ dev front j'utilise les services ZetaPush et avoir une réponse en retour

_GIVEN_

* J'ai importé la dépendance npm nécessaire pour appeler un service ZetaPush
* J'ai un objet `zpService` qui me permet d'appeler les services ZetaPush

_WHEN_

* Lorsque j'appelle un service ZetaPush en attendant une réponse, par exemple :

```javascript
this.zpService
  .createUser({ login, password })
  .then(user => {
    console.log("UserCreated", user);
  })
  .catch(err => {
    console.error("ErrorCreateUser", err);
  });
```

_THEN_

* L'appel au service ZetaPush se fait et une réponse est renvoyée
* La réponse et les éventuelles erreurs sont renvoyées en même temps en utilisant une promesse, async+await, RxJS ou tout autre système similaire

---

### ETQ dev front j'utilise l'autocompletion de mon IDE (VSCode) pour découvrir et utiliser les services ZetaPush

_GIVEN_

* J'utilise Visual Studio Code comme IDE
* J'ai importé la dépendance npm nécessaire pour appeler un service ZetaPush
* J'ai un objet `zpService` qui me permet d'appeler les services ZetaPush
* Je souhaite appeler un service ZetaPush, pour créer un utilisateur par exemple
* J'ai différents services ZetaPush : `createUser()` / `createData()` / `searchCreatedUser()` / `pushData()`

_WHEN_

* Lorsque je commence à écrire mon appel au service ZetaPush : `this.zpService.create`

_THEN_

* L'autocompletion me propose les différents services auquels je peux accèder en fonction de ma saisie :
  * this.zpService.createUser()
  * this.zpService.createData()
  * this.zpService.searchCreatedUser()

---

### ETQ dev front j'écoute les évènements d'un service ZetaPush

_GIVEN_

* J'ai importé la dépendance npm nécessaire pour appeler un service ZetaPush
* J'ai un objet `zpService` qui me permet d'appeler les services ZetaPush et d'écouter les évènements
* Je souhaite écouter les évènements d'un service ZetaPush, dans notre exemple la création d'utilisateur
* J'ajoute par exemple une callback sur un évènement :

```javascript
this.zpService.onUserCreated = user => {
  console.log(`User created : ${user.name}`);
};
```

_WHEN_

* Lorsqu'un nouvel utilisateur est créé sur mon application

_THEN_

* Mon évènement associé à `onUserCreated` est appelée. Dans l'exemple, le message `User created : Toto` est affiché dans la console

---

### ETQ dev front j'ai accès à la documentation des services ZetaPush depuis mon IDE (VSCode)

_GIVEN_

* J'utilise Visual Studio Code comme IDE
* J'ai importé la dépendance npm nécessaire pour appeler un service ZetaPush
* J'ai un objet `zpService` qui me permet d'appeler les services ZetaPush
* Je souhaite me renseigner sur un service ZetaPush
* J'utilise l'autocompletion pour afficher les différents services auquels j'ai accès

_WHEN_

* Lorsqu'un service est en surbrillance dans mon IDE avec l'autocompletion

_THEN_

* La documentation du service concerné est affiché dans l'IDE avec son nom, sa description, ses paramètres entrants et son retour

---

# <a name="parcours-2"></a> Parcours 2 : Je développe une application avec ZetaPush et des services custom

## Schéma

![Développement avec seulement les services ZetaPush](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/archi-dev-front-with-custom-service.html)

## User Stories

---

### ETQ dev je développe mon code métier dans un service custom

_GIVEN_

* J'ai importé les dépendancenpm s nécessaires pour créer un service custom
* J'écris mon service custom, exemple :

```javascript
function createGame({name: string}): Promise<any> {
  ...
}
```

_WHEN_

* Lorsque je publie mon service custom dans mon application

_THEN_

* Je peux utiliser mon service custom de la même manière qu'un service ZetaPush existant
* Je peux l'appeler avec la syntaxe :

```javascript
this.zpService
  .createGame({ name })
  .then(game => {
    console.log(`GameCreated : ${game.name}`);
  })
  .catch(err => {
    console.error(`ErrorCreateGame : ${err}`);
  });
```

* Un évènement peut être écouté lorsqu'un appel à ce service est fait avec la syntaxe :

```javascript
this.zpService.onCreateGame = result => {
  console.log(`CreateGameEvent : ${result}`);
};
```

---

### ETQ dev j'utilise mes services custom et avoir une réponse en retour

_GIVEN_

* J'ai importé la dépendance npm nécessaire pour appeler un service ZetaPush
* J'ai un objet `zpService` qui me permet d'appeler les services ZetaPush
* J'ai déjà créé un service custom, exemple : `createGame()`
* Mon service custom a été déployé sur ZetaPush
* J'ai écrit l'appel à mon service custom :

```javascript
this.zpService
  .createGame({ name })
  .then(game => {
    console.log("gameCreated", game);
  })
  .catch(err => {
    console.error("ErrorCreateGame", err);
  });
```

_WHEN_

* Lorsque j'appelle mon service custom

_THEN_

* L'appel au service custom se fait et une réponse est renvoyée
* La réponse et les éventuelles erreurs sont renvoyées en même temps en utilisant une promesse, async+await, RxJS ou tout autre système similaire

---

### ETQ dev j'utilise l'autocompletion de mon IDE (VSCode) pour découvrir et utiliser mes services custom

_GIVEN_

* J'utilise Visual Studio Code comme IDE
* J'ai importé la dépendance npm nécessaire pour appeler un service ZetaPush ou custom déployés
* J'ai un objet `zpService` qui me permet d'appeler les services ZetaPush ou custom déployés
* Je souhaite appeler un service custom, `createGame()` par exemple

_WHEN_

* Lorsque je commence à écrire mon appel au service ZetaPush : `this.zpService.create`

_THEN_

* L'autocompletion me propose les différents services auquels je peux accèder en fonction de ma saisie :
  * this.zpService.createUser()
  * this.zpService.createGame()
  * this.zpService.createOrganization()
  * this.zpService.createRoom()
  * ...
* L'autocompletion ne fait pas de distinction entre un service ZetaPush ou un service custom déployé

---

### ETQ dev j'écoute les évènements d'un service custom

_GIVEN_

* J'ai importé la dépendance npm nécessaire pour appeler un service ZetaPush ou un service custom déployé
* J'ai un objet `zpService` qui me permet d'appeler les services ZetaPush ou un service custom déployé et d'écouter les évènements
* Je souhaite écouter les évènements d'un service custom que j'ai créé, dans notre exemple l'évènement de création de jeu
* Le service custom est déployé sur mon application
* J'ajoute par exemple une callback sur un évènement :

```javascript
this.zpService.onCreateGame = result => {
  console.log(`GameCreatedEvent : ${result}`);
};
```

_WHEN_

* Lorsque le service custom appelé, `createGame()` dans l'exemple

_THEN_

* Mon évènement associé (`onCreateGame` dans l'exemple) est appelée.

---

### ETQ dev j'ai accès à la documentation de mes services custom depuis mon IDE (VSCode)

_GIVEN_

* J'utilise Visual Studio Code comme IDE
* J'ai importé la dépendance npm nécessaire pour appeler un service ZetaPush ou un service custom déployé
* J'ai un objet `zpService` qui me permet d'appeler les services ZetaPush ou un service custom déployé
* Je souhaite me renseigner sur un service custom que j'ai créé
* Mon service custom est déployé sur mon application
* J'ai documenté mon code en suivant les bonnes pratiques de documentation de mon code
* J'utilise l'autocompletion pour afficher les différents services auquels j'ai accès

_WHEN_

* Lorsqu'un service est en surbrillance dans mon IDE avec l'autocompletion

_THEN_

* La documentation du service concerné est affiché dans l'IDE avec son nom, sa description, ses paramètres entrants et son retour
* L'affichage de la documentation et de l'autocompletion ne fait aucune distinction entre un service ZetaPush ou un service custom
* La documentation du service custom se base sur les commentaires et types lors de la création de ce service

---

# <a name="parcours-3"></a> Parcours 3 : Mon équipe développe une application front avec ZetaPush sans services custom

## Schéma

TODO

## User Stories

TODO

### ETQ équipe de dev front, nous souhaitons utiliser les services ZetaPush

---

# <a name="parcours-4"></a> Parcours 4 : Mon équipe développe une application avec ZetaPush et des services custom

## Schéma

TODO

## User Stories

TODO

### ETQ équipe de dev front, nous souhaitons utiliser les services custom ZetaPush
