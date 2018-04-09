# Cloud Functions pour le service _CommunicationService_

```javascript
/**
 *  Configure the email tool sender
 *  @param {string} smtp_user - SMTP User
 *  @param {string} smtp_pass - SMTP Password
 *  @param {string} smtp_host - SMTP Host
 *  @param {number} smtp_port - SMTP Port (default 25)
 *  @param {boolean} ssl - Enable SSL
 *  @param {boolean} starttls - Enable STARTTLS
 *  @return {Promise} - Return the success of the request
 */
function configureEmail({ smtp_user, smtp_pass, smtp_host, smtp_port, ssl, starttls})
```

```javascript
/**
 *  Send an email using the configured tool (ZetaPush provides one by default)
 *  @param {Array} to : List of email addresses for the recipients
 *  @param {string} sender : Email address of the sender
 *  @param {string} html : HTML code of the content of the email
 *  @param {string} subject : Subject of the email
 *  @param {Array} cc : List of email addresses of the copy recipients
 *  @param {Array} bcc : List of email addresses of the blind copy recipients 
 *  @return {Promise} - Return the success of the request
 */
function sendEmail({ to, sender, html, subject, cc, bcc });
```

```javascript
/**
 *  Configure the SMS tool sender, using OVH only (at this moment)
 *  @param {string} app_key - Application key of the service
 *  @param {string} app_secret - Application secret of the service
 *  @param {string} consumer_key - Consumer key of the service
 *  @param {string} service_name - Service name
 *  @return {Promise} - Return the success of the request
 */
function configureSMS({ app_key, app_secret, consumer_key, service_name});
```

```javascript
/**
 *  Send an SMS using the configured tool (ZetaPush provides one by default)
 *  @param {string} sender - Name of the sender
 *  @param {string} message - SMS content
 *  @param {Array} to - Array of recicipents (phone number)
 *  @return {Promise} - Return the success of the request 
 */
function sendSMS({ sender, message, to });
```

```javascript
/**
 *  Send an HTTP Request
 *  @param {string} url - URL of the request
 *  @param {string} method - Method of the HTTP Request (GET, POST, ...)
 *  @param {string} parseMode - Optional, by default "json"
 *  @param {Array} headers - List of headers (JSON format)
 *  @param {Object} content - Content of the HTTP request
 *  @return {Promise} - Return the success of the request
 */
function sendHTTPRequest({ url, method, parseMode, headers, content });
```

```javascript
// TODO
function configurePushNotification({ })
```

```javascript
// TODO
function sendPushNotification({ })
```


