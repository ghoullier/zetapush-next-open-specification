# Cloud Functions pour le service _SecurityService_

## Prévisions

### setSecurityRule

La _cloud function_ permet d'ajouter des règles de sécurité sur les différentes _cloud services_. Nous pouvons par exemple chercher à bloquer l'envoi de mail pour les utilisateurs qui n'ont pas encore 18 ans :


```javascript
/**
 *  We can access to our _SecurityService_ by `securityService` variable
 *  We can access to our _CommunicationService_ by `communicationService` variable
 *  We can access to our _UserService_ by `userService` variable
 */
this.securityService.setSecurityRule({
    id: "ID_OF_MY_USER",
    cloud_function: this.communicationService.sendEmail,
    rule: async function() {
        // Get the user
        const user = await this.userService.getUserById({ id: "ID_OF_MY_USER"});
        // Apply the rule
        return user.age >= 18;
    }
})
```

## Cloud Functions

```javascript
/**
 *  Put security rules on groups or users
 *  @param {string} id - ID of the user or the group
 *  @param {string} cloud_function - Name of the cloud function affected by rule (example : "UserService.createUser()")
 *  @param {function} rule - Function that return a boolean
 *  @return {string} - Return the ID of the rule
 */
function setSecurityRule({ id, cloud_function, rule });
```
