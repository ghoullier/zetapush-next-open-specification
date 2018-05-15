# Créer un chat temps-réel avec ZetaPush

## Sommaire

1. [Introduction](#introduction)
2. [Initialisation du projet](#initialisation-du-projet)
3. [Création du design de l'application](#création-du-design-de-lapplication)
4. [Utilisation des _cloud services_](#utilisation-des-cloud-services)
5. [Déploiement de l'application](#déploiement-de-lapplication)
6. [Développement back avec ZetaPush](#développement-back-avec-zetapush)
7. [Utilisation d'un _custom cloud service_](#utilisation-dun-custom-cloud-service)
8. [Conclusion](#conclusion)

## Introduction

### Objectif

L'objectif de ce tutoriel est de construire une application de chat en utilisant ZetaPush depuis le démarrage du projet jusqu'à son déploiement.
Pour ceci tu vas découvrir comment utiliser les _cloud services_ de ZetaPush (chat, gestion des utilisateurs, etc...). Ensuite, tu vas voir comment développer toi même un service pour ajouter les fonctionnalités précises que tu souhaites.

### Pré-requis

Pour suivre ce tutoriel, tu as simplement besoin d'un éditeur de texte de type Visual Studio Code, Atom ou encore Vim. Tu peux utiliser l'IDE que tu souhaites.

À noter que dans ce tutoriel, tu écriras en _JavaScript_ pour plus de simplicité. En revanche pour tes futurs développements nous te recommandons d'utiliser _TypeScript_ puisque cela va te permettre d'utiliser d'avantage de fonctionnalités comme la génération de SDK ou de documentation par exemple. 

### Description du projet

Comme nous l'avons énoncé plus haut, tu vas créer une application de chat et plus précisément un **Avengers Chat** ! Le but est d'avoir un chat en pouvant choisir son personnage des Avengers. Chaque Avenger aura plusieurs compétences qui lui seront associées et qu'il pourra utiliser sur le chat (Un message sera affiché dans le chat). Ce dernier sera une application web avec le code front déployé.

Voici la liste des personnages d'Avengers avec leurs compétences :

| Personnage      | Compétences                             |
| :-------------: | :-------------------------------------: |
| Captain America | Lancer de bouclier / Guérison           |
| Oeil de Faucon  | Tir à l'arc / Super vision              |
| Iron Man        | Vol / Lance missile                     |
| Hulk            | Coup de poing / Régénération            |
| Thor            | Coup de marteau / Contrôle de la foudre |
| Spider-Man      | Lancé de toile / Saut avec toile        |
| Wolverine       | Coup de griffes / Régénération          |


Voici le résultat final de l'application :

---
[CAPTURE ECRAN] Capture d'écran du chat lors de son utilisation avec plusieurs personnages et messages

---

Dans un premier temps tu vas préparer ton environnement de travail et initialiser un projet avec la CLI ZetaPush. La CLI est juste là pour te permettre d'aller plus vite, tu pourrais bien-sûr créer ton projet from scratch.

---
[CAPTURE ECRAN] Capture d'écran de la sortie de CLI qui génère un squelette de ton projet

---

Ensuite, tu vas réaliser la première partie du chat. C'est à dire créer un chat temps réel sans pouvoir choisir son personnage au démarrage de l'application. Pour ceci tu vas d'abord te concentrer sur le design de ton application web, puis tu vas apprendre à utiliser les _cloud services_ pour ajouter la partie fonctionnelle du chat.

---
[CAPTURE ECRAN] Capture d'écran du design de l'application, sans le choix des personnages, il y aura donc les id des utilisateurs d'affichés pour chaque message envoyé

---

À ce moment ton chat est prêt et fonctionnel, donc tu souhaiteras sûrement déployer ton application. C'est ici que tu vas découvrir la commande `zeta push` qui va te permettre de déployer le code back et que ton chat soit réellement fonctionnel.

---
[CAPTURE ECRAN] Capture d'écran de la sortie de la CLI après un `zeta push`

---

Ton chat fonctionne, mais ce que tu voulais c'est aussi pouvoir choisir ton personnage des Avengers au lancement de ton application et utiliser ses compétences associées. Ce n'est pas un comportement fournit par défaut par ZetaPush, donc tu vas pouvoir créer cette fonctionnalité dans un _custom cloud service_ (présenté plus tard). Ici notre fonctionnalité sera la possibilité pour un personnage d'utiliser une compétence aléatoire dans la liste des compétences qui lui sont affectées.

Une fois que tu as écrit et déployé ta fonctionnalité, tu vas pouvoir l'utiliser et mettre à jour ton application.

---
[CAPTURE ECRAN] Capture d'écran de l'écran de sélection d'un personnage d'Avengers

---

Avec toutes ces étapes tu pourras chatter avec les Avengers !

---
[CAPTURE ECRAN] De retour la capture d'écran de l'application finie ?

---

## Initialisation du projet

Pour utiliser ZetaPush, tu n'as besoin d'aucune dépendances extérieures. En revanche, dans le cadre de ce tutoriel, nous allons utiliser la CLI ZetaPush (pour un gain de productivité). Tu auras donc besoin de _NodeJS_ (et implicitement _npm_) pour ceci. Il te faut donc installer _NodeJS_ via : https://nodejs.org

Comme ici tu vas utiliser la CLI ZetaPush, installe la :

```bash
$ npm install -g @zetapush/cli
```

Une fois que c'est fait, tu vas pouvoir initialiser ton Avengers chat.

Pour initialiser ton application, tu as plusieurs possibilités. Tu peux utiliser le wizard disponible sur https://console.zetapush.com (En cours de développement) qui va te guider pas à pas, utiliser la CLI ou encore démarrer en créant manuellement les fichiers nécessaires. Ici tu vas directement utiliser la CLI.


Voici la démarche à suivre pour utiliser ton projet :

```bash
$ cd ~/workspace
$ zeta new avengers-chat
```

Si tu veux plus de détails sur la commande `zeta new` tu peux utiliser `zeta new --help` ou voir la documentation sur https://console.zetapush.com/documentation/new


Cette commande va te créer l'arborescence suivante :

```bash
.
└── avengers-chat
    ├── .package.json
    ├── .zetarc
    ├── .gitignore
    ├── worker
    │   └── index.js
    └── front
        ├── index.html
        └── index.js
```


Le fichier `.package.json` comporte les différentes dépendances nécessaires à l'utilisation de ZetaPush (_@zetapush/js_ et _@zetapush/server_). Ensuite le fichier `.zetarc` comporte la configuration nécessaire à l'identification de ton compte sur la plateforme ZetaPush. En effet, un compte temporaire t'es automatiquement créé sur ZetaPush (Avec ton application **avengers-chat** d'associée). Tu peux dès à présent rentre ton compte permanent en te rendant sur https://console.zetapush.com ou en utilisant la CLI.

Cette commande va te créer une arborescence de projet pour différencier ton code front et ton code back qui sera utilisé plus tard dans ce tutoriel (nous appellerons custom could services la partie back).
Le découpage en deux projets n'est pas obligatoire mais c'est une bonne pratique pour bien différencier les différentes composantes de ton application. De plus dans le cadre du tutoriel, ceci te permettra de bien comprendre les interactions entre le front et les customs services. Comme tu as pu le voir, la CLI te donne un code d'exemple. Nous n'allons pas l'utiliser donc tu peux supprimer de contenu de `worker/index.js`, `front/index.html` et de `front/index.js`.

---
### Activation d'un compte via la CLI

Il est possible d'activer un compte temporaire via la CLI. Pour ça il faut que tu sois dans un dossier où se trouve un fichier `.zetarc` (Ou dans un des dossiers parent) avec les identifiants d'un compte temporaire. À ce moment là tu peux lancer la commande :

```console
$ zeta account register
Choose your login : damien
Choose your password : *******
Choose your email : damien@gmail.com
``` 
---

Les fichiers `worker/index.js` / `front/index.html` et `front/index.js` sont remplis d'un exemple de projet type _Hello World_. Tu peux t'y inspirer pour créer une application mais dans ce tutoriel tu peux supprimer le contenu de ces fichiers, nous allons partir de zéro.

Maintenant que ton application est prête à ếtre développée, commence par créer le design.

## Création du design de l'application

Dans cette section tu vas commencer par faire le design de ton Avengers Chat. Voici à quoi ça va ressembler :

![Design sans gestion des Avengers](./images/tuto-design-only.png)

Dans ce tutoriel ce n'est pas la partie design de l'application qui nous intéresse, donc voici les fichiers à utiliser, tu peux directement les copier-coller. À noter que nous avons ajouté un fichier `style.css` dans le sous-dossier `front`.

### **front/index.html**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bulma/0.6.2/css/bulma.min.css">
    <link rel="stylesheet" href="./style.css">
    <title>Avengers Chat</title>
</head>

<body>
    <!-- Area where we add the messages -->
    <div class="content" id="conversation"></div>

    <div id="buttons">
        <input placeholder="Your message" />
        <button class="button">Send</button>
    </div>
    <script src="./index.js"></script>
</body>

</html>
```

### **front/style.css**

```css
body {
    display: flex;
    justify-content: start;
    flex-direction: column;
    align-items: center;
}

#buttons {
    display: flex;
    justify-content: flex-start;
    width: 70%;
    height: 5vh;
    max-width: 700px;
}

input {
    width: 80%;
    padding: 10px;
}

.button {
    width: 20%;
    height: 100%;
}

#conversation {
    margin: 5vh;
    border: 5px double grey;
    width: 70%;
    height: 40vh;
    max-width: 700px;
    padding: 10px;
    overflow-y: auto;
}
```

Le design est maintenant prêt, utilise à présent les _cloud services_ déjà existants sur ZetaPush pour rajouter le fonctionnel du chat.

## Utilisation des _cloud services_

Pour que ton chat fonctionne il te faut 3 choses dans ton application :
- Une connexion à la plateforme ZetaPush
- Un moyen d'envoyer un message
- Un moyen d'écouter les nouveaux messages



Dans ton _Avengers Chat_, tu vas te connecter auprès de ZetaPush en tant qu'utilisateur anonyme.

Dans la plupart des cas tu utiliseras une connexion "standard" avec un couple login/mot de passe, mais ici, une connexion anonyme va te suffire.
Tu peux avoir plus de détails sur ces deux modes de connexion dans la [documentation](https://console.zetapush/documentation/connexion)

Le package `@zetapush/front` te permets d'utiliser le SDK JavaScript et d'avoir accès à tous les _Cloud Services_ fournis par ZetaPush.

Voici le code source pour avoir une connexion d'un point de vue applicatif au démarrage de ton application avec une authentification anonyme :

### **front/index.js**

```javascript
import { ZetaPushClient } from "@zetapush/front";

// Create the ZetaPush client to communicate with the platform and cloud services
const zpClient = new ZetaPushClient();

// Launch an anonymous connection at launch of the application
await zpClient.connect();
```

---

Ensuite, pour envoyer un message et recevoir les messages entrants, tu vas pouvoir utiliser le _cloud service_ `ChatService` fourni par ZetaPush. Ce dernier va te fournir les _cloud function_ `sendMessage()` et `listenIncomingMessages()` pour répondre à ton besoin. Voici comment les utiliser :

### **front/index.js**

```javascript
import { ZetaPushClient } from "@zetapush/front";
import { ChatService } from "@zetapush/services";

// Get the elements from the HTML
const validBtn = document.getElementById("valid-button");
const inputMsg = document.getElementById("input-message");
const conversation = document.getElementById("conversation");

// Create the ZetaPush client to communicate with the platform and cloud services
const zpClient = new ZetaPushClient();

// Create a new ChatService instance to use this CloudService
export const chatService = new ChatService();

// Launch an anonymous connection at launch of the application
await zpClient.connect();

// When the user click on the validation button,
// the application send a new message to the chat (from the input)
validBtn.addEventListener("click", function() {
	// Get the typed message by the user from the input
	const inputValue = inputMsg.value;

	// We send the message only if the input if not null
	if (inputMsg.length > 0) {
		// We send the message to all users (also the sender)
		chatService.sendMessage({ message: inputValue, notify_to_sender: true });
	}
});

// We need to listen incoming messages and add them to the text area to display them
chatService.listenIncomingMessages({
	callback: function(message) {
		conversation.innerHTML += `<p>${message.sender} >>> ${message.content}</p>`;
	}
});
```


Le fonctionnel de ton chat est maintenant fait, il te faut maintenant déployer le fonctionnel de ton application.

--- 
### _cloud services et cloud functions_

Petite précision concernant les _cloud services_ et les _cloud functions_. Un _cloud service_ est un ensemble de _cloud functions_ regroupées par thème. C'est à dire que nous avons des _cloud services_ pour le chat, la gestion d'utilisateurs, la remontée de données, etc... La _cloud function_ effectue une action précise, comme par exemple `createUser()`, `sendMessage()` ou encore `pushData()`.

La liste de l'ensemble des _cloud services_ existants est disponible sur https://console.zetapush.com/documentation/cloud_services

---

## Déploiement de l'application

C'est ici que tu vas découvrir la commande `zeta push`. Cette dernière va te permettre, en une seule ligne, de déployer le fonctionnel de ton application et d'avoir un **Avengers Chat** qui fonctionne.

Pour l'instant nous avons seulement du code front, nous n'avons pas encore créé de _custom cloud service_ (tu verras en détails ce que c'est par la suite), donc voici la commande à exécuter :

```bash
$ zeta push --front-only
```

Si tu veux plus de détails sur la commande `zeta push` tu peux utiliser `zeta push --help` ou voir la documentation sur https://console.zetapush.com/documentation/push

Cette commande va faire plusieurs choses :
- Ajouter les _cloud services_ utiles à ton application (ici `ChatService`)
- Brancher le front avec les _cloud services_

---
[CAPTURE ECRAN] Capture de la barre de progression de la CLI

---

Une fois le déploiement effectué, la CLI va te retourner une période de validité de ton application si tu n'as pas activé ton compte. Au même titre que ton compte sur la plateforme ZetaPush, ton application est temporaire tant que ton compte n'est pas validé (à faire via https://console.zetapush.com ou via la CLI).


Maintenant tu peux lancer ta page web en local et voir le fonctionnement de ton **Avengers Chat**. Pour ça tu peux utiliser la méthode que tu veux, mais un moyen simple de le faire est de se positionner dans le dossier `avengers-chat/front/` et d'y lancer la commande suivante :

```console
$ npx serve .
``` 

À présent ton application est présente sur https://localhost:5000 et tu peux y voir ton chat fonctionner !

Pour l'instant, nous ne gérons pas les utilisateurs donc ce sont les identifiants uniques par utilisateur qui sont affichés en tant que membre du chat. Tu vas y remédier tout de suite en ajoutant ta nouvelle fonctionnalité dans un _custom cloud service_.

## Développement back avec ZetaPush

Pour créer ton code métier tu vas créer un _custom cloud service_. 

---
### Précisions

Un _custom cloud service_ est exactement la même chose qu'un _cloud service_ sauf qu'ici, c'est toi qui va le créer. Une fois déployé sur ton application, tu vas pouvoir l'utiliser de la même manière qu'un _cloud service_.

Tu pourrais créer cette logique métier côté front, mais c'est toujours une bonne pratique de mettre ton code fonctionnel, propre à ton application, côté back, surtout si tu décides d'avoir plusieurs fronts (Web, Android, iOS par exemple).

---

Ton _custom cloud service_ va te permettre de choisir ton personnage des _Avengers_ quand tu accèdes au chat et de lancer des actions en fonction des compétences de chaque avengers. Voici la démarche à suivre :

1. Enregistrer les _Avengers_ et leurs compétences associées dans le _Custom Cloud Service_
2. Réaliser l'UI pour choisir son _Avenger_ 
3. Réaliser l'UI pour lancer une attaque avec son _Avenger_
4. Brancher la sélection du _Avenger_ dans le _Custom Cloud Service_
5. Brancher le lancement d'une attaque dans le _Custom Cloud Service_

### Enregister les _Avengers_ et leurs compétences

Afin d'enregistrer les différents _Avengers_ et leurs compétences associées, tu créé un nouveau fichier. 
C'est une bonne pratique de mettre ce genre d'informations dans un fichier à part.


#### **utils/avengers.js**

```javascript
export const avengers = [
	{ id: 0, name: "Captain America",skills: ["Lancer de bouclier", "Guérison"] },
	{ id: 1, name: "Oeil de Faucon", skills: ["Tir à l'arc", "Super vision"] },
	{ id: 2, name: "Iron Man", skills: ["Vol", "Lance missile"] },
	{ id: 3, name: "Hulk", skills: ["Coup de poing", "Regénération"] },
	{ id: 4, name: "Thor", skills: ["Coup de marteau", "Contrôle de la foudre"] },
	{ id: 5, name: "Spider-Man", skills: ["Lancé de toile", "Saut avec toile"] },
	{ id: 6, name: "Wolverine", skills: ["Coup de griffes", "Regénération"] }
];

```

### Réaliser l'UI

À présent, ajoute l'UI pour sélectionner l'_Avenger_ au démarrage de l'application et lancer l'exécution d'une attaque sur le chat.

#### **front/index.html**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bulma/0.6.2/css/bulma.min.css">
    <link rel="stylesheet" href="./style.css">
    <title>Avengers Chat</title>
</head>

<body>
    <div id="modal-select-avengers">
        <p id="title-modal">Select your Avenger :</p>

        <select id="select-avenger">
            <option value="0">Captain America</option>
            <option value="1">Oeil de Faucon</option>
            <option value="2">Iron Man</option>
            <option value="3">Hulk</option>
            <option value="4">Thor</option>
            <option value="5">Spider-Man</option>
            <option value="6">Wolverine</option>
        </select>

        <button id="select-avenger-button" onclick="validAvenger()">Valid</button>

    </div>

    <!-- Area where we add the messages -->
    <div class="content" id="conversation"></div>
    <div id="buttons">
        <input id="input-message" placeholder="Your message" />
        <button id="valid-button" class="button">Send</button>
        <button id="attack-button" class="button">Attack</button>
    </div>

    <script type="module" src="./index.js"></script>
</body>

</html>
```

#### **front/style.css**

```css
body {
	display: flex;
	justify-content: start;
	flex-direction: column;
	align-items: center;
}

#buttons {
	display: flex;
	justify-content: flex-start;
	width: 70%;
	height: 5vh;
	max-width: 700px;
}

#input-message {
	width: 80%;
	padding: 10px;
}

.button {
	width: 20%;
	height: 100%;
}

#conversation {
	margin: 5vh;
	border: 5px double grey;
	width: 70%;
	height: 40vh;
	max-width: 700px;
	padding: 10px;
	overflow-y: auto;
}

#modal-select-avengers {
	width: 25vw;
	height: 25vh;
	position: absolute;
	left: 50%;
	top: 35%;
	transform: translate(-50%, -50%);
	z-index: 0;
	border: 1px solid grey;
	background-color: blanchedalmond;
}

#title-modal {
	margin: 5px;
	font-style: oblique;
}

form {
	display: flex;
	flex-direction: column;
	align-items: center;
}

#modal-select-avengers {
	display: flex;
	flex-direction: column;
	align-items: center;
}

#select-avenger-button {
	margin-top: 50px;
	width: 100px;
}

#select-avenger {
	margin-top: 50px;
}
```


### Sélection d'un _Avenger_ au démarrage

Maintenant il te faut brancher la sélection de ton _Avenger_ sur l'envoi du message. 
Pour ça tu fais appel à `sendMessage()` en changeant le paramètre `sender`.

#### **front/index.js**


```javascript
import { ZetaPushClient } from "@zetapush/front";
import { ChatService } from "@zetapush/services";
import { avengers } from "../utils/avengers.js";

// Get the elements from the HTML
const validBtn = document.getElementById("valid-button");
const inputMsg = document.getElementById("input-message");
const conversation = document.getElementById("conversation");
const inputAvenger = document.getElementById("select-avenger");
const modalSelectAvenger = document.getElementById("modal-select-avengers");

// The name of our Avenger
let avengerName = "";

// Create the ZetaPush client to communicate with the platform and cloud services
const zpClient = new ZetaPushClient();

// Create a new ChatService instance to use this CloudService
export const chatService = new ChatService();

// Launch an anonymous connection at launch of the application
await zpClient.connect();

// When the user click on the validation button,
// the application send a new message to the chat (from the input)
validBtn.addEventListener("click", function() {
	// Get the typed message by the user from the input
	const inputValue = inputMsg.value;

	// We send the message only if the input if not null
	if (inputMsg.length > 0) {
		// We send the message to all users (also the sender)
		chatService.sendMessage({ message: inputValue, notify_to_sender: true, sender: avengerName });
	}
});

// We need to listen incoming messages and add them to the text area to display them
chatService.listenIncomingMessages({
	callback: function(message) {
		conversation.innerHTML += `<p>${message.sender} >>> ${message.content}</p>`;
	}
});

/**
 * Function to set the sender value
 */
window.validAvenger = function() {
	avengerName = avengers[inputAvenger.value].name;
	modalSelectAvenger.style.display = "none";
};
```

### Lancement d'une attaque
 
 C'est à ce moment la que tu vas créer ta première _Cloud Function_.
 Son rôle est de lancer une attaque sur le chat, en fonction des compétences de ton _Avenger_. Pour ceci voici le _Cloud Service_ que tu vas créer :

#### **worker/index.js**

```javascript
import { avengers } from "../utils/avengers.js";
import { chatService } from "../front/index";

/**
 * Cloud Service to manage Avengers
 */
class AvengerService {
	/**
	 * Attack with a random skill
	 * @param {number} index
	 * @param {name} name
	 */
	attackWithRandomSkill(index, name) {
		// Get the random skill
		const usedSkill =
			avengers[index].skills[
				Math.floor(Math.random() * avengers[index].skills.length)
			];

		// Send the message to the chatroom
		chatService.sendMessage({
			message: `${name} attacks with : ${usedSkill}`,
			notify_to_sender: true,
			sender: name
		});
	}
}
```

## Déploiement


Maintenant que ton code est prêt, il te faut à nouveau déployer ton application pour que le fonctionnel soit mis à jour.
Tu as cette fois ci une partie back-end donc tu utilises :

```bash
$ zeta push
```

La aussi tu peux utiliser la méthode que tu veux pour lancer ta page HTML en local. Tu peux par exemple faire :

```console
$ cd avengers-chat/front
$ npx serve .
```

Tu vois maintenant ton **Avengers Chat** de complètement fonctionnel sur https://localhost:5000.

## Conclusion

Ton **Avengers Chat** est prêt, tu vas pouvoir communiquer avec les Avengers ! 
Tout au long de ce tutoriel, tu as pu voir comment utiliser les _cloud services_ de ZetaPush et même créer tes propres fonctionnalités en utilisant les _custom cloud services_. 
À présent n'hésite pas à aller sur https://console.zetapush.com pour gérer ton application, ou voir les _cloud services_ disponibles chez ZetaPush. 
