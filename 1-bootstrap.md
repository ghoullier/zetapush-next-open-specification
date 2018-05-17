# Objectifs

- Un développeur front doit pouvoir utiliser les services ZetaPush dans son code front
- Un développeur full-stack doit pouvoir utiliser les services ZetaPush dans son code front et coder son propre métier pour simplifier le développement de son/ses front(s)
- Un développeur doit pouvoir initialiser un squelette de projet avec la CLI

Les profils utilisés sont définis dans [le readme](./README.md#profils-identifies).

Pour chaque User Story, nous définissons seulement les fichiers qui sont créés. Pour voir le contenu de chacun, voir la rubrique [fichiers créés](#fichiers).

# Pré-requis

* J'utilise mon éditeur de texte ou IDE préféré.


# <a name="parcours-1"></a> ![Parcours 1](https://img.shields.io/badge/parcours-dev%20front-00d0ff.svg) : Je développe une application front avec ZetaPush sans service custom

## User stories

### <a name="P01-BOOT01"></a> [P01-BOOT01] ETQ dev front je créé une application sans CLI en utilisant mon compte ZetaPush 

![celtia-alpha-1](https://img.shields.io/badge/milestone-celtia--alpha--1-blue.svg)

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- Je souhaite créer une application nommée **myApp** et seulement utiliser les _Cloud Services_ fournis pas ZetaPush
- Je créé l'arboresence suivante (en utilisant la convention ZetaPush) :
  ```
  myApp
  ├── .zetarc
  ├── .gitignore
  ├── front
  │   ├── index.html
  │   └── index.js
  └── package.json
  ```
- Je remplis `.zetarc` avec mes identifiants de connexion à mon compte ZetaPush
- Je remplis `.gitignore` pour éviter d'envoyer mes identifiants de connexion sur GitHub
- Je remplis `package.json` avec le nom de mon application
- J'installe la dépendance _@zetapush/front_ avec : `npm install --save @zetapush/front`

*WHEN*
- Lorsque la création des fichiers et l'installation des dépendances est finie

*THEN*
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_ avec mon compte `user@gmail.com`


---


### <a name="P01-BOOT02"></a> [P01-BOOT02] ETQ dev front j'utilise les _Cloud Services_ dans mon application existante sans CLI en utilisant mon compte ZetaPush 

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- J'ai une application existante nommée **myApp** et je souhaite seulement utiliser les _Cloud Services_ existants
- Mon code est sous l'arboresence suivante :
```
  myApp
    ├── index.html
    └── index.js
```
- Je remplis `.zetarc` avec mes identifiants de connexion à mon compte ZetaPush
- Je remplis `.gitignore` pour éviter d'envoyer mes identifiants de connexion sur GitHub
- Je remplis `package.json` avec le nom de mon application
- Je remplis `package.json` avec le chemin relatif vers la location de mon code front (`./`). 
- J'installe la dépendance _@zetapush/front_ avec : `npm install --save @zetapush/front`

*WHEN*
- Lorsque la création des fichiers et l'installation des dépendances est finie

*THEN*
- J'ai l'arborescence suivante qui est créée :
  ```
  myApp
  ├── .zetarc
  ├── .gitignore
  ├── index.html
  ├── index.js
  └── package.json
  ```
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_


---


### <a name="P01-BOOT03"></a> [P01-BOOT03] ETQ dev front je créé une application avec la CLI en utilisant mon compte ZetaPush

![celtia-beta-1](https://img.shields.io/badge/milestone-celtia--beta--1-blue.svg)

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- Je souhaite créer une application nommée **myApp** et seulement utiliser les _Cloud Services_ existants
- J'utilise la convention ZetaPush

*WHEN*
- Lorsque je lance la commande : `npm init myApp --login user@gmail.com --front`

*THEN*
- Un prompt est lancé pour que je puisse saisir mon mot de passe
- Une application au nom de **myApp** a été ajoutée à mon compte ZetaPush
- Une arborescence fichier à été créée sous la forme :

  ```
  .
  ├── .zetarc
  ├── .gitignore
  ├── front
  │   ├── index.html
  │   └── index.js
  ├── README.md
  └── package.json
  ```
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_
- J'ai un README.md avec les informations m'indiquant comment démarrer (utilisation de la CLI, les bonnes pratiques ZetaPush, les liens vers la documentation)
- La sortie de la console est la suivante :

```
Welcome to ZetaPush !

A new application named myApp was added to your account.
Now you can use Cloud Services in your application. You can see the documentation here : https://console.zetapush.com/documentation

To deploy your application you can use the command zeta push. You have already an existing use of Cloud Service in front/index.js, test it !
```


---


### <a name="P01-BOOT04"></a> [P01-BOOT04] ETQ dev front je créé une application avec la CLI sans compte existant

![celtia-alpha-1](https://img.shields.io/badge/milestone-celtia--alpha--1-blue.svg)

*GIVEN*
- Je n'ai pas de compte ZetaPush existant
- Je souhaite créer une application nommée **myApp** et seulement utiliser les _Cloud Services_ existants

*WHEN*
- Lorsque je lance la commande : `npm init myApp --front`

*THEN*
- Un _captcha_ est affiché pour vérifier que je ne suis pas un robot
- J'ai un prompt qui me demande de résoudre ce captcha pour créer un compte

```console
   #                #####               #####  
  ##        #      #     #             #     # 
 # #        #            #    #####          # 
   #      #####     #####                 ###  
   #        #      #          #####       #    
   #        #      #                           
 #####             #######                #    

Veuillez résoudre cette opération pour créer votre compte sur la plateforme ZetaPush : 

$ Réponse : 
```
- Un compte temporaire sur la plateforme ZetaPush a été créé
- Une application au nom de **myApp** a été ajoutée à ce compte
- Une arborescence fichier à été créée sous la forme :

  ```
  myApp
  ├── .zetarc
  ├── .gitignore
  ├── front
  │   ├── index.html
  │   └── index.js
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

TODO: le captcha ne devrait pas être demandé à l'init de projet, c'est trop intrusif !

---


### <a name="P01-BOOT05"></a> [P01-BOOT05] ETQ dev front j'utilise les _Cloud Services_ dans mon application existante avec la CLI en utilisant mon compte ZetaPush

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- J'ai une application existante nommée **myApp** et je souhaite seulement utiliser les _Cloud Services_ existants
- Mon code est sous l'arborescence suivante (respecte la convention ZetaPush) :
```
  myApp
  └── front
      └── index.html
      └── index.js
```

*WHEN*
- Lorsque je lance la commande `npm init --login user@gmail.com` au sein de mon dossier `myApp`

*THEN*
- La CLI détecte que le dossier n'est pas vide, et me demande si je veux continuer pour créer les fichiers suivants :
```console
.zetarc
.gitignore
README.md
package.json
```
- Un prompt est lancé pour que je puisse saisir mon mot de passe (`password`)
- J'ai l'arborescence suivante qui est créée :
  ```
  myApp
  ├── .zetarc
  ├── .gitignore
  ├── front
  │   ├── index.html
  │   └── index.js
  ├── README.md
  └── package.json
  ```
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_
- J'ai un README.md avec les informations m'indiquant comment démarrer (utilisation de la CLI, les bonnes pratiques ZetaPush, les liens vers la documentation)
- La sortie de la console est la suivante :

```
Welcome to ZetaPush !

A new application named myApp was added to your account.
Now you can use Cloud Services in your application. You can see the documentation here : https://console.zetapush.com/documentation

To deploy your application you can use the command zeta push.
```


### <a name="P01-BOOT06"></a> [P01-BOOT06] ETQ dev front j'utilise les _Cloud Services_ dans mon application existante et une arborescence custom avec la CLI en utilisant mon compte ZetaPush 

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)


*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- J'ai une application existante nommée **myApp** et je souhaite seulement utiliser les _Cloud Services_ existants
- Mon code est sous l'arborescence suivante :
```
  myApp
    ├── index.html
    └── index.js
```
- Je spécifie où se trouve le code front avec l'argument `--front=.`

*WHEN*
- Lorsque je lance la commande `npm init --front=. --login user@gmail.com` au sein de mon dossier `myApp`

*THEN*
- La CLI détecte que le dossier n'est pas vide, et me demande si je veux continuer pour créer les fichiers suivants :
```console
.zetarc
.gitignore
README.md
package.json
```
- Un prompt est lancé pour que je puisse saisir mon mot de passe (`password`)
- J'ai l'arborescence suivante qui est créée :
  ```
  myApp
  ├── .zetarc
  ├── .gitignore
  ├── index.html
  ├── index.js
  ├── README.md
  └── package.json
  ```
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_
- J'ai un README.md avec les informations m'indiquant comment démarrer (utilisation de la CLI, les bonnes pratiques ZetaPush, les liens vers la documentation)
- La sortie de la console est la suivante :

```
Welcome to ZetaPush !

A new application named myApp was added to your account.
Now you can use Cloud Services in your application. You can see the documentation here : https://console.zetapush.com/documentation

To deploy your application you can use the command zeta push.
```


# <a name="parcours-2"></a> ![Parcours 2](https://img.shields.io/badge/parcours-dev%20full--stack-00d0ff.svg) Je développe une application front avec ZetaPush avec service custom

## User stories

### <a name="P02-BOOT01"></a> [P02-BOOT01] ETQ dev full-stack je créé une application sans CLI 

![celtia-alpha-1](https://img.shields.io/badge/milestone-celtia--alpha--1-blue.svg)

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- Je souhaite créer une application nommée **myApp** , utiliser les _Cloud Services_ existants et pouvoir créer mes _Custom Cloud Services_
- Je créé l'arboresence suivante (en suivant les conventions ZetaPush) :
  ```
  .
  ├── .zetarc
  ├── .gitignore
  ├── front
  │   ├── index.html
  │   └── index.js
  ├── worker
  │   └── index.js
  └── package.json
  ```
- Je remplis `.zetarc` avec mes identifiants de connexion à mon compte ZetaPush
- Je remplis `.gitignore` pour éviter d'envoyer mes identifiants de connexion sur GitHub
- Je créé un dossier `front/`, c'est ici que mon code front sera stocké
- Je créé un dossier `worker/`, c'est ici que mon code back sera stocké
- Je remplis `package.json` avec le nom de mon application
- J'installe la dépendance _@zetapush/front_ avec : `npm install --save @zetapush/front`
- J'installe la dépendance _@zetapush/server_ avec : `npm install --save @zetapush/server`

*WHEN*
- Lorsque la création des fichiers et l'installation des dépendances est finie

*THEN*
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_ et à créer mes _Custom Cloud Services_.



---


### <a name="P02-BOOT02"></a> [P02-BOOT02] ETQ dev full-stack j'ajoute  des _Cloud Services_ et je créé  des _Custom Cloud Services_ au sein d'une application existante 

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- J'ai une application existante nommée **myApp** et je souhaite utiliser les _Cloud Services_ existants et créer mes _Custom Cloud Services_
- Je créé un dossier `worker` pour y stocker mon code back
- Je remplis `.zetarc` avec mes identifiants de connexion à mon compte ZetaPush
- Je remplis `.gitignore` pour éviter d'envoyer mes identifiants de connexion sur GitHub
- Je remplis un `package.json` avec le nom de mon application
- Je remplis `package.json` avec les chemins relatifs vers la location de mon code front et de mon code back. 
- Mon code est sous l'arboresence suivante (en respectant la convention ZetaPush) :
  ```
  myApp
  ├── .zetarc
  ├── .gitignore
  ├── front
  │   ├── index.html
  │   └── index.js
  ├── worker
  │   └── index.js
  └── package.json
  ```
- J'installe la dépendance _@zetapush/front_ avec : `npm install --save @zetapush/front`
- J'installe la dépendance _@zetapush/server_ avec : `npm install --save @zetapush/server`

*WHEN*
- Lorsque la création des fichiers et l'installation des dépendances est finie

*THEN*
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_



---


### <a name="P02-BOOT03"></a> [P02-BOOT03] ETQ dev full-stack je créé une application avec la CLI 

![celtia-alpha-1](https://img.shields.io/badge/milestone-celtia--alpha--1-blue.svg)

*GIVEN*
- J'ai un compte ZetaPush existant avec user@gmail.com / password comme couple login/password
- Je souhaite créer une application avec une partie front et une partie back

*WHEN*
- Lorsque je lance la commande : `npm init myApp --login user@gmail.com`

*THEN*
- Un prompt est lancé pour que je puisse saisir mon mot de passe
- Une application au nom de **myApp** a été ajoutée à mon compte ZetaPush
- Une arborescence fichier à été créée sous la forme :

  ```
  .
  ├── .zetarc
  ├── .gitignore
  ├── front
  │   ├── index.html
  │   └── index.js
  ├── worker
  │   └── index.js
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


---


### <a name="P02-BOOT04"></a> [P02-BOOT04] ETQ dev full-stack je créé une application avec la CLI sans compte existant

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

*GIVEN*
- Je n'ai pas de compte ZetaPush
- Je souhaite créer une application avec une partie front et une partie back

*WHEN*
- Lorsque je lance la commande : `npm init myApp`

*THEN*
- Une application au nom de **myApp**
- Une arborescence fichier à été créée sous la forme :

  ```
  myApp
  ├── .zetarc
  ├── .gitignore
  ├── front
  │   ├── index.html
  │   ├── index.js
  │   └── style.css
  ├── worker
  │   └── index.js
  ├── README.md
  └── package.json
  ```
- J'ai un README.md avec les informations m'indiquant comment démarrer (utilisation de la CLI, les bonnes pratiques ZetaPush, les liens vers la documentation)
- La console m'affiche toutes les informations précédentes de la manière suivante :

```
Welcome to ZetaPush !

Now you can use Cloud Services in your application. You can see the documentation here : https://console.zetapush.com/documentation. You have already an existing use of Cloud Service in front/index.js, test it !
```


---


### <a name="P02-BOOT05"></a> [P02-BOOT05] ETQ dev full-stack je créé une application avec la CLI et une arborescence spécifiée en utilisant mon compte ZetaPush

*GIVEN*
- J'ai un compte ZetaPush existant avec user@gmail.com / password comme couple login/password
- Je souhaite créer une application avec une partie front et une partie back
- J'utilise la convention ZetaPush

*WHEN*
- Lorsque je lance la commande : `npm init myApp --login user@gmail.com`

*THEN*
- Un prompt est lancé pour que je puisse saisir mon mot de passe
- Une application au nom de **myApp** a été ajoutée à mon compte ZetaPush
- Une arborescence fichier à été créée sous la forme :

  ```
  myApp
  ├── .zetarc
  ├── .gitignore
  ├── front
  │   ├── index.html
  │   ├── index.js
  │   └── style.css
  ├── worker
  │   └── index.js
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

---


### <a name="P02-BOOT06"></a> [P02-BOOT06] ETQ dev full-stack j'ajoute des _Custom Cloud Services_ au sein d'une application existante avec la CLI 

![celtia-alpha-1](https://img.shields.io/badge/milestone-celtia--alpha--1-blue.svg)


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
- Lorsque de lance la commande `npm init myApp --login user@gmail.com --front=. --worker`


*THEN*
- La CLI détecte que le dossier n'est pas vide, et me demande si je veux continuer comme les fichiers suivants vont être créés :
```console
.zetarc
.gitignore
README.md
package.json
```
- Un prompt est lancé pour que je puisse saisir mon mot de passe
- J'ai l'arborescence suivante qui est créée :
  ```
  myApp
  ├── .zetarc
  ├── .gitignore
  ├── index.html
  ├── index.js
  ├── worker
  │   └── index.js
  └── package.json
  ```
- Les dépendances _@zetapush/front_ et _@zetapush/server_ ont été installées
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_


# <a name="fichiers"></a> Fichiers créés / à créer

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
      "front": "./front", // Chemin relatif vers le code front
      "worker": "./worker" // Chemin relatif vers le code back
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
import { HelloWorldCustomService } from '../worker/index.js';
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
    const result = helloWorldService.helloByName(inputName.value);
    divResultCommands.innerHTML += result;
}
```

## worker/index.js

Code JS d'exemple d'un _Custom Cloud Service_.

```javascript
export class HelloWorldCustomService {

    /**
     *  Cloud function to say `Hello` to a specific name
     *  This cloud function return promise to be asynchrone
     */
    function helloByName(name) {
        return `Hello ${name} !`;
    };
}
```




