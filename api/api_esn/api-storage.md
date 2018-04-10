# Cloud Functions pour _StorageService_

## Précisions

### Séparation des données

La séparation des données en fonction des utilisateurs et des groupes d'utilisateurs se fait à travers le paramètre `owner`. Si ce paramètre est `null`, les données sont toutes dans un espace global, sans distinction entre les utilisateurs. Lorsque le paramètre `owner` est défini, les données seront stockées dans un espace propre à l'utilisateur ou propre au groupe d'utilisateurs. Conventionnellement, ce paramètre est rempli par l'ID de l'utilisateur ou par l'ID du groupe d'utilisateurs. Pour accèder à ces données compartimentées, il faut appeler une _cloud function_ de récupération de données avec le bon `owner`.

Il est aussi possible de séparer les données par type. Pour ça on utilise le paramètre `type`. Chaque données est compartimentée en fonction de ce paramètre. On peut par exemple comparer le `type` avec une table en base de données.

### Fonction de sélection des données

Dans certaines _cloud functions_ il est possible d'utiliser une fonction pour sélectionner un ensemble de données et d'appliquer notre traitement uniquement sur elles. Cette fonction prend en paramètre la donnée qui est lue, à laquelle on cherche la correspondance. Par exemple :

```javascript
/**
 *  We can access to StorageService by "storageService" variable.
 *  We use "getDataByRequest()" cloud function to select data.
 *  Here we don't use "owner" parameter for more simplicity
 * We are 2 data : { "firstname": "Antoine", "lastname": "Martin" } / { "firstname": "Rémy", "lastname": "Gauvin" }
 *  We want to get all data where the firstname is "Antoine"
 */
this.storageService.getDataByRequest({
    function: function(data) {
        return data.firstname === "Antoine";
    }
})
```

### Recherche de données

Le fonctionnement des _Cloud Functions_ de recherche est similaire à l'autocompletion.
Nous avons la _cloud function_ : `function searchData({ request, dataName, input, owner, type });`

- **request** correspond à une fonction qui permet de faire une sélection de données en amont
- **dataName** correspond au paramètre sur lequel nous voulons rechercher. Dans le cas d'un objet, la fonction se charge de parcourir l'ensemble de l'objet pour trouver le bon paramètre.
- **input** correspond à l'entrée pour chercher la correspondance avec le _dataName_. C'est dans la plupart des cas une saisie utilisateur. 
- **owner** correspond à un paramètre optionnel pour compartimenter les données en fonction de son propriétaire.

#### Exemple

Nous voulons implémenter un service d'autocomplétion sur notre site web, pour la recherche d'utilisateur. Nous avons les utilisateurs suivants en base de données :

```json
{
    "login": "antoine",
    "password": "password",
    "firstname": "Antoine",
    "lastname": "Martin"
},
{
    "login": "remy",
    "password": "password",
    "firstname": "Rémy",
    "lastname": "Gauvin"
}
```

Voici notre implémentation :

```javascript
/**
 *  We can access to StorageService by "storageService" variable.
 */
function searchUser(input) {
    return this.storageService.searchData({
        // No selection of data, we take all of them
        request: () => true,
        // We want to check about firstname and lastname
        dataName: "firstname" | "lastname",
        // Input of the user
        input,
        // No separation of data by owner
        owner: null,
        // No separation of data by type
        type: null
    });
}
```

Nous faisons appel à `searchUser()` à chaque fois que l'utilisateur saisi un caractère dans sa barre de recherche. Dans le cas où la saisie est "ma", le système retourne :

```json
{
    "login": "remy",
    "password": "password",
    "firstname": "Rémy",
    "lastname": "Gauvin"
}
```

## Cloud Functions

```javascript
/**
 *  Store a data using a key
 *  @param {string} key - Key to store and get the value
 *  @param {object} value - Stored value
 *  @param {string} owner - Optional key to separate data by owner
 *  @param {string} type - Optional key to separate data by type
 *  @return {Promise<boolean>} - Success of the storage 
 */
function storeDataByKey({ key, value, owner, type });
```

```javascript
/**
 *  Get a data by key
 *  @param {string} key - Key used to store and get the data
 *  @param {string} owner - Optional key to separate data by owner
 *  @param {string} type - Optional key to separate data by type
 *  @return {Promise<Object>} - Stored value
 */
function getDataByKey({ key, owner, type });
```

```javascript
/**
 *  Delete a data by key
 *  @param {string} key - Key used to store and get the data
 *  @param {string} owner - Optional key to separate data by owner
 *  @param {string} type - Optional key to separate data by type
 *  @return {Promise<boolean>} - Success of the suppression
 */
function deleteDataByKey({ key, owner, type });
```

```javascript
/**
 *  Get data using a function to select them
 *  @param {function} request - Function to select data
 *  @param {string} owner - Optional key to separate data by owner
 *  @param {string} type - Optional key to separate data by type
 * @return {Promise<Array>} - Return the list of corresponding data
 */
function getDataByRequest({ request, owner, type });
```

```javascript
/**
 *  Delete data using a function to select them
 *  @param {function} request - Function to select data
 *  @param {string} owner - Optional key to separate data by owner
 *  @param {string} type - Optional key to separate data by type
 * @return {Promise<Array>} - Return the list of deleted data
 */
function deleteDataByRequest({ request, owner, type });
```

```javascript
/**
 *  Get number of data for a specific request
 *  @param {function} request - Function to select data
 *  @param {string} owner - Optional key to separate data by owner
 *  @param {string} type - Optional key to separate data by type
 * @return {Promise<number>} - Return the number of instance
 */
function getSizeDataByRequest({ request, ownern type });
```

```javascript
/**
 *  Search data from an input value (like autocompletion)
 *  @param {function} request - Function to select data
 *  @param {string} dataName - Name of the data we want to check the corresponding
 *  @param {string} input - Input to search correspondance
 *  @param {string} owner - Optional key to separate data by owner
 *  @param {string} type - Optional key to separate data by type
 *  @return {Promise<Array>} - Return the list of corresponding data
 */
function searchData({ request, dataName, input, owner, type });
```
