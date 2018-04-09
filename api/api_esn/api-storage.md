# Cloud Functions pour _StorageService_

```javascript
/**
 *  Store a data using a key
 *  @param {string} key - Key to store and get the value
 *  @param {object} value - Stored value
 *  @param {string} owner - Optional key to separate data, only users having the "owner" property can access to data
 *  @return {Promise} - Success (boolean) of the storage 
 */
function storeDataByKey({ key, value, owner });
```

```javascript
/**
 *  Get a data from it key
 *  @param {string} key - Key used to store the data
 *  @param {string} owner - Optional key to separate data, only users having the "owner" property can access to data
 *  @return {Promise} value - Stored value returned in a promise
 */
function getDataByKey({ key, owner });
```

```javascript
/**
 *  Delete a data from it key
 *  @param {string} key - Key used to store the data
 *  @param {string} owner - Optional key to separate data, only users having the "owner" property can access to data
 *  @return {Promise} - Success (boolean) of the suppression return in a promise
 */
function deleteDataByKey({ key, owner });
```

```javascript
/**
 *  Get data using a function to select them
 *  @param {function} request - Function that should return boolean to get corresponding data
  *  @param {string} owner - Optional key to separate data, only users having the "owner" property can access to data
  * @return {Promise} - Return the list of corresponding data in a promise
 */
function getDataByRequest({ request, owner });
```

```javascript
/**
 *  Delete data using a function to select them
 *  @param {function} request - Function that should return boolean to get corresponding data
  *  @param {string} owner - Optional key to separate data, only users having the "owner" property can access to data
  * @return {Promise} - Return the list of deleted data in a promise
 */
function deleteDataByRequest({ request, owner });
```

```javascript
/**
 *  Get data using a function to select them
 *  @param {function} request - Function that should return boolean to get corresponding data
  *  @param {string} owner - Optional key to separate data, only users having the "owner" property can access to data
  * @return {Promise} - Return the number of instance
 */
function getSizeDataByRequest({ request, owner });
```

```javascript
/**
 *  Search data from an input value (like autocompletion)
 *  @param {function} request - Request to select a list of data where to search
 *  @param {string} dataName - Name of the data we want to check the corresponding (like name, email...)
 *  @param {string} input - Input to search correspondance, like the user input for autocompletion
 *  @param {string} owner - Optional key to separate data, only users having the "owner" property can access to data
 *  @return {Promise} - Return the list of corresponding data
 */
function searchData({ request, dataName, input, owner});
```
