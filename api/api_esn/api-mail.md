# Cloud Functions pour le service _MailService_

## Cloud Functions

```javascript
/**
 *  Configure the email tool sender
 *  @param {string} smtp_user - SMTP User
 *  @param {string} smtp_pass - SMTP Password
 *  @param {string} smtp_host - SMTP Host
 *  @param {number} smtp_port - SMTP Port (default 25)
 *  @param {boolean} ssl - Enable SSL
 *  @param {boolean} starttls - Enable STARTTLS
 *  @return {Promise<boolean>} - Return the success of the request
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
 *  @return {Promise<boolean>} - Return the success of the request
 */
function sendEmail({ to, sender, html, subject, cc, bcc });
```