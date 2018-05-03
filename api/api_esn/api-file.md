# Cloud Functions pour _FileService_

---

# **TODO : Revoir façon de faire et mettre en cas d'utilisations** 

---

## Cloud functions

```javascript
/**
 *  Upload a file on a HDFS storage
 *  @param {string} file - File we want to upload
 *  @param {string} path - Path of the storage
 *  @param {string} owner - Optional owner to separate files
 *  @return {Promise<boolean>} - Success of the upload
 */
function uploadFile({ file, path, owner });
```

```javascript
/**
 *  @param {string} path - Path of the storage
 *  @param {string} owner - Optional owner to separate files
 *  @return {Promise<Array>} - Array of files returned
 */
function getFiles({ path, owner });
```

```javascript
/**
 *  @param {string} path - Path of the storage
 *  @param {string} owner - Optional owner to separate files
 *  @return {Promise<Object>} - Deleted file returned
 */
function deleteFile({ path, owner });
```


