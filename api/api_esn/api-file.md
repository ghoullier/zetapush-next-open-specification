# Cloud Functions pour _FileService_

```javascript
/**
 *  Upload a file on a HDFS storage
 *  @param {string} file - File we want to upload
 *  @param {string} path - Path of the storage
 *  @param {string} owner - Optional owner to separate files
 *  @return {Promise} - Success of the upload in promise
 */
function uploadFile({ file, path, owner });
```

```javascript
/**
 *  @param {string} path - Path of the storage
 *  @param {string} owner - Optional owner to separate files
 *  @return {Promise} - Array of files returned in a promise
 */
function getFiles({ path, owner });
```

```javascript
/**
 *  @param {string} path - Path of the storage
 *  @param {string} owner - Optional owner to separate files
 *  @return {Promise} - Deleted file returned in a promise
 */
function deleteFile({ path, owner });
```


