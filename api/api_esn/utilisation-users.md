# Description d'utilisation du _UserService_

## Introduction

- Pour utiliser un service il faut créer une instance de ce dernier sous la forme : `const userService = new UserService()`.
- Plusieurs instances de _UserService_ sont utilisables dans une seule application. Dans ce cas, les données sont strictement séparées (comportement par défaut).

Nous allons voir chaque cas d'usage pour décrire l'utilisation de _UserService_.

## Cas d'utilisation

---

### CRUD des utilisateurs

#### Création d'un utilisateur

Dans ce cas, nous voulons créer un utilisateur.

```javascript
// Create a new instance of UserService
const userService = new UserService();

// Create a new user
const newUser = await userService.createUser({ login: "antoine", password: "password", properties: { firstname: "Antoine", lastname: "Martin" }});
```

Chaque utilisateur créé a un ID qui est auto-généré.
Le format du nouvel utilisateur créé est :

```json
{
    "id": "generated_id",
    "login": "antoine",
    "password": "password", 
    "firstname": "Antoine",
    "lastname": "Martin"
}
```
Il est possible de donner manuellement l'ID en suivant cette syntaxe :

```javascript
const newUser = await userService.createUser({ login: "antoine", password: "password", properties: { firstname: "Antoine", lastname: "Martin", id: "my-user-id" }});
```

#### Suppression d'un utilisateur unique

Dans ce cas, nous voulons supprimer un utilisateur. Nous avons deux manières de faire, soit une suppression par login, soit par ID.
La suppression renvoi l'utilisateur supprimé.

L'appel de _Cloud Function_ est la même, voici les deux syntaxes :

```javascript
// Create a new instance of UserService
const userService = new UserService();

const deletedUser = await deleteUser({ login: "antoine" });
// OR
const deletedUser = await deleteUser({ id: "my-user-id"});
```

#### Suppression d'un ensemble d'utilisateurs

Dans ce cas, nous voulons pouvoir supprimer un ensemble d'utilisateurs, en fonction d'une requête.

```javascript
// Create a new instance of UserService
const userService = new UserService();

// Create 3 users with specific role
const newUser1 = await userService.createUser({ login: "antoine", password: "password", properties: { role: "admin"});
const newUser2 = await userService.createUser({ login: "martin", password: "password", properties: { role: "user"});
const newUser3 = await userService.createUser({ login: "grégoire", password: "password", properties: { role: "user"});

// I want to delete all users with the role "user"
const deletedUser = await userService.deleteUsersByRequest({ request: function(user) {
    return user.role === "user";
}});
```

Le paramètre `request` prend en paramètre une fonction qui doit retourner un boolean en fonction d'un utilisateur en entrée.
Si le boolean renvoi `true`, l'utilisateur concerné est supprimé.

#### Récupération d'un utilisateur unique

Dans ce cas, nous voulons récupérer un utilisateur. Nous avons deux manières de faire, soit une récupération par login, soit par ID.
La suppression renvoi l'utilisateur supprimé.

L'appel de _Cloud Function_ est la même, voici les deux syntaxes :

```javascript
// Create a new instance of UserService
const userService = new UserService();

const user = await getUser({ login: "antoine" });
// OR
const user = await getUser({ id: "my-user-id"});
```

#### Récupération d'un ensemble d'utilisateurs

Dans ce cas, nous voulons pouvoir récupérer un ensemble d'utilisateurs, en fonction d'une requête.

```javascript
// Create a new instance of UserService
const userService = new UserService();

// Create 3 users with specific role
const newUser1 = await userService.createUser({ login: "antoine", password: "password", properties: { role: "admin"});
const newUser2 = await userService.createUser({ login: "martin", password: "password", properties: { role: "user"});
const newUser3 = await userService.createUser({ login: "gregoire", password: "password", properties: { role: "user"});

// I want to get all users with the role "user"
const users = await userService.getUsersByRequest({ request: function(user) {
    return user.role === "user";
}});
```

Le paramètre `request` prend en paramètre une fonction qui doit retourner un boolean en fonction d'un utilisateur en entrée.
Si le boolean renvoi `true`, l'utilisateur concerné est renvoyé.

#### Mise à jour d'un utilisateur

Dans ce cas, nous voulons mettre à jour un utilisateur existant.

```javascript
// Create a new instance of UserService
const userService = new UserService();

// Create one user with specific role
const newUser = await userService.createUser({ id: "my-user", login: "antoine", password: "password", properties: { role: "user"});

// I want to change the role of an user
const updatedUser = await userService.updateUser({ id: "my-user", properties: { role: "admin" }});
```

On peut identifier un utilisateur à mettre à jour par son login :

```javascript
// I want to change the role of an user
const updatedUser = await userService.updateUser({ login: "antoine", properties: { role: "admin" }});
```

Il est aussi possible de mettre à jour plusieurs utilisateurs en même temps.
Pour ceci nous utilisons un paramètre `request` pour sélectionner les utilisateurs concernés.
Voici la syntaxe :

```javascript
// Create a new instance of UserService
const userService = new UserService();

// Create one user with specific role
const newUser1 = await userService.createUser({ login: "antoine", password: "password", properties: { role: "admin"});
const newUser2 = await userService.createUser({ login: "martin", password: "password", properties: { role: "user"});
const newUser3 = await userService.createUser({ login: "gregoire", password: "password", properties: { role: "user"});

// I want to change all "user" to "admin"
const updatedUsers = await userService.updateUsersByRequest({ request: function(user) {
    return user.role == "user";
}, properties: { role: "admin" }});
```

### Gestion de la présence

#### Récupération de la présence d'un utilisateur

Dans ce cas, nous voulons connaitre l'état de connexion d'un utilisateur.
Il est possible de récupérer la présence à partir de l'ID ou du login de l'utilisateur.

```javascript
// Create a new instance of UserService
const userService = new UserService();

// Create one user
const newUser = await userService.createUser({ id: "my-user", login: "antoine", password: "password"});

// Get the state of the connection for a specfic user
const presence = await userService.getPresence({ id: "my-user" });
// OR
const presence = await userService.getPresence({ login: "antoine" });
```

#### Écoute des changements de connexion d'un utilisateur

Dans ce cas, nous voulons être notifié des changements de connexion d'un utilisateur particulier.

```javascript
// Create a new instance of UserService
const userService = new UserService();

// Create one user
const newUser = await userService.createUser({ id: "my-user", login: "antoine", password: "password"});

// Listen the presence
userService.listenPresenceChanges(function(presence) => {
    console.log(`The user ${presence.user.login} has new presence state : ${presence.value} at the timestamp : ${presence.timestamp}`);
});
```

### Utilisation de plusieurs _UserServices_

#### Utiliser deux services distincts

Dans ce cas, nous voulons avoir deux services de gestion des utilisateurs qui sont différents et complètement distincts. Pour ceci, il suffit de créer deux instances de `UserService`, par défaut les données sont strictements séparées.

```javascript
// Create a first instance of UserService
const userService1 = new UserService();

// Create a second instance of UserService
const userService2 = new UserService();
```

#### Utiliser deux services distincts mais avec les données partagées

Il est possible d'avoir plusieurs services distincts qui partagent les mêmes données. Pour ça il faut identifier chaque service par le même ID.

```javascript
// Create two instances of UserService that have different data
const userService1 = new UserService({ id: "my-service-1"});
const userService2 = new UserService({ id: "my-service-2"});

// Create two instances of UserService that have same data
const userService3 = new UserService({ id: "my-service-global"});
const userService4 = new UserService({ id: "my-service-global"});
```
