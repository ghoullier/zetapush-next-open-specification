
# Objectifs

- Un développeur doit pouvoir appeler un service (ZetaPush ou custom) et avoir une promesse en retour.
- Un développeur doit pouvoir utiliser l'autocomplétion de son IDE pour l'aider dans le développement ou les appels de service ZetaPush.
- Un développeur doit avoir accès depuis son IDE à la documentation des services ZetaPush.
- Un développeur doit pouvoir associer une callback à un service ZetaPush pour être notifié des différents évènements.
- Un développeur doit pouvoir spécifier quels évnèments il souhaite exposer sur ses services custom.


Les profils utilisés sont définis dans [commun.md](./commun.md).

***

# Pré-requis

- J'ai un compte sur ZetaPush
- J'ai une application front qui est configurée pour utiliser ZetaPush

***

# <a name="parcours-1"></a> Parcours 1 : Je développe une application front avec ZetaPush sans service custom

## User Stories

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
  - Lorsque j'exécute mon appel au service ZetaPush, à la création d'un utilisateur dans l'exemple

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

## User Stories

### ETQ dev je souhaite utiliser les services custom ZetaPush

### ETQ dev je souhaite utiliser l'autocompletion de mon IDE pour utiliser les services custom créés dans mon application
  
### ETQ dev je souhaite avoir une promesse en retour lorsque j'appelle un service custom

### ETQ dev front je souhaite pouvoir m'abonner à un obervable pour écouter les messages d'un service custom

***

# <a name="parcours-3"></a> Parcours 3 : Mon équipe développe une application front avec ZetaPush sans services custom

## User Stories

### ETQ équipe de dev front, nous souhaitons utiliser les services ZetaPush


  


***

# <a name="parcours-4"></a> Parcours 4 : Mon équipe développe une application avec ZetaPush et des services custom

## User Stories

### ETQ équipe de dev front, nous souhaitons utiliser les services custom ZetaPush

  


