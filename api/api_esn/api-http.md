# Cloud Functions pour le service _HTTPService_

## Cloud Functions

```javascript
/**
 *  Send an HTTP Request
 *  @param {string} url - URL of the request
 *  @param {string} method - Method of the HTTP Request (GET, POST, ...)
 *  @param {string} parseMode - Optional, by default "json"
 *  @param {Array} headers - List of headers (JSON format)
 *  @param {Object} content - Content of the HTTP request
 *  @return {Promise<boolean>} - Return the success of the request
 */
function sendHTTPRequest({ url, method, parseMode, headers, content });
```