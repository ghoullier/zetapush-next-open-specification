# Cloud Functions pour le service _UserService_

## Précisions


## Cloud Functions

```javascript
/**
 *  Create an user with a specific login, password and additional properties
 *  @param {string} login - Login of the created user
 *  @param {string} password - Password of the created user
 *  @param {object} properties - Additional properties with JSON format.
 *  @return {Promise} - Return the created user in a promise (each user has a ID)
 */
function createUser({ login, password, properties });
```

```javascript
/**
 *  Get an user from his ID
 *  @param {string} id - ID of the user
 *  @return {Promise} - Return the user in a promise
 */
function getUserById({ id });
```

```javascript
/**
 *  Get an user from his login
 *  @param {string} login - Login of the user
 *  @return {Promise} - Return the user in a promise
 */
function getUserByLogin({ login });
```

```javascript
/**
 *  Delete an user by his ID
 *  @param {string} id - ID of the user
 *  @return {Promise} - Return the deleted user in a promise
 */
function deleteUserById({ id });
```

```javascript
/**
 *  Delete an user by his login
 *  @param {string} login - Login of the user
 *  @return {Promise} - Return the deleted user in a promise
 */
function deleteUserByLogin({ login });
```

```javascript
/**
 *  Update the users properties of an user. It changes only given properties on "properties" param (based on his ID)
 * @param {string} id - ID of the user
 * @param {object} properties - Properties that will change. We can change login, password or additional properties
 * @return {Promise} - Return the updated user in a promise
 */
function updateUserById({ id, properties });
```

```javascript
/**
 *  Update the users properties of an user. It changes only given properties on "properties" param (based on his login)
 * @param {string} login - Login of the user
 * @param {object} properties - Properties that will change. We can change login, password or additional properties
 * @return {Promise} - Return the updated user in a promise
 */
function updateUserByLogin({ login, properties });
```

```javascript
/**
 *  Create an users group. For exemple to regroup users by type.
 *  @param {string} name - Name of the users group
 *  @return {Promise} - Return the users group with a specific ID
 */
function createUsersGroup({ name });
```

```javascript
/**
 *  Get an users group from his id
 *  @param {string} id - ID of the users group
 *  @return {Promise} - Return the users group
 */
function getUsersGroupById({ id });
```

```javascript
/**
 *  Get an users group from his name
 *  @param {string} name - Name of the users group
 *  @return {Promise} - Return the users group
 */
function getUsersGroupByName({ name });
```

```javascript
/**
 *  Delete an users group from his ID.
 *  @param {string} id - ID of the users group
 *  @return {Promise} - Return the deleted users group
 */
function deleteUsersGroupById({ id });
```

```javascript
/**
 *  Delete an users group from his name.
 *  @param {string} name - Name of the users group
 *  @return {Promise} - Return the deleted users group
 */
function deleteUsersGroupByName({ name });
```

```javascript
/**
 *  Update an users group name from his ID.
 *  @param {string} id - ID of the users group
 *  @param {string} newName - New name of the group
 *  @return {Promise} - Return the updated group
 */
function updateUsersGroupById({ id, newName });
```

```javascript
/**
 *  Update an users group name from his name.
 *  @param {string} name - Name of the users group
 *  @param {string} newName - New name of the group
 *  @return {Promise} - Return the updated group
 */
function updateUsersGroupByName({ name, newName });
```

```javascript
/**
 *  Add users to an users group
 *  @param {Array} users - Array of users ID
 *  @param {string} idGroup - ID of the users group
 *  @return {Promise} - Return the users group 
 */
function addUsersToGroup({ users, idGroup });
```

```javascript
/**
 *  Remove users from an users group
 *  @param {Array} users - Array of users ID
 *  @param {string} idGroup - ID of the users group
 *  @return {Promise} - Return the users group 
 */
function removeUsersFromGroup({ users, idGroup });
```

```javascript
/**
 *  Get the users of a specific group
 *  @param {string} id - ID of the group
 *  @return {Promise} - Return all users in an array
 */
function getUsersByGroup({ id });
```

```javascript
/**
 *  Get all groups where is this specific user
 *  @param {string} id - ID of the user
 *  @param {Promise} - Return all groups in an array
 */
function getGroupsForUser({ id });
```

```javascript
/**
 *  Get the presence state of an user
 *  @param {string} id - ID of the user
 *  @return {Promise} - Return boolean for the presence state
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