# Objectifs

- Un développeur front doit pouvoir initialiser un projet pour utiliser les _cloud services_
- Un développeur full-stack doit pouvoir initialiser un projet pour utiliser les _cloud services_ et créer ses propres _custom cloud services_.
- Un développeur doit pouvoir initialiser un squelette de projet avec la CLI
- Un développeur front doit pouvoir rajouter à son projet existant l'utilisation des cloud services
- Un développeur full-stack doit pouvoir rajouter à son projet existant l'utilisation des cloud services et créer ses propres custom cloud services

Les profils utilisés sont définis dans [le readme](./README.md#profils-identifies).

# Pré-requis

* J'utilise mon éditeur de texte ou IDE préféré.

# <a name="parcours-1"></a> ![Parcours 1](https://img.shields.io/badge/parcours-dev%20front-00d0ff.svg) : Je développe une application front avec ZetaPush sans service custom

## User stories

### <a name="P01-BOOT01"></a> [P01-BOOT01] ETQ dev front je créé une application sans CLI en utilisant mon compte ZetaPush 

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

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

```bash
ZP_DEVELOPER_LOGIN = user@gmail.com
ZP_DEVELOPER_PASSWORD = password
```

- Je remplis `.gitignore` pour éviter d'envoyer mes identifiants de connexion sur GitHub

```bash
.zetarc
```

- Je créé un dossier `front` où j'utilise les _cloud services_ de ZetaPush

- Je remplis `package.json` avec le nom de mon application

```json
{
  "name": "myApp",
  "version": "0.0.1",
  "dependencies": {
  }
}
```

*WHEN*
- J'ajoute la dépendance _@zetapush/core_ avec : `npm install --save @zetapush/core`

*THEN*
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_ avec mon compte `user@gmail.com`

---


### <a name="P01-BOOT02"></a> [P01-BOOT02] ETQ dev front je prépare mon application existante pour utiliser ZetaPush sans utiliser la CLI en utilisant mon compte ZetaPush

![celtia-alpha-3](https://img.shields.io/badge/milestone-celtia--alpha--3-blue.svg)

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- J'ai une application existante nommée **myApp** et je souhaite seulement utiliser les _Cloud Services_ existants
- Mon code est sous l'arborescence suivante :
```
  myApp
    ├── index.html
    └── index.js
```
- Je remplis `.zetarc` avec mes identifiants de connexion à mon compte ZetaPush

```bash
ZP_DEVELOPER_LOGIN = user@gmail.com
ZP_DEVELOPER_PASSWORD = password
```

- Je remplis `.gitignore` pour éviter d'envoyer mes identifiants de connexion sur GitHub

```bash
.zetarc
```

- Je remplis `package.json` avec le nom de mon application et avec le chemin relatif vers la location de mon code front `./`

```json
{
  "name": "myApp",
  "version": "0.0.1",
  "dependencies": {
  },
  "zetapush": {
    "front": "./"
  }
}
```

*WHEN*
- J'ajoute la dépendance _@zetapush/core_ avec : `npm install --save @zetapush/core`

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

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- Je souhaite créer une application nommée **myApp** et seulement utiliser les _Cloud Services_ existants

*WHEN*
- Lorsque je lance la commande : `npm init @zetapush myApp --developer-login user@gmail.com --front`

*THEN*
- Un prompt est lancé pour que je puisse saisir mon mot de passe

```console
$ Please type your developer password of your ZetaPush account :
$ *****
```

- Une application au nom de **myApp** a été ajoutée à mon compte ZetaPush
- Une arborescence fichier a été créée sous la forme :

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

- Mon fichier `.zetarc` est sous la forme :

```bash
ZP_DEVELOPER_LOGIN = user@gmail.com
ZP_DEVELOPER_PASSWORD = password
```

- Mon fichier `.gitignore` est sous la forme :

```bash
.zetarc
```

- Mon fichier `front/index.html` comporte le contenu spécifié [ici](./fichiers/index-front.html)

- Mon fichier `front/index.js` comporte le contenu spécifié [ici](./fichiers/index-front.js)

- Mon fichier `README.md` comporte le contenu spécifié [ici](./fichiers/README.md)

- Mon fichier `package.json` est sous la forme : 

```json
{
  "name": "myApp",
  "version": "0.0.1",
  "dependencies": {
    "@zetapush/core": "1.0.0"
  },
  "zetapush": {
    "front": "./front"
  }
}
```


- La dépendance à _@zetapush/core_ est installée
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_
- J'ai un exemple d'application front avec les fichiers `index.html` et `index.js`
- La sortie de la console est la suivante :

```
Welcome to ZetaPush !

A new application named myApp was added to your account.
Now you can use the Cloud Services in your application. You can see the documentation here : https://console.zetapush.com/documentation

To deploy your application you can use the command "zeta push". You have already an existing use of Cloud Service in front/index.js, test it !
```

---

### <a name="P01-BOOT04"></a> [P01-BOOT04] ETQ dev front je créé une application avec la CLI sans compte existant

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

*GIVEN*
- Je n'ai pas de compte ZetaPush existant
- Je souhaite créer une application nommée **myApp** et seulement utiliser les _Cloud Services_ existants

*WHEN*
- Lorsque je lance la commande : `npm init @zetapush myApp --front`

*THEN*

- Une arborescence fichier a été créée sous la forme :

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

- Mon fichier `.zetarc` est sous la forme (Aucun compte ZetaPush n'est spécifié donc les informations sont vides) :

```bash
ZP_DEVELOPER_LOGIN =
ZP_DEVELOPER_PASSWORD =
```

- Mon fichier `.gitignore` est sous la forme :

```bash
.zetarc
```

- Mon fichier `front/index.html` comporte le contenu spécifié [ici](./fichiers/index-front.html)

- Mon fichier `front/index.js` comporte le contenu spécifié [ici](./fichiers/index-front.js)

- Mon fichier `README.md` comporte le contenu spécifié [ici](./fichiers/README.md)

- Mon fichier `package.json` est sous la forme : 

```json
{
  "name": "myApp",
  "version": "0.0.1",
  "dependencies": {
    "@zetapush/core": "1.0.0"
  },
  "zetapush": {
    "front": "./front"
  }
}
```


- La dépendance à _@zetapush/core_ est installée
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_
- J'ai un exemple d'application front avec les fichiers `index.html` et `index.js`
- La sortie de la console est la suivante :

```
Welcome to ZetaPush !

A new application named myApp was created.
Now you can use the Cloud Services in your application. You can see the documentation here : https://console.zetapush.com/documentation

To deploy your application you can use the command "zeta push". You have already an existing use of Cloud Service in front/index.js, test it !
```

---

# <a name="parcours-2"></a> ![Parcours 2](https://img.shields.io/badge/parcours-dev%20full--stack-00d0ff.svg) Je développe une application front avec ZetaPush avec service custom

## User stories

### <a name="P02-BOOT01"></a> [P02-BOOT01] ETQ dev full-stack je créé une application sans CLI 

![celtia-alpha-1](https://img.shields.io/badge/milestone-celtia--alpha--1-blue.svg)

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- Je souhaite créer une application nommée **myApp** , utiliser les _Cloud Services_ existants et pouvoir créer mes _Custom Cloud Services_
- Je créé l'arborescence suivante (respect des conventions ZetaPush) :
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

```bash
ZP_DEVELOPER_LOGIN = user@gmail.com
ZP_DEVELOPER_PASSWORD = password
```

- Je remplis `.gitignore` pour éviter d'envoyer mes identifiants de connexion sur GitHub

```bash
.zetarc
```

- Je créé un dossier `front/`, c'est ici que mon code front sera stocké
- Je créé un dossier `worker/`, c'est ici que mon code back sera stocké
- Je remplis `package.json` avec le nom de mon application 

```json
{
  "name": "myApp",
  "version": "0.0.1",
  "dependencies": {
  }
}
```


*WHEN*
- J'installe ls dépendances _@zetapush/core_ et _@zetapush/platform_ avec : `npm install --save @zetapush/core` et `npm install --save @zetapush/platform`

*THEN*
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_ et à créer mes _Custom Cloud Services_.



---


### <a name="P02-BOOT02"></a> [P02-BOOT02] ETQ dev full-stack je prépare mon application existante à utiliser ZetaPush sans utiliser la CLI

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- J'ai une application existante nommée **myApp** et je souhaite utiliser les _Cloud Services_ existants et créer mes _Custom Cloud Services_
- Mon application a l'arborescence suivante (respect de la convention) :

```
  myApp
    └── front
        ├── index.html
        └── index.js
```

- Je créé un dossier `worker` pour y stocker mon code back
- Je remplis `.zetarc` avec mes identifiants de connexion à mon compte ZetaPush

```bash
ZP_DEVELOPER_LOGIN = user@gmail.com
ZP_DEVELOPER_PASSWORD = password
```

- Je remplis `.gitignore` pour éviter d'envoyer mes identifiants de connexion sur GitHub

```bash
.zetarc
```

- Je remplis `package.json` avec le nom de mon application 

```json
{
  "name": "myApp",
  "version": "0.0.1",
  "dependencies": {
  }
}
```

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

*WHEN*
- J'installe la dépendance _@zetapush/core_ avec : `npm install --save @zetapush/core`
- J'installe la dépendance _@zetapush/platform_ avec : `npm install --save @zetapush/platform`

*THEN*
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_

---

### <a name="P02-BOOT03"></a> [P02-BOOT03] ETQ dev full-stack je créé une application avec la CLI avec mon compte ZetaPush

![celtia-alpha-1](https://img.shields.io/badge/milestone-celtia--alpha--1-blue.svg)

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- Je souhaite créer une application nommée **myApp** et je souhaite utiliser les _Cloud Services_ existants et créer mes propres _custom cloud services_.

*WHEN*
- Lorsque je lance la commande : `npm init @zetapush myApp --developer-login user@gmail.com`

*THEN*
- Un prompt est lancé pour que je puisse saisir mon mot de passe

```console
$ Please type your developer password of your ZetaPush account :
$ *****
```

- Une application au nom de **myApp** a été ajoutée à mon compte ZetaPush
- Une arborescence fichier a été créée sous la forme :

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

- Mon fichier `.zetarc` est sous la forme :

```bash
ZP_DEVELOPER_LOGIN = user@gmail.com
ZP_DEVELOPER_PASSWORD = password
```

- Mon fichier `.gitignore` est sous la forme :

```bash
.zetarc
```

- Mon fichier `front/index.html` comporte le contenu spécifié [ici](./fichiers/index-fullstack.html)

- Mon fichier `front/index.js` comporte le contenu spécifié [ici](./fichiers/index-fullstack.js)

- Mon fichier `worker/index.js` comporte le contenu spécifié [ici](./fichiers/index-worker.js)

- Mon fichier `README.md` comporte le contenu spécifié [ici](./fichiers/README.md)

- Mon fichier `package.json` est sous la forme : 

```json
{
  "name": "myApp",
  "version": "0.0.1",
  "dependencies": {
    "@zetapush/core": "1.0.0",
    "@zetapush/platform": "1.0.0"
  },
  "zetapush": {
    "front": "./front",
    "worker": "./worker"
  }
}
```


- La dépendance à _@zetapush/core_ est installée
- La dépendance à _@zetapush/platform_ est installée
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_ et créer mes _custom cloud services_.
- J'ai un exemple d'application avec les fichiers `front/index.html`, `front/index.js` et `worker/index.js`
- La sortie de la console est la suivante :

```
Welcome to ZetaPush !

A new application named myApp was added to your account.
Now you can use the Cloud Services in your application. You can see the documentation here : https://console.zetapush.com/documentation

To deploy your application you can use the command "zeta push". You have already an existing use of Cloud Service in front/index.js, test it !
```

---

### <a name="P02-BOOT04"></a> [P02-BOOT04] ETQ dev full-stack je créé une application avec la CLI sans compte existant

![celtia-alpha-1](https://img.shields.io/badge/milestone-celtia--alpha--1-blue.svg)

*GIVEN*
- Je n'ai pas de compte ZetaPush existant
- Je souhaite créer une application nommée **myApp** et je souhaite utiliser les _Cloud Services_ existants et créer mes propres _custom cloud services_.

*WHEN*
- Lorsque je lance la commande : `npm init @zetapush myApp`

*THEN*
- Une arborescence fichier a été créée sous la forme :

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

- Mon fichier `.zetarc` est sous la forme (Aucun compte ZetaPush n'est spécifié donc les informations sont vides) :

```bash
ZP_DEVELOPER_LOGIN =
ZP_DEVELOPER_PASSWORD =
```

- Mon fichier `.gitignore` est sous la forme :

```bash
.zetarc
```

- Mon fichier `front/index.html` comporte le contenu spécifié [ici](./fichiers/index-fullstack.html)

- Mon fichier `front/index.js` comporte le contenu spécifié [ici](./fichiers/index-fullstack.js)

- Mon fichier `worker/index.js` comporte le contenu spécifié [ici](./fichiers/index-worker.js)

- Mon fichier `README.md` comporte le contenu spécifié [ici](./fichiers/README.md)

- Mon fichier `package.json` est sous la forme : 

```json
{
  "name": "myApp",
  "version": "0.0.1",
  "dependencies": {
    "@zetapush/core": "1.0.0",
    "@zetapush/platform": "1.0.0"
  },
  "zetapush": {
    "front": "./front",
    "worker": "./worker"
  }
}
```


- La dépendance à _@zetapush/core_ est installée
- La dépendance à _@zetapush/platform_ est installée
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_ et créer mes _custom cloud services_.
- J'ai un exemple d'application avec les fichiers `front/index.html`, `front/index.js` et `worker/index.js`
- La sortie de la console est la suivante :

```
Welcome to ZetaPush !

A new application named myApp was created.
Now you can use the Cloud Services in your application. You can see the documentation here : https://console.zetapush.com/documentation

To deploy your application you can use the command "zeta push". You have already an existing use of Cloud Service in front/index.js, test it !
```

---

### <a name="P02-BOOT05"></a> [P02-BOOT05] ETQ dev full-stack je créé une application avec la CLI avec une arborescence spécifiée en utilisant mon compte ZetaPush

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- Je souhaite créer une application nommée **myApp** et je souhaite utiliser les _Cloud Services_ existants et créer mes propres _custom cloud services_.

*WHEN*
- Lorsque je lance la commande : `npm init @zetapush myApp --developer-login user@gmail.com --front=. --worker=./worker`

*THEN*
- Un prompt est lancé pour que je puisse saisir mon mot de passe (comme j'utilise un compte que je spécifie en paramètre avec `--developer-login`)

```console
$ Please type your developer password of your ZetaPush account :
$ *****
```

- Une application au nom de **myApp** a été ajoutée à mon compte ZetaPush
- Une arborescence fichier a été créée sous la forme :

  ```
  .
  ├── .zetarc
  ├── .gitignore
  ├── index.html
  ├── index.js
  ├── worker
  │   └── index.js
  ├── README.md
  └── package.json
  ```

- Mon fichier `.zetarc` est sous la forme :

```bash
ZP_DEVELOPER_LOGIN = user@gmail.com
ZP_DEVELOPER_PASSWORD = password
```

- Mon fichier `.gitignore` est sous la forme :

```bash
.zetarc
```

- Mon fichier `index.html` comporte le contenu spécifié [ici](./fichiers/index-fullstack.html)

- Mon fichier `index.js` comporte le contenu spécifié [ici](./fichiers/index-fullstack.js)

- Mon fichier `worker/index.js` comporte le contenu spécifié [ici](./fichiers/index-worker.js)

- Mon fichier `README.md` comporte le contenu spécifié [ici](./fichiers/README.md)

- Mon fichier `package.json` est sous la forme : 

```json
{
  "name": "myApp",
  "version": "0.0.1",
  "dependencies": {
    "@zetapush/core": "1.0.0",
    "@zetapush/platform": "1.0.0"
  },
  "zetapush": {
    "front": ".",
    "worker": "./worker"
  }
}
```


- La dépendance à _@zetapush/core_ est installée
- La dépendance à _@zetapush/platform_ est installée
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_ et créer mes _custom cloud services_.
- J'ai un exemple d'application avec les fichiers `./index.html`, `./index.js` et `worker/index.js`
- La sortie de la console est la suivante :

```
Welcome to ZetaPush !

A new application named myApp was added to your account.
Now you can use the Cloud Services in your application. You can see the documentation here : https://console.zetapush.com/documentation

To deploy your application you can use the command "zeta push". You have already an existing use of Cloud Service in front/index.js, test it !
```

---


### <a name="P02-BOOT06"></a> [P02-BOOT06] ETQ dev full-stack je prépare monapplication existante pour utiliser ZetaPush en utilisant la CLI

![celtia-alpha-1](https://img.shields.io/badge/milestone-celtia--alpha--1-blue.svg)

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- J'ai une application existante nommée **myApp** et je souhaite seulement utiliser les _Cloud Services_ existants et créer mes propres _Custom Cloud Services_.
- Mon code est sous l'arborescence suivante (respecte la convention ZetaPush) :
```
  myApp
  └── front
      └── index.html
      └── index.js
```

*WHEN*
- Lorsque je lance la commande `npm init @zetapush --developer-login user@gmail.com` au sein de mon dossier `myApp`

*THEN*
- La CLI détecte que le dossier n'est pas vide, et me demande si je veux continuer pour créer les fichiers suivants :

```console
$ Do you want to create/replace this files in this place ? (Y/n)
  .zetarc
  .gitignore
  README.md
  package.json
  worker/index.js
$ 
```

- Un prompt est lancé pour que je puisse saisir mon mot de passe de mon compte ZetaPush

```console
$ Please type your developer password of your ZetaPush account :
$ *****
```

- J'ai l'arborescence suivante qui est créée :
  ```
  myApp
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

- Mon fichier `.zetarc` est sous la forme :

```bash
ZP_DEVELOPER_LOGIN = user@gmail.com
ZP_DEVELOPER_PASSWORD = password
```

- Mon fichier `.gitignore` est sous la forme :

```bash
.zetarc
```

- Mon fichier `README.md` comporte le contenu spécifié [ici](./fichiers/README.md)

- Mon fichier `package.json` est sous la forme : 

```json
{
  "name": "myApp",
  "version": "0.0.1",
  "dependencies": {
    "@zetapush/core": "1.0.0"
  },
  "zetapush": {
    "front": "./front",
    "worker": "./worker"
  }
}
```

- La dépendance à _@zetapush/core_ est installée
- La dépendance à _@zetapush/platform_ est installée
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_ et créer des _Custom Cloud Services_.
- La sortie de la console est la suivante :

```
Welcome to ZetaPush !

A new application named myApp was added to your account.
Now you can use Cloud Services in your application. You can see the documentation here : https://console.zetapush.com/documentation

To deploy your application you can use the command "zeta push".
```

### <a name="P02-BOOT07"></a> [P02-BOOT07] ETQ dev full-stack je prépare mon application existante pour utiliser ZetaPush en utilisation la CLI avec mon compte ZetaPush avec une arborescence custom

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- J'ai une application existante nommée **myApp** et je souhaite seulement utiliser les _Cloud Services_ existants et créer des _Custom Cloud Services_
- Mon code est sous l'arborescence suivante (non respect de la convention ZetaPush) :
```
  myApp
  ├── index.html
  └── index.js
```

*WHEN*
- Lorsque je lance la commande `npm init @zetapush --developer-login user@gmail.com --front=. --worker=./worker` au sein de mon dossier `myApp`

*THEN*
- La CLI détecte que le dossier n'est pas vide, et me demande si je veux continuer pour créer les fichiers suivants :

```console
$ Do you want to create/update this files in this place ? (Y/n)
  .zetarc
  .gitignore
  README.md
  package.json
  worker/index.js
$ 
```

- Un prompt est lancé pour que je puisse saisir mon mot de passe de mon compte ZetaPush

```console
$ Please type your developer password of your ZetaPush account :
$ *****
```

- J'ai l'arborescence suivante qui est créée :
  ```
  myApp
  ├── .zetarc
  ├── .gitignore
  ├── index.html
  ├── index.js
  ├── README.md
  ├── worker
  │   └── index.js
  └── package.json
  ```

- Mon fichier `.zetarc` est sous la forme :

```bash
ZP_DEVELOPER_LOGIN = user@gmail.com
ZP_DEVELOPER_PASSWORD = password
```

- Mon fichier `.gitignore` est sous la forme :

```bash
.zetarc
```

- Mon fichier `README.md` comporte le contenu spécifié [ici](./fichiers/README.md)

- Mon fichier `package.json` est sous la forme : 

```json
{
  "name": "myApp",
  "version": "0.0.1",
  "dependencies": {
    "@zetapush/core": "1.0.0",
    "@zetapush/platform": "1.0.0"
  },
  "zetapush": {
    "front": ".",
    "worker": "./worker"
  }
}
```

- Les dépendances _@zetapush/core_ et _@zetapush/platform_ sont installées
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_ et créer mes _Custom Cloud Services_.
- La sortie de la console est la suivante :

```
Welcome to ZetaPush !

A new application named myApp was added to your account.
Now you can use Cloud Services in your application. You can see the documentation here : https://console.zetapush.com/documentation

To deploy your application you can use the command "zeta push".
```

---

### <a name="P02-BOOT08"></a> [P02-BOOT08] ETQ dev full-stack je créé une application sans CLI et sans compte ZetaPush

![celtia-alpha-1](https://img.shields.io/badge/milestone-celtia--alpha--1-blue.svg)

*GIVEN*
- Je n'ai pas de compte ZetaPush existant
- Je souhaite créer une application nommée **myApp** , utiliser les _Cloud Services_ existants et pouvoir créer mes _Custom Cloud Services_
- Je créé l'arborescence suivante (respect des conventions ZetaPush) :
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


- Je créé un dossier `front/`, c'est ici que mon code front sera stocké
- Je créé un dossier `worker/`, c'est ici que mon code back sera stocké
- Je remplis `package.json` avec le nom de mon application

```json
{
  "name": "myApp",
  "version": "0.0.1",
  "dependencies": {
  }
}
```


*WHEN*
- j'installe la dépendance _@zetapush/core_ avec : `npm install --save @zetapush/core` et j'installe la dépendance _@zetapush/platform_ avec : `npm install --save @zetapush/platform`

*THEN*
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_ et à créer mes _Custom Cloud Services_.

---

### <a name="P02-BOOT09"></a> [P02-BOOT09] ETQ dev full-stack je créé une application sans CLI avec une arborescence custom

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

*GIVEN*
- J'ai un compte ZetaPush existant (user : user@gmail.com / password : password)
- Je souhaite créer une application nommée **myApp** , utiliser les _Cloud Services_ existants et pouvoir créer mes _Custom Cloud Services_
- Je créé l'arborescence suivante (non respect des conventions ZetaPush) :
  ```
  .
  ├── .zetarc
  ├── .gitignore
  ├── index.html
  ├── index.js
  ├── worker
  │   └── index.js
  └── package.json
  ```
- Je remplis `.zetarc` avec mes identifiants de connexion à mon compte ZetaPush

```bash
ZP_DEVELOPER_LOGIN = user@gmail.com
ZP_DEVELOPER_PASSWORD = password
```

- Je remplis `.gitignore` pour éviter d'envoyer mes identifiants de connexion sur GitHub

```bash
.zetarc
```
- Je créé mes fichiers `index.html` et `index.js` pour mon code front
- Je créé un dossier `worker/`, c'est ici que mon code back sera stocké
- Je remplis `package.json` avec le nom de mon application et les paths vers les dossiers du code front et du code back

```json
{
  "name": "myApp",
  "version": "0.0.1",
  "dependencies": {
  },
  "zetapush": {
    "front": "./",
    "worker": "./worker"
  }
}
```


*WHEN*
- J'installe la dépendance _@zetapush/core_ avec : `npm install --save @zetapush/core` et j'installe la dépendance _@zetapush/platform_ avec : `npm install --save @zetapush/platform`

*THEN*
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_ et à créer mes _Custom Cloud Services_.

---

### <a name="P02-BOOT10"></a> [P02-BOOT10] ETQ dev full-stack je prépare mon application existante pour utiliser ZetaPush en utilisant la CLI sans compte ZetaPush


*GIVEN*
- Je n'ai pas de compte ZetaPush existant
- J'ai une application existante nommée **myApp** et je souhaite seulement utiliser les _Cloud Services_ existants et créer mes propres _Custom Cloud Services_.
- Mon code est sous l'arborescence suivante (respecte la convention ZetaPush) :
```
  myApp
  └── front
      └── index.html
      └── index.js
```

*WHEN*
- Lorsque je lance la commande `npm init @zetapush` au sein de mon dossier `myApp`

*THEN*
- La CLI détecte que le dossier n'est pas vide, et me demande si je veux continuer pour créer les fichiers suivants :

```console
$ Do you want to create/replace this files in this place ? (Y/n)
  .zetarc
  .gitignore
  README.md
  package.json
  worker/index.js
$ 
```

- J'ai l'arborescence suivante qui est créée :
  ```
  myApp
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

- Mon fichier `.zetarc` est sous la forme (Aucun compte ZetaPush n'est spécifié donc les informations sont vides) :

```bash
ZP_DEVELOPER_LOGIN =
ZP_DEVELOPER_PASSWORD =
```

- Mon fichier `.gitignore` est sous la forme :

```bash
.zetarc
```

- Mon fichier `README.md` comporte le contenu spécifié [ici](./fichiers/README.md)

- Mon fichier `package.json` est sous la forme : 

```json
{
  "name": "myApp",
  "version": "0.0.1",
  "dependencies": {
    "@zetapush/core": "1.0.0"
  },
  "zetapush": {
    "front": "./front",
    "worker": "./worker"
  }
}
```

- La dépendance à _@zetapush/core_ est installée
- La dépendance à _@zetapush/platform_ est installée
- Mon application est prête et je suis prêt à utiliser les _Cloud Services_ et créer des _Custom Cloud Services_.
- La sortie de la console est la suivante :

```
Welcome to ZetaPush !

A new application named myApp was created.
Now you can use Cloud Services in your application. You can see the documentation here : https://console.zetapush.com/documentation

To deploy your application you can use the command "zeta push".
```
