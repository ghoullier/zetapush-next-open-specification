# Cloud Functions pour _ChatService_

---

# **TODO : Revoir façon de faire et mettre en cas d'utilisations** 

---



## Objets

### Room

Une `Room` comporte son id, son nom et la liste des IDs des utilisateurs qui appartiennent à cette dernière.

```json
{
    "id": "id_of_the_room",
    "name": "name_of_the_room",
    "users": [
        "id_user_1",
        "id_user_2",
        "id_user_3"
    ]
}
```

### Message

Un `Message` comporte un id, un contenu, un envoyeur, un destinataire. Le contenu est un objet donc on peut saisir un objet JSON.

```json
{
    "id": "id_of_the_message",
    "content": "Content of the message",
    "sender": "id_of_the_sender",
    "recipient": "id_of_the_recipient"
}
```

## Précisions

## Cloud functions

```javascript
/**
 *  Create a room to communicate between many users
 *  @param {string} name - Name of the room
 *  @param {Array} users - List of users inside the room
 *  @return  {Promise<Room>} - Created room
 */
function createRoom({ name, users });
```

```javascript
/**
 *  Delete a room by id
 *  @param {string} id - ID of the room
 *  @return  {Promise<Room>} - Deleted room
 */
function deleteRoomById({ id });
```

```javascript
/**
 *  Delete a room by name
 *  @param {string} name - Name of the room
 *  @return  {Promise<Room>} - Deleted room
 */
function deleteRoomByName({ name });
```

```javascript
/**
 *  Update room name by id
 *  @param {string} id - ID of the room
 *  @param {string} newName - New name of the room
 *  @return  {Promise<Room>} - Updated room
 */
function updateRoomById({ id });
```

```javascript
/**
 *  Update room name by name
 *  @param {string} name - Name of the room
 *  @param {string} newName - New name of the room
 *  @return  {Promise<Room>} - Updated room
 */
function updateRoomByName({ name, newName });
```

```javascript
/**
 *  Get a room by id
 *  @param {string} id - ID of the room
 *  @return  {Promise<Room>} - Room
 */
function getRoomById({ id });
```

```javascript
/**
 *  Get a room by name
 *  @param {string} name - Name of the room
 *  @return  {Promise<Room>} - Room
 */
function getRoomByName({ name });
```

```javascript
/**
 *  Add new users to an existing room
 *  @param {string} id - ID of the room
 *  @param {Array} users - List of users to add in the room
 *  @param {Promise<Room>} - Room with the new users
 */
function addUsersToRoom({ id, users });
```

```javascript
/**
 *  Remove users to an existing room
 *  @param {string} id - ID of the room
 *  @param {Array} users - List of users we want to remove from room
 *  @param {Promise<Room>} - Updated room
 */
function removeUsersToRoom({ id, users });
```

```javascript
/**
 *  Get all users of the room
 *  @param {string} id - ID of the room
 *  @return {Promise<Array>} - List of users id
 */
function getUsersByRoom({ id });
```

```javascript
/**
 *  Get all rooms of the user (where he is)
 *  @param {string} id - ID of the user
 *  @return {Promise<Array>} - List of all groups id
 */
function getRoomsByUser({ id });
```

```javascript
/**
 *  Send a message to all users of the room
 *  @param {string} id - ID of the room
 *  @param {string} message - Message we are sending
 *  @param {boolean} send_to_me - Define if we send the message to the sender
 *  @param {Promise<Array>} - List of all users we are sent the message
 */
function sendMessageToRoom({ id, message, send_to_me });
```

```javascript
/**
 *  Send a message to specified users of the room
 *  @param {string} id - ID of the room
 *  @param {string} message - Message we are sending
 *  @param {Array} users - List of all users id we will send the message
 *  @param {Promise<Array>} - List of all users we are sent the message
 */
function sendMessageToUsers({ id, message, users });
```

```javascript
/**
 *  Get messages of the room by user (all by default)
 *  @param {string} id - ID of the room
 *  @param {Array} users - Optional list of users we get messages, if null get all
 *  @return {Promise<Array>} - List of all messages
 */
function getMessages({ id, users });
```

```javascript
/**
 *  Delete messages of the room by user (all by default)
 *  @param {string} id - ID of the room
 *  @param {Array} users - Optional list of users we delete messages, if null delete all
 *  @return {Promise<Array>} - List of all deleted messages
 */
function deleteMessages({ id, users });
```

```javascript
/**
 *  Listen the incoming messages for a specific room
 *  @param {string} id - ID of the room
 *  @param {Array} users - List of all senders we want to get incoming message, if null, get all incoming messages
 *  @param {Function} callback - Callback used to get message. Should have one parameter.
 */
function onNewMessage({ id, users, callback });
```