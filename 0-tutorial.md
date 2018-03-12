# Créer un chat temps-réel avec ZetaPush

## Objectif

L'objectif principal de ce tutoriel est de te montrer la rapidité et la simplicité de développement avec ZetaPush. En quelques lignes de code, tu auras créé un chat temps réel qui sera déployé et utilisable immédiatement !

Pour ceci tu vas découvrir les services de ZetaPush qui te permettent de rapidement créer la partie back de ton application. Ensuite, tu vas voir comment étendre toi même ces services pour développer les fonctionnalités précises que tu souhaites.



## Pré-requis

Pour suivre ce tutoriel, tu as simplement besoin d'un éditeur de texte de type Visual Studio Code, Atom ou encore Vim. Tu peux utiliser ton IDE préféré si tu le souhaite. Si tu n'as pas ou peu de compétences en développement ce n'est pas grave, nous allons partir du début.

## Tutoriel

### Installation de nodejs / npm

- Installation des outils
- Lien pour chaque installation en fonction des plateformes (Linux / Windows / Mac)


### Initialisation du projet

- `npm init` pour créer l'architecture du projet
- `npm install --save zetapush` pour ajouter la dépendence à ZetaPush
- Création d'un dossier front (Ajouter une image de l'arborescence, même si elle est simple)
- Création de `index.html` , `style.css` et de `script.js` (plus import de ce dernier dans la page HTLM)
- Création et connexion d'un client ZetaPush :

    ```
    import ZetaPushClient from 'zetapush';

    const zpClient = new ZetaPushClient();

    zpClient.connect().then(() => {
        console.log('ZetaPush::ConnectionSuccessful');
    });
    ```

### Développement du front

- Création de la page HTML
- Ajout de CSS si nécessaire

### Utilisateur du service ZetaPush

- Écoute du service ZetaPush pour afficher les messages reçus :

    ```
    import ZetaPushClient from 'zetapush';

    const zpClient = new ZetaPushClient();

    const conversation = document.getElementById('conversationArea');

    zpClient.connect().then(() => {
        console.log('ZetaPush::ConnectionSuccessful');

        zpClient.listenService('chat', 'onMessage', (message) => {
            conversation.value += `\n (${message.author}) >>> ${message.value}`;
        });
    });
    ```

- Appel du service ZetaPush pour envoyer un message :

    ```
    import ZetaPushClient from 'zetapush';

    const zpClient = new ZetaPushClient();

    const conversation = document.getElementById('conversationArea');
    const btnAddMsg = document.getElementById('btnAddMsg');
    const inputMsg = document.getElementById('inputMsg');

    zpClient.connect().then(() => {
        console.log('ZetaPush::ConnectionSuccessful');

        zpClient.listenService('onMessage', (message) => {
            conversation.value += `\n (${message.author}) >>> ${message.value}`;
        });
    });

    btnAddMsg.addEventListener("click", () => {
        zpClient.callService.sendMessage(inputMsg.value);
    });
    ```

- Affichage d'un message lorsqu'un destinataire écrit

    ```
    import ZetaPushClient from 'zetapush';

    const zpClient = new ZetaPushClient();

    const conversation = document.getElementById('conversationArea');
    const btnAddMsg = document.getElementById('btnAddMsg');
    const inputMsg = document.getElementById('inputMsg');
    const displayUserTyping = document.getElementById('textUserTyping');

    let intervalTyping;

    zpClient.connect().then(() => {
        console.log('ZetaPush::ConnectionSuccessful');

        zpClient.listenService('onMessage', (message) => {
            conversation.value += `\n (${message.author}) >>> ${message.value}`;
        });

        zpClient.listenService('onUserTyping', (author) => {
            clearInterval(intervalTyping);
            displayUserTyping.value = `${author} is typing...`;

            intervalTyping = setTimeout(() => {
                displayUserTyping.value = '';
            }, 3000);
        });
    });

    btnAddMsg.addEventListener("click", () => {
        zpClient.callService.sendMessage(inputMsg.value);
    });
    ```

### Déploiement du code sur ZetaPush

- Utilisation de `zeta push` pour déployer sur ZetaPush
- Une barre de progression est affichée
- Un lien avec une URL pour le front est renvoyée.

### Personnalisation des participants (front)

- Modification de la partie front pour pouvoir saisir un nom dans le chat

### Création d'un service custom

- Création d'un fichier pour saisir son service custom
- Écriture du service custom :

    ```
    function renameUser(name: string) {
        ...
        ...
    }
    ```


- Appel du service custom pour personnaliser son nom

    ```
    import ZetaPushClient from 'zetapush';

    const zpClient = new ZetaPushClient();

    const conversation = document.getElementById('conversationArea');
    const btnAddMsg = document.getElementById('btnAddMsg');
    const inputMsg = document.getElementById('inputMsg');
    const displayUserTyping = document.getElementById('textUserTyping');
    const inputName = document.getElementById('inputName');
    const btnValidName = document.getElementById('btnValidName');

    let intervalTyping;

    zpClient.connect().then(() => {
        console.log('ZetaPush::ConnectionSuccessful');

        zpClient.listenService('onMessage', (message) => {
            conversation.value += `\n (${message.author}) >>> ${message.value}`;
        });

        zpClient.listenService('onUserTyping', (author) => {
            clearInterval(intervalTyping);
            displayUserTyping.value = `${author} is typing...`;

            intervalTyping = setTimeout(() => {
                displayUserTyping.value = '';
            }, 3000);
        });
    });

    btnAddMsg.addEventListener("click", () => {
        zpClient.callService.sendMessage(inputMsg.value);
    });
    
    btnValidName.addEventListener("click", () => {
        zpClient.callService.renameUser(inputName.value);
    });
    ```

### Déploiement du code sur ZetaPush

- Utilisation de `zeta push` pour déployer sur ZetaPush
- Une barre de progression est affichée
- Un lien avec une URL pour le front est renvoyée.


# Aller plus loin

- Présentation des services existantes (lien)
- Présentation de comment étendre un service existant (lien)