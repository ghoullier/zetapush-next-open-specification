# Description d'utilisation du _StorageService_

## Introduction

- Pour utiliser un service il faut créer une instance de ce dernier sous la forme : `const storageService = new StorageService()`.
- Plusieurs instances de _StorageService_ sont utilisables dans une seule application. Dans ce cas, les données sont strictement séparées (comportement par défaut).

Nous allons voir chaque cas d'usage pour décrire l'utilisation de _StorageService_.

## Cas d'utilisation

---

### Stockage

#### Stockage de données dans un espace global

Dans ce cas toutes les données sont au même endroit.

```javascript
// Create an instance of StorageService
const storageService = new StorageService();
// I want to store the user informations in the global storage
storageService.store({key: "id_of_my_data", value: { name: "Damien", age: 23 }});
```

#### Utilisation de 2 instances de _StorageService_

Dans ce cas, nous avons deux instances de _StorageService_, ce qui implique que les données sont strictement séparées.
Nous pouvons illustrer ce cas lorsque nous voulons deux bases de données séparées.

```javascript
// Create 2 instances of StorageService
const storageService1 = new StorageService();
const storageService2 = new StorageService();

// I want to store the user informations in two separate storages
storageService1.store({key: "id_first_data", value: { name: "Damien", age: 23 }});
storageService2.store({key: "id_second_data", value: { name: "Antoine", age: 26 }});
```

#### Utilisation de 2 instances de _StorageService_ qui utilisent le même espace de données

Dans ce cas, nous avons deux instances de _StorageService_ mais les données sont partagées au sein d'un seul et même espace.
Pour ça nous utilisons la notion d'**ID** d'une instance de _StorageService_.
Si deux instances partagent le même ID, les données sont les mêmes pour les deux.

```javascript
// Create 2 instances of StorageService
const storageService1 = new StorageService({id: "my-storage-service"});
const storageService2 = new StorageService({id: "my-storage-service"});

// I want to store the user informations in the same storage
storageService1.store({key: "id_first_data", value: { name: "Damien", age: 23 }});
storageService2.store({key: "id_second_data", value: { name: "Antoine", age: 26 }});
```

#### Stockage de données dans 2 espaces de stockage différents

Dans ce cas, nous souhaitons séparer nos données au sein d'un seul _StorageService_.
Pour ça nous utilisons le concept de **Collection**.
Nous pouvons illustrer ça par des données qui sont séparées dans plusieurs _tables_.

```javascript
// Create an instance of StorageService
const storageService = new StorageService({ collection: "type" });

// I want to store the user informations in one collection
storageService.store({key: "id_of_my_data", value: { name: "Damien", age: 23 }, type: "users"});

// I want to store the animal informations in other one collection
storageService.store({key: "id_of_my_new_data", value: { name: "Doly", age: 11 }, type: "animal"});
```

Dans le cas où le développeur ne saisit pas de paramètre `type`, les données sont stockées dans une **collection** par défaut.

#### Stockage de données en donnant des contraintes de stockage

Dans ce cas, nous voulons que les données que nous stockons soient dans un format particulier.
Pour ceci, nous ajoutons la possibilité d'ajouter des contraintes sur le format de stockage des données.
Une liste des contraintes applicables sera disponible (ex: _size, notnull, id, notempty, ..._)

```javascript
// Create an instance of StorageService
const storageService = new StorageService({ constraints: [{ data: "name", value: "size > 4 && size < 20"}]});

// I want to store the user informations
storageService.store({key: "id_of_my_data", value: { name: "Damien", age: 23 });
```

#### Stockage de données en donnant des contraintes de stockage pour une collection particulière

Comme pour le précédent cas d'utilisation, nous voulons ajouter des contraintes d'utlisation mais dans notre cas seulement pour une table précise.

```javascript
// Create an instance of StorageService
const storageService = new StorageService({ constraints: [{ collection: "users", data: "name", value: "size > 4 && size < 20"}]});

// I want to store the user informations in one collection
storageService.store({key: "id_of_my_data", value: { name: "Damien", age: 23 }, type: "users"});
```

### Stockage de données avec des contraintes de stockage par annotation

Dans ce cas, nous voulons aussi donner des contraintes de stockage, mais avec une syntaxe plus élégante.

```javascript
@Storable
class AvengerUser {
    @Id
    id,
    @NotNull
    @Size(min=4, max=50)
    name,
    realIdentity: { firstname, lastname },
    @NotEmpty
    superpowers
}

const storageService = new StorageService();
const newAvengers = new AvengerUser({name: "Spider-Man", realIdentity: {firstname: "Peter", lastname: "Parker"}, superpowers: ["Spider attack"]});
// If the object is not in the correct format, the storage failed
storageService.store({ key: "id_user__timestamp", value: newAvengers);
```

#### Stockage de données en rendant certaines données cherchables par un moteur de recherche

Dans ce cas, nous voulons stocker un objet, qui a des propriétés qui seront recherchables par la suite en utilisant une _Cloud Function_.

```javascript
// Create an instance of StorageService
// We give the list of parameters we want to be able to search
const storageService = new StorageService({ searchable: { collection: "users", values: ["name"]}});

// I want to store the user informations in one collection
storageService.store({key: "id_of_my_data", value: { name: "Damien", age: 23 }, type: "users"});
```

#### Stockage de données en rendant certaines données cherchables par annotation

Comme précédement, nous voulons rendre certaines données cherchables, mais cette fois-ci nous allons le faire avec une syntaxe plus élégante.

```javascript
@Searchable(fields=["name", "realIdentity.firstname", "realIdentity.lastname"])
class AvengerUser {
    id,
    name,
    realIdentity: { firstname, lastname },
    superpowers
}

const storageService = new StorageService();
const newAvengers = new AvengerUser({name: "Spider-Man", realIdentity: {firstname: "Peter", lastname: "Parker"}, superpowers: ["Spider attack"]});
storageService.store({ key: "id_user__timestamp", value: newAvengers);
```

---

### Récupération des données

#### Récupération d'une donnée dans un espace global

```javascript
// Create an instance of StorageService
const storageService = new StorageService("my-existing-storage-service");

// Get the data
const data = await storageService.get({ key: "id_of_my_data" });
```

#### Récupération d'une donnée dans une collection particulière

```javascript
// Create an instance of StorageService
const storageService = new StorageService("my-existing-storage-service");

// Get the data
const data = await storageService.get({ key: "id_of_my_data", collection: "users" });
```

#### Récupération de données en utilisant une requête pour la sélection

Dans ce cas, nous voulons récupérer un ensemble de données qui correspondent à une requête particulière.

```javascript
// Create an instance of StorageService
const storageService = new StorageService();
// I want to store many user informations in the global storage
storageService.store({key: "id_of_my_data1", value: { name: "Damien", age: 23 }});
storageService.store({key: "id_of_my_data2", value: { name: "Antoine", age: 11 }});
storageService.store({key: "id_of_my_data3", value: { name: "Martin", age: 34 }});

// I want to get all users which are 18 years old or more
const arrayOfUsers = await storageService.request({ function: (data) => {
    return data.age >= 18;
}});
```

Dans ce cas, nous avons seulement les utilisateurs _Damien_ et _Martin_ qui sont renvoyés par la requête.

Il est aussi possible de restreindre cette sélection à une _collection_ avec cette syntaxe :

```javascript
const storageService = new StorageService({ collection: "type" });

const arrayOfUsers = await storageService.request({ type: "users", function: (data) => {
    return data.age >= 18;
}});
```

#### Recherche de données

Dans ce cas, nous voulons trouver les données qui correspondent à notre valeur d'entrée. Cela correspond à un cas d'usage d'autocomplétion par exemple.

```javascript
// Create an instance of StorageService
// We give the list of parameters we want to be able to search
const storageService = new StorageService({ searchable: { values: ["name"]}});

// I want to store the user informations in one collection
storageService.store({key: "id_of_my_data1", value: { name: "Damien", age: 23 }});
storageService.store({key: "id_of_my_data2", value: { name: "Antoine", age: 11 }});
storageService.store({key: "id_of_my_data3", value: { name: "Martin", age: 34 }});

// I want to search all matched data
const result = await storageService.search({ input: "da" });
```

Dans ce cas, nous aurons seulement l'utilisateur _Damien_ qui sera renvoyé.

Il est aussi possible dans ce cas de sélectionner les données en amont par collection :

```javascript
// Create an instance of StorageService
// We give the list of parameters we want to be able to search
const storageService = new StorageService({ searchable: { collection: "users", values: ["name"]}});


// I want to search all matched data
const result = await storageService.search({ input: "da" , type: "users"});
```

---

### Suppression de données

#### Suppression d'une donnée dans un espace global

```javascript
// Create an instance of StorageService
const storageService = new StorageService("my-existing-storage-service");

// Get the data
const deletedData = await storageService.delete({ key: "id_of_my_data" });
```

#### Suppression d'une donnée dans une collection particulière

```javascript
// Create an instance of StorageService
const storageService = new StorageService("my-existing-storage-service");

// Get the data
const deletedData = await storageService.delete({ key: "id_of_my_data", collection: "users" });
```

#### Suppression de données en utilisant une requête pour la sélection

Dans ce cas, nous voulons supprimer un ensemble de données qui correspondent à une requête particulière.

```javascript
// Create an instance of StorageService
const storageService = new StorageService();
// I want to store many user informations in the global storage
storageService.store({key: "id_of_my_data1", value: { name: "Damien", age: 23 }});
storageService.store({key: "id_of_my_data2", value: { name: "Antoine", age: 11 }});
storageService.store({key: "id_of_my_data3", value: { name: "Martin", age: 34 }});

// I want to delete all users which are 18 years old or more
const deletedUsers = await storageService.deleteByRequest({ function: (data) => {
    return data.age >= 18;
}});
```

Dans ce cas, nous avons seulement les utilisateurs _Damien_ et _Martin_ qui sont supprimés par la requête.

Il est aussi possible de restreindre cette sélection à une _collection_ avec cette syntaxe :

```javascript
const storageService = new StorageService({ collection: "type" });

const deletedUsers = await storageService.deleteByRequest({ type: "users", function: (data) => {
    return data.age >= 18;
}});
```


