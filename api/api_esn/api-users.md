# Cloud Functions pour le service _UserService_

---

# **TODO : Revoir façon de faire et mettre en cas d'utilisations** 

---

## Précisions

### Création d'utilisateurs et de groupes

Lorsqu'un utilisateur ou un groupe d'utilisateur est créé, un ID lui est affecté pour permettre de l'identifier de manière unique. Cet ID est renvoyé lors de la création d'utilisateur (idem pour les groupes).

### Properties d'un utilisateur

Lors de la création d'utilisateur, il est possible d'ajouter des properties au choix. (firstname, lastname, email, age...). Ces données sont au même niveau que le _login_ et le _password_ dans l'objet créé. Par exemple nous créons un utilisateur avec :

```javascript
/**
 *  We can access to "UserService" by "userService" variable
 *  The cloud function return a promise, we display the result into this result
 */
this.userService.createUser({
    login: "antoine",
    password: "password",
    properties: {
        "firstname": "Antoine",
        "lastname": "Martin"
    }
}).then((createdUser) => {
    console.log(`Created user : ${createdUser.firstname} ${createdUser.lastname}`);
});
```

L'objet sauvegardé en base pour la création de cet utilisateur est :

```json
{
    "id": "my_long_user_id",
    "login": "antoine",
    "password": "password",
    "firstname": "Antoine",
    "lastname": "Martin"
}
```

### Mise à jour d'un utilisateur

Les _cloud functions_ `updateUserById( id, properties )` et `updateUserByLogin( login, properties )` permettent de mettre à jour les propriétées d'un utilisateur. 
En revanche, seulement les données envoyées dans le paramètre "properties" sont modifiées. Par exemple si nous avons un utilisateur :

```json
{
    "id": "my_long_user_id",
    "login": "antoine",
    "password": "password",
    "firstname": "Antoine",
    "lastname": "Martin",
    "age": 23
}
```

Et que nous voulons seulement mettre à jour l'age, nous avons seulement à faire :

```javascript
/**
 *  We can access to "UserService" by "userService" variable
 */
this.userService.updateUserByLogin({
    login: "antoine",
    properties: {
        "age": 24
    }
});
```

## Cloud Functions

```javascript
/**
 *  Create an user with a specific login, password and additional properties
 *  @param {string} login - Login of the created user
 *  @param {string} password - Password of the created user
 *  @param {object} properties - Additional properties with JSON format.
 *  @return {Promise<Object>} - Return the created user
 */
function createUser({ login, password, properties });
```

```javascript
/**
 *  Get an user from his ID
 *  @param {string} id - ID of the user
 *  @return {Promise<Object>} - Return the user
 */
function getUserById({ id });
```

```javascript
/**
 *  Get an user from his login
 *  @param {string} login - Login of the user
 *  @return {Promise<Object>} - Return the user
 */
function getUserByLogin({ login });
```

```javascript
/**
 *  Delete an user by his ID
 *  @param {string} id - ID of the user
 *  @return {Promise<Object>} - Return the deleted user
 */
function deleteUserById({ id });
```

```javascript
/**
 *  Delete an user by his login
 *  @param {string} login - Login of the user
 *  @return {Promise<Object>} - Return the deleted user
 */
function deleteUserByLogin({ login });
```

```javascript
/**
 *  Update the users properties of an user
 * @param {string} id - ID of the user
 * @param {object} properties - Properties that will change
 * @return {Promise<Object>} - Return the updated user
 */
function updateUserById({ id, properties });
```

```javascript
/**
 *  Update the users properties of an user
 * @param {string} login - Login of the user
 * @param {object} properties - Properties that will change
 * @return {Promise<Object>} - Return the updated user
 */
function updateUserByLogin({ login, properties });
```

```javascript
/**
 *  Create an users group
 *  @param {string} name - Name of the users group
 *  @return {Promise<Object>} - Return the users group
 */
function createUsersGroup({ name });
```

```javascript
/**
 *  Get an users group from his id
 *  @param {string} id - ID of the users group
 *  @return {Promise<Object>} - Return the users group
 */
function getUsersGroupById({ id });
```

```javascript
/**
 *  Get an users group from his name
 *  @param {string} name - Name of the users group
 *  @return {Promise<Object>} - Return the users group
 */
function getUsersGroupByName({ name });
```

```javascript
/**
 *  Delete an users group from his ID.
 *  @param {string} id - ID of the users group
 *  @return {Promise<Object>} - Return the deleted users group
 */
function deleteUsersGroupById({ id });
```

```javascript
/**
 *  Delete an users group from his name.
 *  @param {string} name - Name of the users group
 *  @return {Promise<Object>} - Return the deleted users group
 */
function deleteUsersGroupByName({ name });
```

```javascript
/**
 *  Update an users group name from his ID.
 *  @param {string} id - ID of the users group
 *  @param {string} newName - New name of the group
 *  @return {Promise<Object>} - Return the updated group
 */
function updateUsersGroupById({ id, newName });
```

```javascript
/**
 *  Update an users group name from his name.
 *  @param {string} name - Name of the users group
 *  @param {string} newName - New name of the group
 *  @return {Promise<Object>} - Return the updated group
 */
function updateUsersGroupByName({ name, newName });
```

```javascript
/**
 *  Add users to an users group
 *  @param {Array} users - Array of users ID
 *  @param {string} idGroup - ID of the users group
 *  @return {Promise<Object>} - Return the users group 
 */
function addUsersToGroup({ users, idGroup });
```

```javascript
/**
 *  Remove users from an users group
 *  @param {Array} users - Array of users ID
 *  @param {string} idGroup - ID of the users group
 *  @return {Promise<Object>} - Return the users group 
 */
function removeUsersFromGroup({ users, idGroup });
```

```javascript
/**
 *  Get the users of a specific group
 *  @param {string} id - ID of the group
 *  @return {Promise<Array>} - Return all users for this group
 */
function getUsersByGroup({ id });
```

```javascript
/**
 *  Get all groups where is this specific user
 *  @param {string} id - ID of the user
 *  @param {Promise<Array>} - Return all groups for this user
 */
function getGroupsForUser({ id });
```

```javascript
/**
 *  Get the presence state of an user
 *  @param {string} id - ID of the user
 *  @return {Promise<boolean>} - Return boolean for the presence state
 */
function getPresenceByUser({ id });
```

```javascript
/**
 *  Event launch when a presence state has changed for this user
 *  @param {string} id - ID of the user
 *  @return {boolean} - Return the presence state
 */
function onNewPresence({ id });
```