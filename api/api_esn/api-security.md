# Cloud Functions pour le service _SecurityService_

```javascript
/**
 *  Put security rules on group or users
 *  @param {string} id - ID of the user or the group
 *  @param {string} cloud_function - Name of the cloud function affected by rule (example : "UserService.createUser()")
 *  @param {function} rule - Function that return a boolean
 *  @return {string} - Return the ID of the rule
 */
function setSecurityRule({ id, cloud_function, rule });
```

## Examples

### setSecurityRule

Only the users with age >= 18 can send email. We assume that we can access to our _SecurityService_ by `securityService` variable, _CommunicationService_ by `communicationService` variable and _UserService_ by `userService` variable.

```javascript
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