# Description d'utilisation du _ChatService_

## Introduction

- Pour utiliser un service il faut créer une instance de ce dernier sous la forme : `const chatService = new ChatService()`.
- Plusieurs instances de _ChatService_ sont utilisables dans une seule application. Dans ce cas, les données sont strictement séparées (comportement par défaut).
- L'utilisation du chat se base sur le principe de `room`. Une `room` correspond à un espace d'échange entre les utilisateurs qui y sont affectés

Nous allons voir chaque cas d'usage pour décrire l'utilisation de _ChatService_.

## Cas d'utilisation

---

### Gestion d'une room

#### Création d'une room

Dans ce cas, nous voulons créer une room. Une room a un paramètre **name** et peut prendre des paramètres additionnels au choix en utilisant le paramètre **properties**.

```javascript
// Create an instance of ChatService
const chatService = new ChatService();

// Create a room with additional properties
const createdRoom  = await chatService.createRoom({ name: "my-room", properties: { createdAt: Date.now()}});
```

Voici le retour de la création d'une room :

```json
{
    "id": "generated-id-of-my-room",
    "name": "my-room",
    "users": [
        "id-of-the-user-that-create-room"
    ],
    "createdAt": 1523534053567 
}
```

L'objet de `room` contient un ID auto-généré ainsi que la liste des utilisateurs qui sont affectés à ce groupe (via le paramètre `users`). Un utilisateur peut appartenir à plusieurs rooms.

Il est aussi possible de forcer l'ID avec :

```javascript
// Create a room
const createdRoom  = await chatService.createRoom({ id: "my-room-id", name: "my-room" });
```

#### Suppression d'une room

Dans ce cas, nous voulons supprimer une room. Nous pouvons supprimer une room à partir de son ID ou de son nom.

```javascript
// Create an instance of ChatService
const chatService = new ChatService();

// Delete a room
const deletedRoom = await chatService.deleteRoom({ name: "my-room"});
// OR
const deletedRoom = await chatService.deleteRoom({ id: "my-room-id"});
```

#### Récupération d'une room

Dans ce cas, nous voulons récupérer une room. Nous pouvons récupérer une room à partir de son ID ou de son nom.

```javascript
// Create an instance of ChatService
const chatService = new ChatService();

// Get a room
const room = await chatService.getRoom({ name: "my-room"});
// OR
const room = await chatService.getRoom({ id: "my-room-id"});
```

#### Mise à jour d'une room

Dans ce cas, nous voulons mettre à jour les propriétés de la room. Pour ceci nous pouvons l'identifier à partir de son ID ou de son nom.

```javascript
// Create an instance of ChatService
const chatService = new ChatService();

// Get a room
const updatedRoom = await chatService.updateRoom({ name: "my-room", properties: { createdAt: Date.now(), name: "new-name"}});
// OR
const updatedRoom = await chatService.updateRoom({ id: "my-room-id", properties: { createdAt: Date.now(), name: "new-name"}});
```

---

### Intéraction des utilisateurs avec une room

#### Affectation d'un utilisateur à une room

Dans ce cas, nous voulons ajouter un utilisateur à une room. Pour ceci, nous pouvons identifier la room, soit par son ID, soit par son nom.

```javascript
// Create our services
const chatService = new ChatService();
const userService = new UserService();

// Create a room
const createdRoom  = await chatService.createRoom({ id: "my-room-id", name: "my-room" });

// Create one user
const newUser = await userService.createUser({ login: "antoine", password: "password" });

// Add user in the room
const addedUser = await chatService.addUser({ id: "my-room-id", user: newUser.id});
// OR
const addedUser = await chatService.addUser({ name: "my-room", user: newUser.id});
```

Il est aussi possible d'ajouter plusieurs utilisateurs en même temps en utilisant cette syntaxe :

```javascript
const addedUser = await chatService.addUsers({ id: "my-room-id", users: ["id-user1", "id-user2"]});
```

#### Auto affection à une room

Dans ce cas, nous voulons ajouter l'utilisateur courant à une room. Pour ceci, nous pouvons identifier la room, soit par son ID, soit par son nom.

```javascript
// Create our services
const chatService = new ChatService();
const userService = new UserService();

// Create a room
const createdRoom  = await chatService.createRoom({ id: "my-room-id", name: "my-room" });

// Add user in the room
const addedUser = await chatService.addMe({ id: "my-room-id"});
// OR
const addedUser = await chatService.addMe({ name: "my-room"});
```

#### Suppresion d'un utilisateur à une room

Dans ce cas, nous voulons enlever un utilisateur d'une room. Pour ceci, nous pouvons identifier la room, soit par son ID, soit par son nom.

```javascript
// Create our services
const chatService = new ChatService();
const userService = new UserService();

// Create a room
const createdRoom  = await chatService.createRoom({ id: "my-room-id", name: "my-room" });

// Create one user
const newUser = await userService.createUser({ login: "antoine", password: "password" });

// Add user in the room
const addedUser = await chatService.addUser({ id: "my-room-id", user: newUser.id});

// Remove user from the room
const removedUser = await chatService.removeUser({ id: "my-room-id", user: newUser.id });
// OR
const removedUser = await chatService.removeUser({ name: "my-room", user: newUser.id });
```

#### Récupération de la liste des utilisateurs par room

Dans ce cas, nous voulons récupérer la liste des utilisateurs pour une room. Nous pouvons identifier cette dernière par son ID ou son nom.

```javascript
// Create our services
const chatService = new ChatService();

// Create a room
const createdRoom  = await chatService.createRoom({ id: "my-room-id", name: "my-room" });

const users = await chatService.getUsersByRoom({ id: "my-room-id"});
// OR
const users = await chatService.getUsersByRoom({ name: "my-room"});
```

#### Récupération de la liste des rooms auquel un utilisateur appartient

Dans ce cas, nous voulons récupérer la liste des rooms auquel appartient un utilisateur.

```javascript
// Create our services
const chatService = new ChatService();
const userService = new UserService();

// Create a room
const createdRoom  = await chatService.createRoom({ id: "my-room-id", name: "my-room" });

// Create one user
const newUser = await userService.createUser({ login: "antoine", password: "password" });

// Add user in the room
const addedUser = await chatService.addUser({ id: "my-room-id", user: newUser.id});

// Get rooms of the users
const rooms = await chatService.getRoomsByUser({ id: newUser.id }); 
```

#### Récupération de la présence de chaque utilisateurs dans la room

Dans ce cas, nous voulons récupérer la liste des utilisateurs avec leur présence associée par room. Nous pouvons identifier la room soit par son ID, soit par son nom.

```javascript
// Create our services
const chatService = new ChatService();

// Create a room
const createdRoom  = await chatService.createRoom({ id: "my-room-id", name: "my-room" });

// Create two user
const newUser1 = await userService.createUser({ id: "user-1-id", login: "antoine", password: "password" });
const newUser2 = await userService.createUser({ id: "user-2-id", login: "martin", password: "password" });

// Add users in the room
const addedUser1 = await chatService.addUser({ id: "my-room-id", user: newUser1.id});
const addedUser2 = await chatService.addUser({ id: "my-room-id", user: newUser2.id});

// Get presences for the room
const presences = await chatService.getPresences({ id: "my-room-id" });
// OR
const presences = await chatService.getPresences({ name: "my-room" });
```

Le format de sortie des présences est le suivant :

```json
[
    {
        "user_id": "user-1-id",
        "presence": true 
    }, 
    {
        "user_id": "user-2-id",
        "presence": false
    }
]
```

_L'écoute d'un évènement de présence se fait via UserService._

---


### Envoi de messages


#### Envoi d'un message à toute la room

Dans ce cas, nous voulons envoyer un message à tous les utilisateurs de la room. On peut aussi spécifier si on souhaite que le message nous soit aussi envoyé (en tant qu'expéditeur) en utilisant le paramètre `send_to_sender`.

```javascript
// Create our services
const chatService = new ChatService();

// Create a room
const createdRoom  = await chatService.createRoom({ id: "my-room-id", name: "my-room" });

// Send message to all users
const sentMessage = await chatService.sendMessageToAllUsers({ room: createdRoom.id, message: "My message content", send_to_sender: true });
```
Dans ce cas `sentMessage` est un tableau de messages envoyés.

Le paramètre `message` peut aussi être un objet.


Voici le format de chaque message :

```json
{
    "id": "id_of_my_message",
    "message": "My message content",
    "sender": "id-of-sender-user",
    "recipient": "id-of-recipient-user",
    "timestamp": 1523527476595
}
```

#### Envoi de message en personnalisant le sender

Dans ce cas, nous voulons définir au moment de l'envoi du message, le nom à afficher pour l'envoyeur :

```javascript
// Create our service
const chatService = new ChatService();

// Create a room
const createdRoom  = await chatService.createRoom({ id: "my-room-id", name: "my-room" });

// Send message to all users
const sentMessage = await chatService.sendMessageToAllUsers({ room: createdRoom.id, message: "My message content", sender: "Damien" });
```


#### Envoi de message avec des metadata

Dans ce cas, nous voulons ajouter des metadata à notre message. Chaque méthode d'envoi est utilisable, c'est juste l'objet d'envoi qui est modifié :

```javascript
// Create our services
const chatService = new ChatService();

// Create a room
const createdRoom  = await chatService.createRoom({ id: "my-room-id", name: "my-room" });

// Send message to all users
const sentMessage = await chatService.sendMessageToAllUsers({ room: createdRoom.id, message: "My message content", send_to_sender: true, metadata: { time: Date.now()} });
```

#### Écouter les messages entrants

Dans ce cas, nous voulons écouter les messages entrants. Un utilisateur peut seulement écouter les messages qui lui sont destinés. Nous pouvons identifier la room soit par son ID, soit par son nom.

```javascript
// Create our services
const chatService = new ChatService();

// Create a room
const createdRoom  = await chatService.createRoom({ id: "my-room-id", name: "my-room" });

// Add user in the room
const addedUser = await chatService.addMe({ id: "my-room-id"});

// Listen the incoming messages
chatService.listenIncomingMessages({ room: createdRoom.id, callback: function(message) => {
    console.log(`I have a new message from ${message.sender}`);
}});
// OR
chatService.listenIncomingMessages({ room: createdRoom.name, callback: function(message) => {
    console.log(`I have a new message from ${message.sender}`);
}});
```

---

### Gestion des messages

#### Récupération de la liste des messages de la room ou par utilisateur

Dans ce cas, nous voulons pouvoir récupérer l'ensemble des messages de la room.
Il est aussi possible de sélectionner les messages en utilisant le paramètre `request`:

```javascript
// Create our services
const chatService = new ChatService();

// Create a room
const createdRoom  = await chatService.createRoom({ id: "my-room-id", name: "my-room" });

// Get all messages of specific sender and from a specific date
const messages = await chatService.getMessages({ id: "my-room-id", request: function(message) => {
    return message.sender == "id-wanted-sender" && message.time > (Date.now() - 10000);
}});
```

#### Suppression des messages de la room ou par utilisateur

Dans ce cas, nous voulons pouvoir supprimer l'ensemble des messages de la room.
Il est aussi possible de sélectionner les messages en utilisant le paramètre `request`:

```javascript
// Create our services
const chatService = new ChatService();

// Create a room
const createdRoom  = await chatService.createRoom({ id: "my-room-id", name: "my-room" });

// Delete all messages of specific sender and from a specific date
const deletedMessages = await chatService.deleteMessages({ id: "my-room-id", request: function(message) => {
    return message.sender == "id-wanted-sender" && message.time > (Date.now() - 10000);
}});
```

--- 

### Utilisation de plusieurs _ChatServices_

#### Utiliser deux services distincts

Dans ce cas, nous voulons avoir deux services de chat qui sont différents et complètement distincts. Pour ceci, il suffit de créer deux instances de `ChatService`, par défaut les données sont strictements séparées.

```javascript
// Create a first instance of ChatService
const chatService1 = new ChatService();

// Create a second instance of UserService
const chatService2 = new ChatService();
```

#### Utiliser deux services distincts mais avec les données partagées

Il est possible d'avoir plusieurs services distincts qui partagent les mêmes données. Pour ça il faut identifier chaque service par le même ID.

```javascript
// Create two instances of ChatService that have different data
const chatService1 = new ChatService({ id: "my-service-1"});
const chatService2 = new ChatService({ id: "my-service-2"});

// Create two instances of UserService that have same data
const chatService3 = new ChatService({ id: "my-service-global"});
const chatService4 = new ChatService({ id: "my-service-global"});
```

### Room par défaut

#### Envoi d'un message sans création de room

Il est possible d'utiliser le `ChatService` sans avoir créé de room au préalable. Dans ce cas, tous les utilisateurs et messages appartiennent à une room par défaut.

```javascript
// Create one instance of ChatService
const chatService1 = new ChatService();

// Send message to all users on default room
const sentMessage = await chatService.sendMessageToAllUsers({ message: "My message content"});
```