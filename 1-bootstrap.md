# Objectifs

- Un développeur front doit pouvoir utiliser les services ZetaPush dans son code front.
- Un développeur full-stack doit pouvoir utiliser les services ZetaPush dans son code front et coder son propre métier pour simplifier le développement de son/ses front(s).
- Un développeur doit pouvoir initialiser un squelette de projet avec la CLI

Les profils utilisés sont définis dans [commun.md](./commun.md).

Pour chaque User Story, nous définissons seulement les fichiers qui sont créés. Pour voir le contenu de chacun, voir la rubrique _fichiers créés_.

# Pré-requis

* J'utilise mon éditeur de texte ou IDE préféré.


# <a name="parcours-1"></a> Parcours 1 : Je développe une application front avec ZetaPush sans service custom

## User stories

### ETQ dev front je veux créer une application sans CLI

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- Je souhaite créer une application nommée **myApp** et seulement utiliser les _Cloud Services_ existants

*WHEN*
- Je créé l'arboresence suivante :

  ```
  .
  ├── .zetarc
  ├── .gitignore
  ├── front
      ├── index.html
      └── index.js
  └── package.json
  ```
- Je remplis `.zetarc` avec mes identifiants de connexion à mon compte ZetaPush
- Je remplis `.gitignore` pour éviter d'envoyer mes identifiants de connexion sur GitHub
- Je créé un dossier `front/`, c'est ici que mon code front sera stocké
- Je remplis `package.json` avec le nom de mon application
- Je remplis `package.json` avec le chemin relatif vers mon code front
- J'installe la dépendance _@zetapush/front_ avec : `npm install --save @zetapush/front`

*THEN*
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_

### ETQ de front je veux utiliser les _Cloud Services_ dans mon application existante sans CLI

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- J'ai une application existante nommée **myApp** et je souhaite seulement utiliser les _Cloud Services_ existants
- Mon code est sous l'arboresence suivante :
```
  myApp
    ├── index.html
    └── index.js
```

*WHEN*
- Je déplace mon code front dans un sous dossier pour plus de clarté
- Je remplis `.zetarc` avec mes identifiants de connexion à mon compte ZetaPush
- Je remplis `.gitignore` pour éviter d'envoyer mes identifiants de connexion sur GitHub
- Je remplis `package.json` avec le nom de mon application
- Je remplis `package.json` avec le chemin relatif vers mon code front
- J'installe la dépendance _@zetapush/front_ avec : `npm install --save @zetapush/front`

*THEN*
- J'ai l'arborescence suivante qui est créée :
  ```
  myApp
  ├── .zetarc
  ├── .gitignore
  ├── front
      ├── index.html
      └── index.js
  └── package.json
  ```
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_


### ETQ dev front je veux créer une application avec la CLI

*GIVEN*
- J'ai la dépendance à `@zetapush/cli` qui est installée en global
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- Je souhaite créer une application nommée **myApp** et seulement utiliser les _Cloud Services_ existants

*WHEN*
- Lorsque je lance la commande : `zeta init myApp --user user@gmail.com --password password --front-only`

*THEN*
- Une application au nom de **myApp** a été ajouté à mon compte ZetaPush
- Une arborescence fichier à été créée sous la forme :

  ```
  .
  ├── .zetarc
  ├── .gitignore
  ├── front
      └── index.html
      └── index.js
  ├── README.md
  └── package.json
  ```
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_
- La sortie de la console est la suivante :

```
Welcome to ZetaPush !

A new application named myApp was added to your account.
Now you can use Cloud Services in your application. You can see the documentation here : https://console.zetapush.com/documentation

To deploy your application you can use the command zeta push. You have already an existing use of Cloud Service in front/index.js, test it !
```

### ETQ dev front je veux créer une application avec la CLI sans compte existant

*GIVEN*
- J'ai la dépendance à `@zetapush/cli` qui est installée en global
- Je n'ai pas de compte ZetaPush existant
- Je souhaite créer une application nommée **myApp** et seulement utiliser les _Cloud Services_ existants

*WHEN*
- Lorsque je lance la commande : `zeta init myApp --front-only`

*THEN*
- Un compte temporaire sur la plateforme ZetaPush a été créé
- Une application au nom de **myApp** a été ajouté à ce compte
- Je suis alerté que mon compte est temporaire (message dans la console)
- Une arborescence fichier à été créée sous la forme :

  ```
  .
  ├── .zetarc
  ├── .gitignore
  ├── front
      └── index.html
      └── index.js
  ├── README.md
  └── package.json
  ```
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_
- La sortie de la console est la suivante :

```
Welcome to ZetaPush !

A new application named myApp was added to your account.
Now you can use Cloud Services in your application. You can see the documentation here : https://console.zetapush.com/documentation

To deploy your application you can use the command zeta push. You have already an existing use of Cloud Service in front/index.js, test it !

As no account is specified, a temporary account has been created for you : 
    - login: vsgygfzq12ffq4fq
    - password: zhfuqzbvgfhreq4f56q4fqf6
    This account is only available for X days.
    You can convert this temporary account into a permanent account with your own login/password here : 
    https://console.zetapush.com/account/register/vsgygfzq12ffq4fq/zhfuqzbvgfhreq4f56q4fqf6
    NOTE: By registering, your current work and data will be kept
```

### ETQ dev front je veux utiliser les _Cloud Services_ dans mon application existante en utilisant la CLI

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- J'ai une application existante nommée **myApp** et seulement utiliser les _Cloud Services_ existants
- Mon code est sous l'arborescence suivante :
```
  myApp
    ├── index.html
    └── index.js
```

*WHEN*
- Lorsque je lance la commande `zeta init --front-only --existing-app --user user@gmail.com --password password` au sein de mon dossier `myApp`

*THEN*
- J'ai l'arborescence suivante qui est créée :
  ```
  myApp
  ├── .zetarc
  ├── .gitignore
  ├── index.html
  └── index.js
  └── package.json
  ```
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_
- Il est possible de spécifier où se trouve le code front avec l'argument `--front /path/`
- Pour une meilleure clarté, il est utile de déplacer le code front dans un sous dossier au préalable
- La sortie de la console est la suivante :

```
Welcome to ZetaPush !

A new application named myApp was added to your account.
Now you can use Cloud Services in your application. You can see the documentation here : https://console.zetapush.com/documentation

To deploy your application you can use the command zeta push.
```

# <a name="parcours-2"></a> Parcours 2 : Je développe une application front avec ZetaPush avec service custom

## User stories

### ETQ dev full-stack je créé une application

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- Je souhaite créer une application nommée **myApp** , utiliser les _Cloud Services_ existants et pouvoir créer mes _Custom Cloud Services_

*WHEN*
- Je créé l'arboresence suivante :

  ```
  .
  ├── .zetarc
  ├── .gitignore
  ├── front
      ├── index.html
      └── index.js
  ├── server
      └── index.js
  └── package.json
  ```
- Je remplis `.zetarc` avec mes identifiants de connexion à mon compte ZetaPush
- Je remplis `.gitignore` pour éviter d'envoyer mes identifiants de connexion sur GitHub
- Je créé un dossier `front/`, c'est ici que mon code front sera stocké
- Je créé un dossier `server/`, c'est ici que mon code back sera stocké
- Je remplis `package.json` avec le nom de mon application
- Je remplis `package.json` avec les chemins relatifs vers mon code front et mon code back 
- J'installe la dépendance _@zetapush/front_ avec : `npm install --save @zetapush/front`
- J'installe la dépendance _@zetapush/server_ avec : `npm install --save @zetapush/server`

*THEN*
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_ et à créer mes _Custom Cloud Services_.


### ETQ dev full-stack j'ajoute la possibilité d'utiliser des _Cloud Services_ et de créer des _Custom Cloud Services_ au sein d'une application existante

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- J'ai une application existante nommée **myApp** et je souhaite utiliser les _Cloud Services_ existants et créer mes _Custom Cloud Services_
- Mon code est sous l'arboresence suivante :
```
  myApp
    ├── index.html
    └── index.js
```

*WHEN*
- Je déplace mon code front dans un sous dossier `front` pour plus de clarté
- Je créé un dossier `server` pour y stocker mon code back
- Je remplis `.zetarc` avec mes identifiants de connexion à mon compte ZetaPush
- Je remplis `.gitignore` pour éviter d'envoyer mes identifiants de connexion sur GitHub
- Je remplis un `package.json` avec le nom de mon application
- Je remplis `package.json` avec les chemins relatifs vers mon code front et mon code back
- J'installe la dépendance _@zetapush/front_ avec : `npm install --save @zetapush/front`
- J'installe la dépendance _@zetapush/server_ avec : `npm install --save @zetapush/server`

*THEN*
- J'ai l'arborescence suivante qui est créée :
  ```
  myApp
  ├── .zetarc
  ├── .gitignore
  ├── front
      ├── index.html
      └── index.js
  ├── back
      └── index.js
  └── package.json
  ```
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_



### ETQ dev full-stack je créé une application avec la CLI 

*GIVEN*
- J'ai la dépendance à `@zetapush/cli` qui est installée en global
- J'ai un compte ZetaPush existant avec user@gmail.com / password comme couple login/password
- Je souhaite créer une application avec une partie front et une partie back

*WHEN*
- Lorsque je lance la commande : `zeta init myApp --user user@gmail.com --password password`

*THEN*
- Une application au nom de **myApp** a été ajouté à mon compte ZetaPush
- Une arborescence fichier à été créée sous la forme :

  ```
  .
  ├── .zetarc
  ├── .gitignore
  ├── front
      ├── index.html
      └── index.js
  ├── server
      └── index.js
  ├── README.md
  └── package.json
  ```

- J'ai un README.md avec les informations m'indiquant comment démarrer (utilisation de la CLI, les bonnes pratiques ZetaPush, les liens vers la documentation)
- La console m'affiche toutes les informations précédentes de la manière suivante :

```
Welcome to ZetaPush !

A new application named myApp was added to your account.
Now you can use Cloud Services in your application. You can see the documentation here : https://console.zetapush.com/documentation

To deploy your application you can use the command zeta push.  You have already an existing use of Cloud Service in front/index.js, test it !
  ```



### ETQ dev full-stack je créé une application avec la CLI sans compte existant

*GIVEN*
- J'ai la dépendance à `@zetapush/cli` qui est installée en global
- Je n'ai pas de compte ZetaPush
- Je souhaite créer une application avec une partie front et une partie back

*WHEN*
- Lorsque je lance la commande : `zeta init myApp`

*THEN*
- Un compte temporaire sur la plateforme ZetaPush a été créé
- Une application au nom de **myApp** a été ajouté à ce compte
- Je suis alerté que mon compte est temporaire et que je peux le rendre permanent sur https://console.zetapush.com
- Une arborescence fichier à été créée sous la forme :

  ```
  .
  ├── .zetarc
  ├── .gitignore
  ├── front
      └── index.html
      └── index.js
      └── style.css
  ├── server
      └── index.js
  ├── README.md
  └── package.json
  ```

- Un lien pour accèder à mon compte avec les crédentials est affiché dans la console
- Une aide sur le déploiement de l'application est affiché dans la console (Comment utiliser `zeta push`)
- J'ai un README.md avec les informations m'indiquant comment démarrer (utilisation de la CLI, les bonnes pratiques ZetaPush, les liens vers la documentation)
- La console m'affiche toutes les informations précédentes de la manière suivante :

```
Welcome to ZetaPush !

As no account is specified, a temporary account has been created for you : 
- login: vsgygfzq12ffq4fq
- password: zhfuqzbvgfhreq4f56q4fqf6
This account is only available for X days.
You can convert this temporary account into a permanent account with your own login/password here : 
https://console.zetapush.com/account/register/vsgygfzq12ffq4fq/zhfuqzbvgfhreq4f56q4fqf6
NOTE: By registering, your current work and data will be kept

A new application named myApp was added to your account.
Now you can use Cloud Services in your application. You can see the documentation here : https://console.zetapush.com/documentation. You have already an existing use of Cloud Service in front/index.js, test it !
```

### ETQ dev full-stack je créé une application avec la CLI et une arborescence spécifiée

*GIVEN*
- J'ai la dépendance à `@zetapush/cli` qui est installée en global
- J'ai un compte ZetaPush existant avec user@gmail.com / password comme couple login/password
- Je souhaite créer une application avec une partie front et une partie back

*WHEN*
- Lorsque je lance la commande : `zeta init myApp --user user@gmail.com --password password --front ./front --back ./server`

*THEN*
- Une application au nom de **myApp** a été ajouté à mon compte ZetaPush
- Une arborescence fichier à été créée sous la forme :

  ```
  .
  ├── .zetarc
  ├── .gitignore
  ├── front
      └── index.html
      └── index.js
      └── style.css
  ├── server
      └── index.js
  ├── README.md
  └── package.json
  ```

- J'ai un README.md avec les informations m'indiquant comment démarrer (utilisation de la CLI, les bonnes pratiques ZetaPush, les liens vers la documentation)
- La console m'affiche toutes les informations précédentes de la manière suivante :

```
Welcome to ZetaPush !

A new application named myApp was added to your account.
Now you can use Cloud Services in your application. You can see the documentation here : https://console.zetapush.com/documentation

To deploy your application you can use the command zeta push. You have already an existing use of Cloud Service in front/index.js, test it !
  ```


### ETQ dev full-stack j'ajoute la possibilité de créer des _Custom Cloud Services_ au sein d'une application existante avec la CLI


*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- J'ai une application existante nommée **myApp** et je souhaite utiliser les _Cloud Services_ existants et créer mes _Custom Cloud Services_
- Mon code est sous l'arboresence suivante :
```
  myApp
    ├── index.html
    └── index.js
```

*WHEN*
- Lorsque de lance la commande `zeta init myApp --existing-app --user user@gmail.com --password password`


*THEN*
- J'ai l'arborescence suivante qui est créée :
  ```
  myApp
  ├── .zetarc
  ├── .gitignore
  ├── index.html
  ├── index.js
  ├── back
  └── package.json
  ```
- Les dépendances _@zetapush/front_ et _@zetapush/server_ ont été installées
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_
- Il peut être intéressant pour plus de clarté de déplacer dans le front dans un sous-dossier


# Fichiers créés / à créer

Cette section permet de spécifier ce que contient chaque fichier dans l'arborescence créée ou à créer dans lors de l'initialisation de projet.

## .zetarc

```bash
# Compte existant sur la plateforme ZetaPush
zeta_user = user@gmail.com
zeta_password = password
``` 

## .gitignore

Fichier utile seulement pour empêcher l'utilisateur d'envoyer ses identifiants de connexion sur GitHub par exemple.

```bash
.zetarc
```

## package.json

Comporte le nom de l'application ainsi que les dépendances ZetaPush nécessaires.

```json
{
  "name": "myApp",
  "version": "0.0.1",
  "dependencies": {
    "@zetapush/front": "1.0.0",
    "@zetapush/server": "1.0.0", // Pas forcément nécessaire
  },
  "zetapush": {
      "front": "./front",
      "back": "./server"
  }
}
```

## front/index.html

Code html d'exemple à l'utilisation d'un _Cloud Service_.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>ZetaPush example</title>
</head>

<body>
    <h1>Hello World By ZetaPush</h1>
    
    <button id="btnHelloWorld" onclick="sayHelloWorld()">Say Hello world</button>
    
    <!-- Présent seulement si on utilise les Custom Cloud Services -->
    <input id="inputName" placeholder="Name">
    <button id="btnHelloUser">Say Hello to a specific name</button>

    <hr>

    <div id="result"></div>

    <script src="./index.js"></script>
</body>

</html>
```

## front/index.js

Code JS d'exemple à l'utilisation d'un _Cloud Service_.

```javascript
import { HelloWorldService } from '@zetapush/front';

// Only if we use a custom cloud service
import { HelloWorldCustomService } from '../server/index.js';
const btnSayHelloUser = document.getElementById("btnHelloUser");
const inputName = document.getElementById("inputName");


const btnSayHelloWorld = document.getElementById("btnHelloWorld");
const divResult = document.getElementById("result");

const helloService = new HelloWorldService();

/**
 *  Function called when the user click on the "say hello world" button
 */
async function sayHelloWorld() {
  const resultHello = await helloService.hello();
  divResult.innerHTML += `<p>${resultHello.content} at ${resultHello.timestamp}</p>`
}

/**
 * Function to say Hello to a specific name
 * Only if we use Custom Cloud Service
 */
function sayHelloByName() {
    helloWorldService.helloByName(inputName.value)
        .then((result) => {
            divResultCommands.innerHTML += result;
        })
        .catch((error) => {
            divResultCommands.innerHTML += `Failed to call custom Service : ${error.message}`;
        });
}
```

## server/index.js

Code JS d'exemple d'un _Custom Cloud Service_.

```javascript
export class HelloWorldCustomService {

    /**
     *  Cloud function to say `Hello` to a specific name
     *  This cloud function return promise to be asynchrone
     */
    function helloByName(name) {
        return new Promise((resolve, reject) => {
            resolve(`Hello ${name} !`);
        });
    }
}
```




