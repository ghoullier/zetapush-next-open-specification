# Cloud Functions pour le service _SMSService_

---

# **TODO : Revoir façon de faire et mettre en cas d'utilisations** 

---

## Cloud Functions

```javascript
/**
 *  Configure the SMS tool sender, using OVH only (at this moment)
 *  @param {string} app_key - Application key of the service
 *  @param {string} app_secret - Application secret of the service
 *  @param {string} consumer_key - Consumer key of the service
 *  @param {string} service_name - Service name
 *  @return {Promise<boolean>} - Return the success of the request
 */
function configureSMS({ app_key, app_secret, consumer_key, service_name});
```

```javascript
/**
 *  Send an SMS using the configured tool (ZetaPush provides one by default)
 *  @param {string} sender - Name of the sender
 *  @param {string} message - SMS content
 *  @param {Array} to - Array of recicipents (phone number)
 *  @return {Promise<boolean>} - Return the success of the request 
 */
function sendSMS({ sender, message, to });
```
