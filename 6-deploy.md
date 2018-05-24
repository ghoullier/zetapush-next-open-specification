# Objectifs

- Un développeur front doit pouvoir développer son front en utilisant les services ZetaPush et sans être obligé de développer de code backend spécifique. Il doit pouvoir déployer son front sur ZetaPush.
- Un développeur full-stack ayant un front et des services custom doit pouvoir déployer son application sur ZetaPush (front et backend custom)


# Pré-requis

# <a name="parcours-1"></a> ![Parcours 1](https://img.shields.io/badge/parcours-dev%20front-00d0ff.svg) : Je développe une application front avec ZetaPush sans service custom

## Vue d'ensemble

![Déploiement en production front seulement](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/dev-front-deploiement-prod-front-only.html)

## User stories

### <a name="P01-DEPLOY01"></a> [P01-DEPLOY01] ETQ dev front je déploie mon application en production 

![celtia-alpha-1](https://img.shields.io/badge/milestone-celtia--alpha--1-blue.svg)

*GIVEN*
  - J'ai le nom de l'application dans le fichier `package.json`
  - Le nom de mon application est _avengers chat web_
  - J'ai un compte sur ZetaPush (login=jeni@yopmail.com, password=zp-password)
  - Je suis au sein d'un dossier contenant un fichier `.zetarc` contenant les informations de mon compte ZetaPush
  - J'utilise l'arborescence par défaut :

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

*WHEN*
  - J'exécute la commande : ```zeta push --front```

*THEN*
  - Le contenu du dossier `front` est envoyé sur ZetaPush
  - Je vois l'état d'avancement du déploiement global :
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      | Publishing web application            ██████░░░░░░
    ```
  - Je sais lorsque mon application est prête à être utilisée :
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      ✓ Web application published

    Your web application is ready and available at https://avengers-chat-web.prod.my-first-app.jeni.zetapush-apps.com
    ```
  - Mon front est disponible sur le site https://avengers-chat-web.prod.my-first-app.jeni.zetapush-apps.com


# <a name="parcours-2"></a> ![Parcours 2](https://img.shields.io/badge/parcours-dev%20full--stack-00d0ff.svg) Je développe une application avec ZetaPush et des services custom

## Vue d'ensemble

J'ai développé sur ma machine avec mon propre NodeJS qui interagit avec ZetaPush.

![Développement local](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/dev-front-processus-developpement.html)


Mon application est prête à partir en production. Je la déploie depuis mon poste.

![Déploiement en production](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/dev-full-stack-deploiement-prod-server-only.html)


## User stories

### <a name="P02-DEPLOY01"></a> [P02-DEPLOY01] ETQ dev full-stack je déploie mes services custom en production 

![celtia-alpha-1](https://img.shields.io/badge/milestone-celtia--alpha--1-blue.svg)

*GIVEN*
  - Je suis au sein d'un dossier contenant un fichier `.zetarc`
  - J'ai le nom de l'application dans le fichier `package.json`
  - J'ai un compte sur ZetaPush (login=jeni@yopmail.com, password=zp-password)
  - J'ai développé un service custom avec les fonctions suivantes :
    - ```createGame(player1, player2)```
    - ```gameAction(player, name, args)```
    - ```isFinished()```
    - ```getWinner()```
    - ```endGame()```
  - ZetaPush me permet de répliquer 3 fois mon worker en production et je n'ai rien configuré
  - J'utilise l'arborescence par défaut :

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

*WHEN*
- J'exécute la commande : ```zeta push --worker```

*THEN*
  - Mes _custom cloud services_ présents dans le dossier `worker` sont envoyés sur ZetaPush
  - Je vois l'état d'avancement du déploiement global
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      | Publishing custom services on worker instance 1   ██████░░░░░░
      - Publishing custom services on worker instance 2   ████████░░░░
      / Publishing custom services on worker instance 3   ██░░░░░░░░░░
    ```
  - Je sais lorsque mon application est prête à être utilisée
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      ✓ Custom services published on worker instance 1
      ✓ Custom services published on worker instance 2
      ✓ Custom services published on worker instance 3

    Your custom services are ready and accessible through ZetaPush
    ```
  - Je peux utiliser mon frontend local pour interagir avec mon service custom déployé en production
  - Je peux appeler la fonction `createGame` de mon service custom directement depuis mon frontend via le SDK JS ZetaPush avec les paramètres suivants :
    - ```player1 = {"name": "Georgesdelajungle"}```
    - ```player2 = {"name": "Aladdin"}```
  - ZetaPush gère le load-balancing entre les 3 instances de mon worker (voir autres US)
  - Je peux visualiser les logs applicatifs de mon service custom (voir autres US)
  - Je peux consulter la santé de mon worker (voir autres US)


---

### <a name="P02-DEPLOY02"></a> [P02-DEPLOY02] ETQ dev full-stack je déploie mon application (front et _custom cloud services_) en production 

![celtia-alpha-1](https://img.shields.io/badge/milestone-celtia--alpha--1-blue.svg)

*GIVEN*
  - Je suis au sein d'un dossier contenant un fichier `.zetarc`
  - J'ai le nom de l'application dans le fichier `package.json`
  - J'ai un compte sur ZetaPush (login=jeni@yopmail.com, password=zp-password)
  - J'ai développé un service custom avec les fonctions suivantes :
    - ```createGame(player1, player2)```
    - ```gameAction(player, name, args)```
    - ```isFinished()```
    - ```getWinner()```
    - ```endGame()```
  - ZetaPush me permet de répliquer 3 fois mon worker en production et je n'ai rien configuré
  - J'utilise l'arborescence par défaut :

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

*WHEN*
  - J'exécute la commande : ```zeta push```

*THEN*
  - Mes _custom cloud services_ (définis dans le dossier `worker`) sont envoyés sur ZetaPush
  - Je vois l'état d'avancement du déploiement global
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      | Publishing web application                        ██████░░░░░░
      / Publishing custom services on worker instance 1   ██████░░░░░░
      - Publishing custom services on worker instance 2   ████████░░░░
      \ Publishing custom services on worker instance 3   ██░░░░░░░░░░
    ```
  - Je sais lorsque mon application est prête à être utilisée
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      ✓ Web application published
      ✓ Custom services published on worker instance 1
      ✓ Custom services published on worker instance 2
      ✓ Custom services published on worker instance 3

    Your application is ready:
    - Your web application is ready and available at https://avengers-chat-web.prod.my-first-app.jeni.zetapush-apps.com
    - Your custom services are ready and accessible through ZetaPush
    ```
  - Mon frontend (dossier `front`) est envoyé sur ZetaPush
  - Mon front est disponible sur le site `avengers-chat-web.prod.my-first-app.jeni.zetapush-apps.com`
  - Mon frontend de production déployé utilise les services custom déployés
  - ZetaPush gère le load-balancing entre les 3 instances de mon worker (voir autres US)
  - Je peux visualiser les logs applicatifs de mon service custom (voir autres US)
  - Je peux consulter la santé de mon worker (voir autres US)


---

### <a name="P02-DEPLOY03"></a> [P02-DEPLOY03] ETQ dev je suis aidé lorsque mon application (front et service custom) n'a pas pu être déployé en production

![celtia-alpha-1](https://img.shields.io/badge/milestone-celtia--alpha--1-blue.svg)

*GIVEN*
  - J'ai exécuté la commande : ```zeta push```
  
*WHEN*
  - Je vois dans ma console que le déploiement a échoué

*THEN*
  - Je sais que mon application n'a pas pu être déployée
  - J'ai suffisamment d'information pour savoir ce qui n'a pas fonctionné
  - La précédente version déployée n'est pas écrasée ou corrompue (que ce soit front ou back)
  - J'ai un retour dans mon terminal du type :
  
    ```
    $ zeta push
    
    Your application couldn't be deployed. The previous version is still running.
    The returned error is the following :

    code : NET-01
    message : No network connection available
    ```
  
  > Ensemble des messages erreurs potentielles
  >
  > | Cause | Code | Message |
  > |:---:|:---:|:---:|
  > | Le poste du développeur n'a pas accès à internet | NET-01 | No network connection available |
  > | Le poste du développeur n'arrive pas à accèder à la plateforme ZetaPush | NET-02 | Failed to access to the ZetaPush platform (Network issue) |
  > | Aucun login développeur n'a été trouvé (variable d'environnement / package.json / paramètre de la commande) | ACCOUNT-01 | No developer login found |
  > | Aucun mot de passe développeur n'a été trouvé (variable d'environnement / package.json / paramètre de la commande) | ACCOUNT-02 | No developer password found |
  > | Le compte développeur spécifié n'existe pas (Le login ou le mot de passe est mauvais) | ACCOUNT-03 | This account doesn't exists on this platform |
  > | Le manager de votre organisation ZetaPush ne vous autorise pas à déployer sur cette application | RIGHT-01 | You can't deploy your code on this application : Access denied |
  > | Mauvaise utilisation des cloud services (Mauvaise syntaxe) | SERVICE-01 | Failed to create the services |
  > | Deux custom cloud services ont le même ID | SERVICE-02 | Some custom cloud services have the same name |
  > | Mauvaise utilisation des custom cloud services (Mauvaise syntaxe) | SERVICE-03 | Failed to create the custom cloud services |
  > | Utilisation d'une dépendance NPM inexistante | DEPENDENCY-01 | An used npm dependency doesn't exists
---

### <a name="P02-DEPLOY04"></a> [P02-DEPLOY04] ETQ dev je déploie mon custom cloud service en production avec une configuration dédiée à cet environnement avec les credentials externalisés

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

*GIVEN*
  - Je suis au sein d'un dossier contenant un fichier `.zetarc`
  - J'ai le nom de l'application dans le fichier `package.json`
  - J'utilise l'arborescence par défaut de ZetaPush
  - J'ai un compte sur ZetaPush (login=jeni@yopmail.com, password=zp-password)
  - J'ai deux environnements fournis par ZetaPush : 
    - `dev` pour le développement et les tests
    - `prod` pour déployer mon application
  - J'ai développé un service custom avec les fonctions suivantes :
    - ```createGame(player1, player2)```
    - ```gameAction(player, name, args)```
    - ```isFinished()```
    - ```getWinner()```
    - ```endGame()```
  - ZetaPush me permet de répliquer 3 fois mon worker en production et je n'ai rien configuré
  - J'ai plusieurs fichiers de configuration pour mes différents environnements :
    - ```worker/environment.yml``` (valeurs par défaut pour le développement) avec le contenu suivant :
      ```yml
      stripe:
          url: 'https://api.stripe.com'
          token: 'sk_test_BQokikJOvBiI2HlWgH4olfQ2'
      ```
    - ```worker/environment-prod.yml``` (surcharge pour l'environnement de production) avec le contenu suivant :
      ```yml
      stripe:
          token: 'sk_prod_dNuiVQyTlDMH5RdFYSD4nIV0'
      ```
  - Je ne précise aucune configuration concernant l'emplacement de mes fichiers (utilisation de la convention ZetaPush)

*WHEN*
  - J'exécute la commande : ```zeta push --worker --prod```

*THEN*
  - Le code présent dans `worker` est envoyé sur ZetaPush
  - Je vois l'état d'avancement du déploiement global
  - Je sais lorsque mon application est prête à être utilisée
  - Mes deux configurations sont "mergées" et la configuration finale équivant à :
    ```yml
    stripe:
        url: 'https://api.stripe.com'
        token: 'sk_prod_dNuiVQyTlDMH5RdFYSD4nIV0'
    ```
  - Je peux utiliser mon frontend pour interagir avec mon service custom déployé en production
  - Je peux appeler la fonction `createGame` de mon service custom directement depuis mon frontend via le SDK JS ZetaPush avec les paramètres suivants :
    - ```player1 = {"name": "Georgesdelajungle"}```
    - ```player2 = {"name": "Aladdin"}```
  - ZetaPush gère le load-balancing entre les 3 instances de mon worker (voir autres US)
  - Je peux visualiser les logs applicatifs de mon service custom (voir autres US)
  - Je peux consulter la santé de mon worker (voir autres US)


---

### <a name="P02-DEPLOY06"></a> [P02-DEPLOY06] ETQ dev je mets à jour mon application en production 

> TODO: A spécifier, avec le rollback

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

TODO: snapshot automatique faite par ZP avant l'upgrade pour backup des données en cas de code foireux ?

TODO: pouvoir skipper snapshot avec --no-snapshot-needed-im-the-best ?


---

### <a name="P02-DEPLOY07"></a> [P02-DEPLOY07] ETQ dev full-stack je déploie mon application (front et service custom) en production sans credentials à disposition

![celtia-alpha-1](https://img.shields.io/badge/milestone-celtia--alpha--1-blue.svg)

*GIVEN*
  - Je suis au sein d'un dossier ne contenant pas de fichier `.zetarc`
  - J'ai le nom de l'application dans le fichier `package.json`
  - J'utilise l'arborescence par défaut de ZetaPush
  - Je n'ai pas de compte ZetaPush
  - J'ai développé un service custom avec les fonctions suivantes :
    - ```createGame(player1, player2)```
    - ```gameAction(player, name, args)```
    - ```isFinished()```
    - ```getWinner()```
    - ```endGame()```
  - ZetaPush me permet de répliquer 3 fois mon worker en production et je n'ai rien configuré
  - J'utilise l'arborescence par défaut :

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

*WHEN*
  - J'exécute la commande : ```zeta push```

*THEN*
  - Un compte temporaire sur la plateforme ZetaPush a été créé
  - Mes _custom cloud services_ (dossier `worker`) sont envoyés sur ZetaPush
  - Je vois l'état d'avancement du déploiement global
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      | Publishing web application                        ██████░░░░░░
      / Publishing custom services on worker instance 1   ██████░░░░░░
      - Publishing custom services on worker instance 2   ████████░░░░
      \ Publishing custom services on worker instance 3   ██░░░░░░░░░░
    ```
  - Je sais lorsque mon application est prête à être utilisée
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      ✓ Web application published
      ✓ Custom services published on worker instance 1
      ✓ Custom services published on worker instance 2
      ✓ Custom services published on worker instance 3

    Your application is ready:
    - Your web application is ready and available at https://avengers-chat-web.prod.my-first-app.jeni.zetapush-apps.com
    - Your custom services are ready and accessible through ZetaPush

    As no account is specified, a temporary account has been created for you: 
    - login: vsgygfzq12ffq4fq
    - password: zhfuqzbvgfhreq4f56q4fqf6
    This account is only available for X days.
    You can convert this temporary account into a permanent account with your own login/password here : 
    https://console.zetapush.com/account/register/vsgygfzq12ffq4fq/zhfuqzbvgfhreq4f56q4fqf6
    NOTE: By registering, your current work and data will be kept
    ```
  - Mon frontend (dossier `front`) est envoyé sur ZetaPush
  - Mon front est disponible sur le site `avengers-chat-web.prod.my-first-app.jeni.zetapush-apps.com`
  - Mon frontend de production déployé utilise les services custom déployés
  - ZetaPush gère le load-balancing entre les 3 instances de mon worker (voir autres US)
  - Je peux visualiser les logs applicatifs de mon service custom (voir autres US)
  - Je peux consulter la santé de mon worker (voir autres US)

---

### <a name="P02-DEPLOY09"></a> [P02-DEPLOY09] ETQ dev full-stack je déploie mon application (front et service custom) en production avec la configuration en ligne de commande

![celtia-alpha-1](https://img.shields.io/badge/milestone-celtia--alpha--1-blue.svg)

*GIVEN*
  - Je suis au sein d'un dossier contenant un fichier `.zetarc` ayant le contenu suivant :
  ```
  ZP_DEVELOPER_LOGIN = fdhjsqfhruqih
  ZP_DEVELOPER_PASSWORD = gfjqh4564
  ```
  - J'ai le nom de l'application dans le fichier `package.json` (`avengers-chat`)
  - J'utilise l'arborescence par défaut de ZetaPush
  - J'ai un compte sur ZetaPush (login=jeni@yopmail.com, password=zp-password)
  - J'ai développé un service custom avec les fonctions suivantes :
    - ```createGame(player1, player2)```
    - ```gameAction(player, name, args)```
    - ```isFinished()```
    - ```getWinner()```
    - ```endGame()```
  - ZetaPush me permet de répliquer 3 fois mon worker en production et je n'ai rien configuré
  - J'utilise l'arborescence par défaut :

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

*WHEN*
  - J'exécute la commande : ```zeta push --developer-login jeni@yopmail.com --developer-password zp-password```

*THEN*
  - Le dossier `front` est envoyé sur ZetaPush pour le compte `jeni@yopmail.com` et l'application `avengers-chat`
  - L'ensemble de mes _custom cloud services_ définis dans le dossier `worker` est envoyé sur ZetaPush pour le compte `jeni@yopmail.com` et l'application `avengers-chat`
  - Je vois l'état d'avancement du déploiement global
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      | Publishing web application                        ██████░░░░░░
      / Publishing custom services on worker instance 1   ██████░░░░░░
      - Publishing custom services on worker instance 2   ████████░░░░
      \ Publishing custom services on worker instance 3   ██░░░░░░░░░░
    ```
  - Je sais lorsque mon application est prête à être utilisée
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      ✓ Web application published
      ✓ Custom services published on worker instance 1
      ✓ Custom services published on worker instance 2
      ✓ Custom services published on worker instance 3

    Your application is ready:
    - Your web application is ready and available at https://avengers-chat-web.prod.my-first-app.jeni.zetapush-apps.com
    - Your custom services are ready and accessible through ZetaPush
    ```
  - Mon front est disponible sur le site `avengers-chat-web.prod.my-first-app.jeni.zetapush-apps.com`
  - Mon frontend de production déployé utilise les services custom déployés
  - ZetaPush gère le load-balancing entre les 3 instances de mon worker (voir autres US)
  - Je peux visualiser les logs applicatifs de mon service custom (voir autres US)
  - Je peux consulter la santé de mon worker (voir autres US)

---

### <a name="P02-DEPLOY10"></a> [P02-DEPLOY10] ETQ dev full-stack je déploie mon application (front et service custom) avec une aborescence custom

![celtia-alpha-1](https://img.shields.io/badge/milestone-celtia--alpha--1-blue.svg)

*GIVEN*
  - Je suis au sein d'un dossier contenant un fichier `.zetarc`
  ```
  ZP_DEVELOPER_LOGIN = fdhjsqfhruqih
  ZP_DEVELOPER_PASSWORD = gfjqh4564
  ```
  - Le nom de l'application est spécifié dans le fichier `package.json` (`avengers-chat`)
  - J'ai un compte sur ZetaPush (login=jeni@yopmail.com, password=zp-password)
  - J'ai développé un service custom avec les fonctions suivantes :
    - ```createGame(player1, player2)```
    - ```gameAction(player, name, args)```
    - ```isFinished()```
    - ```getWinner()```
    - ```endGame()```
  - ZetaPush me permet de répliquer 3 fois mon worker en production et je n'ai rien configuré
  - L'arborescence de mon projet est :
  ```
  avengers-chat
  ├── .zetarc
  ├── .gitignore
  ├── dashboard
  │   ├── src
  │   │   └── app
  │   │       └── main.ts
  │   └── dist
  │       ├── assets
  │       │   └── toto.png
  │       ├── main.js
  │       └── index.html
  ├── business
  │   ├── src
  │   │   ├── user-service.ts
  │   │   ├── chat-service.ts
  │   │   └── index.ts
  │   └── dist
  │       └── index.js
  └── package.json
  ```
  - Je n'ai pas configuré mon `package.json` pour indiquer mon arborescence custom

*WHEN*
  - J'exécute la commande : ```zeta push --front=dashboard/dist --worker=business/dist```

*THEN*
  - Mon application front packagée est envoyée sur ZetaPush
  - Mes _custom cloud services_ sont envoyés sur ZetaPush
  - Je vois l'état d'avancement du déploiement global
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      | Publishing web application                        ██████░░░░░░
      / Publishing custom services on worker instance 1   ██████░░░░░░
      - Publishing custom services on worker instance 2   ████████░░░░
      \ Publishing custom services on worker instance 3   ██░░░░░░░░░░
    ```
  - Je sais lorsque mon application est prête à être utilisée
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      ✓ Web application published
      ✓ Custom services published on worker instance 1
      ✓ Custom services published on worker instance 2
      ✓ Custom services published on worker instance 3

    Your application is ready:
    - Your web application is ready and available at https://avengers-chat-web.prod.my-first-app.jeni.zetapush-apps.com
    - Your custom services are ready and accessible through ZetaPush
    ```
  - Mon front est disponible sur le site `avengers-chat-web.prod.my-first-app.jeni.zetapush-apps.com`
  - Mon frontend de production déployé utilise les services custom déployés
  - ZetaPush gère le load-balancing entre les 3 instances de mon worker (voir autres US)
  - Je peux visualiser les logs applicatifs de mon service custom (voir autres US)
  - Je peux consulter la santé de mon worker (voir autres US)

---

### <a name="P02-DEPLOY11"></a> [P02-DEPLOY11] ETQ dev full-stack je sais lorsque mon worker n'a pas démarré 

![celtia-alpha-1](https://img.shields.io/badge/milestone-celtia--alpha--1-blue.svg)

*GIVEN*
  - J'ai exécuté la commande : ```zeta push```
  
*WHEN*
  - Je vois dans ma console que le déploiement a fonctionné mais que le lancement de mon worker n'a pas fonctionné

*THEN*
  - Je sais que mon worker n'est pas en fonctionnement
  - J'ai suffisamment d'information pour savoir ce qui n'a pas fonctionné
  - La précédente version déployée et fonctionnelle n'est pas écrasée ou corrompue (que ce soit front ou back)
  - J'ai un retour dans mon terminal du type :
  
    ```
    $ zeta push
    
    Your application is deployed but the worker failed to start. The previous version is still running.
    The returned error is the following :

    code : NET-01
    message : The ZetaPush platform has no network access
    ```
  
  > Ensemble des messages erreurs potentielles
  >
  > | Cause | Code | Message |
  > |:---:|:---:|:---:|
  > | La plateforme ZetaPush n'a pas accès à internet | NET-03 | The ZetaPush platform has no network access
  > | La plateforme ZetaPush est down | PLATFORM-01 | The ZetaPush platform is down |
  > | La commande `npm install` n'a pas fonctionné lors de la création du worker | DEPENDENCY-02 | The worker failed to install npm dependencies |
  > | L'instanciation des services n'a pas fonctionné | SERVICE-04 | The worker failed to create the services on the application |
  > | La création de l'image Docker n'a pas fonctionné | PLATFORM-02 | The docker image to deploy your worker failed to be created |
  > | Le déploiement des workers (point de vue Kubernetes) a complètement échoué | DEPLOY-01 | The platform failed to deploy the workers |

---


# <a name="parcours-3"></a> ![Parcours 3](https://img.shields.io/badge/parcours-équipe%20front-00d0ff.svg) Mon équipe développe une application front avec ZetaPush sans services custom


## Vue d'ensemble


## User stories


### <a name="P03-DEPLOY01"></a> [P03-DEPLOY01] ETQ exploitant je mets à disposition l'application web pour la qualification avec mes outils habituels

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

*GIVEN*
  - Mon entreprise a un compte chez ZetaPush (login=dragons@yopmail.com, password=zp-password)
  - Mon entreprise a créé une application dont l'identifiant est `avengers-chat`
  - Mon entreprise a souscrit plusieurs environnements sur ZetaPush (developpement, intégration, recette, production) :
    - `dev` pour le développement et les tests
    - `integration` pour l'intégration continue
    - `recette` pour la qualification
    - `prod` pour déployer mon application
  - L'environnement de recette est configuré pour répliquer 4 fois mon worker
  - L'application utilise les services standard ZetaPush
  - L'intégration continue a généré un livrable contenant l'application web (`avengers-chat-front-2.0.1.zip`). Ce livrable est disponible sur un repository privé de l'entreprise.
  - J'ai téléchargé le livrable `avengers-chat-front-2.0.1.zip` sur mon poste (dans `~/avengers-chat`)

*WHEN*
  - J'exécute la commande : 
      ```console
      $ curl -X POST -H "Content-Type: multipart/form-data" \
                    -u "dragons@yopmail.com:zp-password" \
                    -F "file=@avengers-chat/avengers-chat-front-2.0.1.zip" \
                    https://console.zetapush.com/apps/avengers-chat/env/recette
      ```

*THEN*
  - L'application est envoyée sur ZetaPush
  - TODO: comment voir l'état d'avancement du déploiement ? Ouvrir la console ZetaPush ?
  - L'application est prête à être utilisée pour la qualification
  - TODO: logs ?
  - TODO: status pour savoir si tout est ok
  - TODO: utiliser curl/wget pour interroger le status ?

---

### <a name="P03-DEPLOY02"></a> [P03-DEPLOY02] ETQ exploitant je mets à disposition l'application web pour la qualification avec les outils ZetaPush

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

---

### <a name="P03-DEPLOY03"></a> [P03-DEPLOY03] ETQ exploitant je mets à disposition l'application web en production avec mes outils habituels

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

*GIVEN*
  - Mon entreprise a un compte chez ZetaPush (login=dragons@yopmail.com, password=zp-password)
  - Mon entreprise a créé une application dont l'identifiant est `avengers-chat`
  - Mon entreprise a souscrit plusieurs environnements sur ZetaPush (developpement, intégration, recette, production) :
    - `dev` pour le développement et les tests
    - `integration` pour l'intégration continue
    - `recette` pour la qualification
    - `prod` pour déployer mon application
  - L'environnement de production est configuré pour pour répliquer 4 fois mon worker
  - L'application utilise les services standard ZetaPush
  - L'intégration continue a généré un livrable contenant l'application web (`avengers-chat-front-2.0.1.zip`). Ce livrable est disponible sur un repository privé de l'entreprise.
  - La qualification de la version 2.0.1 est terminée et le livrable 2.0.1 est accepté pour être utilisé en production
  - J'ai téléchargé le livrable `avengers-chat-front-2.0.1.zip` sur mon poste (dans `~/avengers-chat`)

*WHEN*
  - J'exécute la commande : 
      ```console
      $ curl -X POST -H "Content-Type: multipart/form-data" \
                    -u "dragons@yopmail.com:zp-password" \
                    -F "file=@avengers-chat/avengers-chat-front-2.0.1.zip" \
                    https://console.zetapush.com/apps/avengers-chat/env/prod
      ```

*THEN*
  - L'application est envoyée sur ZetaPush
  - TODO: comment voir l'état d'avancement du déploiement ? Ouvrir la console ZetaPush ?
  - L'application est prête à être utilisée pour la qualification
  - TODO: logs ?
  - TODO: status pour savoir si tout est ok
  - TODO: utiliser curl/wget pour interroger le status ?


---

### <a name="P03-DEPLOY04"></a> [P03-DEPLOY04] ETQ exploitant je mets à disposition l'application web en production avec les outils ZetaPush

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

# <a name="parcours-4"></a> ![Parcours 4](https://img.shields.io/badge/parcours-équipe%20full--stack-00d0ff.svg) Mon équipe développe une application avec ZetaPush et des services custom


## Vue d'ensemble

TODO: est-ce que les services ZetaPush sont partagés en dev ? Risque de se marcher sur les pieds !
TODO: cette vue d'ensemble devrait être mutualisée et il faudrait se concentrer ici sur la partie déploiement uniquement

En phase de développement, chaque développeur travaille en local sur son poste. Il utilise son navigateur préféré ainsi que son nodeJS en local.
Son frontend et ses services custom interagissent avec ZetaPush pour bénéficier des services proposés par ZetaPush afin de lui faire gagner du temps.


Lorsque l'un des développeur a terminé le développement d'une fonctionnalité, il commite son code (sur son Git, SVN ou autre).


L'intégration continue se charge alors de construire l'application.


TODO: tests auto







## User stories

### <a name="P04-DEPLOY01"></a> [P04-DEPLOY01] ETQ exploitant je mets à disposition l'application web avec les services custom pour la qualification avec mes outils habituels

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

*GIVEN*
  - Mon entreprise a un compte chez ZetaPush (login=dragons@yopmail.com, password=zp-password)
  - Mon entreprise a créé une application dont l'identifiant est `avengers-chat`
  - Mon entreprise a souscrit plusieurs environnements sur ZetaPush (developpement, intégration, recette, production) :
    - `dev` pour le développement et les tests
    - `integration` pour l'intégration continue
    - `recette` pour la qualification
    - `prod` pour déployer mon application
  - L'équipe de développement a développé un service custom avec les fonctions suivantes :
    - ```createGame(player1, player2)```
    - ```gameAction(player, name, args)```
    - ```isFinished()```
    - ```getWinner()```
    - ```endGame()```
  - L'environnement de recette est configuré pour répliquer 4 fois mon worker
  - L'intégration continue a généré un livrable contenant l'application web (`avengers-chat-front-2.0.1.zip`). Ce livrable est disponible sur un repository privé de l'entreprise.
  - J'ai téléchargé le livrable `avengers-chat-front-2.0.1.zip` sur mon poste (dans `~/avengers-chat`)
  - L'intégration continue a généré un livrable contenant les services custom (`avengers-chat-services-2.0.1.zip`). Ce livrable est disponible sur un repository privé de l'entreprise.
  - J'ai téléchargé le livrable `avengers-chat-services-2.0.1.zip` sur mon poste (dans `~/avengers-chat`)
  - J'ai plusieurs fichiers de configuration pour les différents environnements :
    - ```src/worker/environment.yml``` (valeurs par défaut pour le développement directement contenu dans l'archive `avengers-chat-services-2.0.1.zip`) avec le contenu suivant :
      ```yml
      stripe:
          url: 'https://api.stripe.com'
          token: 'sk_test_BQokikJOvBiI2HlWgH4olfQ2'
      ```
    - ```~/avengers-chat/recette.yml``` :
      ```yml
      stripe:
          token: 'sk_recette_dNuiVQyTlDMH5RdFYSD4nIV0'
      ```
  - J'ai généré un zip nommé `avengers-chat-2.0.1.zip` et contenant :
    - `avengers-chat-front-2.0.1.zip`
    - `avengers-chat-services-2.0.1.zip`
    - `recette.yml`

*WHEN*
  - J'exécute la commande : 
      ```console
      $ curl -X POST -H "Content-Type: multipart/form-data" \
                    -u "dragons@yopmail.com:zp-password" \
                    -F "file=@avengers-chat/avengers-chat-2.0.1.zip" \
                    https://console.zetapush.com/apps/avengers-chat/env/recette
      ```

*THEN*
  - L'application est envoyée sur ZetaPush
  - TODO: comment voir l'état d'avancement du déploiement ? Ouvrir la console ZetaPush ?
  - L'application est prête à être utilisée pour la qualification
  - TODO: logs
  - TODO: status pour savoir si tout est ok
  - TODO: utiliser curl/wget pour interroger le status ?


---

### <a name="P04-DEPLOY02"></a> [P04-DEPLOY02] ETQ exploitant je mets à disposition l'application web avec les services custom en production avec les outils ZetaPush

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

---

### <a name="P04-DEPLOY03"></a> [P04-DEPLOY03] ETQ exploitant je mets à disposition l'application web avec les services custom pour la qualification avec les outils ZetaPush

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

---

### <a name="P04-DEPLOY04"></a> [P04-DEPLOY04] ETQ exploitant je mets à disposition l'application web avec les services custom en production avec mes outils habituels

![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-blue.svg)

*GIVEN*
  - Mon entreprise a un compte chez ZetaPush (login=dragons@yopmail.com, password=zp-password)
  - Mon entreprise a créé une application dont l'identifiant est `avengers-chat`
  - Mon entreprise a souscrit plusieurs environnements sur ZetaPush (developpement, intégration, recette, production) :
    - `dev` pour le développement et les tests
    - `integration` pour l'intégration continue
    - `recette` pour la qualification
    - `prod` pour déployer mon application
  - L'équipe de développement a développé un service custom avec les fonctions suivantes :
    - ```createGame(player1, player2)```
    - ```gameAction(player, name, args)```
    - ```isFinished()```
    - ```getWinner()```
    - ```endGame()```
  - L'environnement de production est configuré pour répliquer 4 fois mon worker
  - L'intégration continue a généré un livrable contenant l'application web (`avengers-chat-front-2.0.1.zip`). Ce livrable est disponible sur un repository privé de l'entreprise.
  - L'intégration continue a généré un livrable contenant les services custom (`avengers-chat-services-2.0.1.zip`). Ce livrable est disponible sur un repository privé de l'entreprise.
  - La qualification de la version 2.0.1 est terminée et le livrable 2.0.1 est accepté pour être utilisé en production
  - J'ai téléchargé le livrable `avengers-chat-front-2.0.1.zip` sur mon poste (dans `~/avengers-chat`)
  - J'ai téléchargé le livrable `avengers-chat-services-2.0.1.zip` sur mon poste (dans `~/avengers-chat`)
  - J'ai plusieurs fichiers de configuration pour les différents environnements :
    - ```src/worker/environment.yml``` (valeurs par défaut pour le développement directement contenu dans l'archive `avengers-chat-services-2.0.1.zip`) avec le contenu suivant :
      ```yml
      stripe:
          url: 'https://api.stripe.com'
          token: 'sk_test_BQokikJOvBiI2HlWgH4olfQ2'
      ```
    - ```~/avengers-chat/prod.yml``` :
      ```yml
      stripe:
          token: 'sk_recette_dNuiVQyTlDMH5RdFYSD4nIV0'
      ```
  - J'ai généré un zip nommé `avengers-chat-2.0.1.zip` et contenant :
    - `avengers-chat-front-2.0.1.zip`
    - `avengers-chat-services-2.0.1.zip`
    - `prod.yml`

*WHEN*
  - J'exécute la commande : 
      ```console
      $ curl -X POST -H "Content-Type: multipart/form-data" \
                    -u "dragons@yopmail.com:zp-password" \
                    -F "file=@avengers-chat/avengers-chat-2.0.1.zip" \
                    https://console.zetapush.com/apps/avengers-chat/env/prod
      ```

*THEN*
  - L'application est envoyée sur ZetaPush
  - TODO: comment voir l'état d'avancement du déploiement ? Ouvrir la console ZetaPush ?
  - L'application est prête à être utilisée pour la qualification
  - TODO: logs
  - TODO: status pour savoir si tout est ok
  - TODO: utiliser curl/wget pour interroger le status ?


---

TODO: gestion des versions
TODO: mise à jour






