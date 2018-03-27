# Objectifs

- Un développeur front doit pouvoir utiliser les services ZetaPush dans son front.
- Un développeur full-stack doit pouvoir utiliser les services ZetaPush dans son front et coder son propre métier pour simplifier le développement de son/ses front(s).

Les profils utilisés sont définis dans [commun.md](./commun.md).

# Pré-requis

J'utilise mon éditeur de texte ou IDE préféré.
Je créé une nouvelle application front avec mon framework préféré (Angular, React, Vue, ...).


# <a name="parcours-1"></a> Parcours 1 : Je développe une application front avec ZetaPush sans service custom


## User stories

### ETQ dev front je créé ma première application from scratch avec les outils du standard du web


*GIVEN*
  - J'ai un gestionnaire de package installé (npm ou yarn par exemple)
  - J'ai un début d'application front (au moins le package.json)
  
*WHEN*
  - Lorsque j'ajoute la dépendance au SDK JavaScript ZetaPush, exemple:
  ```npm i --save zetapush-js```

*THEN*
  - Je peux dès à présent (en ajoutant le code associé à mon application) faire des appels sur ZetaPush
  - Un compte a été automatiquement créé pour moi avec un espace pour mon application
  - Je connais l'identifiant de mon application et les credentials ZetaPush
  - Mon application est configurée avec cet identifiant
  - Je suis alerté que l'application automatiquement créée sur ZetaPush est valable X jours
  - Je peux me connecter sur la console ZetaPush avec les credentials auto-générés par ZetaPush pour transformer mon application temporaire en application permanente et choisir mes vrais identifiants
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
    
  As no application is specified, a temporary application has been created for you :
    - application name: my-first-app-with-zetapush
    This application is only available X days
    You can convert this temporary application into a permanent application with your own name here :
    https://console.zetapush.com/app/register/my-first-app-with-zetapush
    NOTE: By registering, your current work and data will be kept
  ```
  

### ETQ dev front je créé ma première application via la CLI

*GIVEN*
  - J'ai un gestionnaire de package installé (npm ou yarn par exemple)
  - J'ai installé la CLI ZetaPush (via npm ou yarn)

*WHEN*
  - Lorsque que j'initialise un nouveau projet front exemple:
  ```$> zeta new --front ```

*THEN*
  - J'ai une application front minimaliste avec package.json
  - Je peux dès à présent faire des appels sur ZetaPush
  - Un compte a été automatiquement créé pour moi avec un espace pour mon application
  - Je connais l'identifiant de mon application et les credentials ZetaPush
  - Mon application est configurée avec cet identifiant
  - Je suis alerté que l'application automatiquement créée sur ZetaPush est valable X jours
  - Je peux me connecter avec les credentials auto-générés par ZetaPush pour transformer mon application temporaire en application permanente et choisir mes vrais identifiants
  - J'ai un README.md avec les informations m'indiquant comment démarrer (utilisation de la CLI, les bonnes pratiques ZetaPush, les liens vers la documentation)
  - J'ai un exemple de service type "Welcome/HelloWorld" dans mon front

  
### ETQ dev front je souhait ajouter des services ZetaPush à une application front existante

*GIVEN*
  - J'ai un gestionnaire de package installé (npm ou yarn par exemple)
  - Mon application front contient un package.json

*WHEN*
  - Lorsque que j'installe zetapush-js:
  ```npm i --save zetapush-js```

*THEN*
  - Je peux dès à présent faire des appels sur ZetaPush
  - Un compte a été automatiquement créé pour moi avec un espace pour mon application
  - Je connais l'identifiant de mon application et les credentials ZetaPush
  - Mon application est configurée avec cet identifiant
  - Je suis alerté que l'application automatiquement créée sur ZetaPush est valable X jours
  - Je peux me connecter avec les credentials auto-générés par ZetaPush pour transformer mon application temporaire en application permanente et choisir mes vrais identifiants


# <a name="parcours-2"></a> Parcours 2 : Je développe une application front avec ZetaPush avec service custom

## User stories

### ETQ dev full-stack je créé ma première application from scratch avec les outils du standard du web

*GIVEN*
  - J'ai un gestionnaire de package installé (npm ou yarn par exemple)
  - J'ai un début d'application front (au moins le package.json)
  - J'ai un début d'application backend Node (au moins le package.json)
  
*WHEN*
  - Lorsque j'ajoute la dépendance au SDK JavaScript ZetaPush dans mon front, exemple:
  ```npm i --save zetapush-js```
  - Lorsque j'ajoute la dépendance au SDK Custom ZetaPush dans mon back, exemple:
  ```npm i --save zetapush-custom``` TODO: trouver mieux que ZetaPush-custom

*THEN*
  - Je peux dès à présent faire des appels sur ZetaPush
  - Un compte a été automatiquement créé pour moi avec un espace pour mon application
  - Je connais l'identifiant de mon application et les credentials ZetaPush
  - Mon application est configurée avec cet identifiant
  - Je suis alerté que l'application automatiquement créée sur ZetaPush est valable X jours
  - Je peux me connecter avec les credentials auto-générés par ZetaPush pour transformer mon application temporaire en application permanente et choisir mes vrais identifiants
  - Je peux créer des methodes dans mon back-end appelables via mon front.

### ETQ dev full-stack je créé ma première application via la CLI

*GIVEN*
  - J'ai un gestionnaire de package installé (npm ou yarn par exemple)
  - J'ai installé la CLI ZetaPush (via npm ou yarn)

*WHEN*
  - Lorsque que j'init un nouveau projet, exemple:
  ```$> zeta new``` (équivaut à ```$> zeta new --front --server``` et  ```$> zeta new --front=front/dist --server=server```)

*THEN*
  - J'obtient l'arborescence suivante : 
     ```
     .
     ├── node_modules/...
     ├── front
     |   └── dist
     |       ├── index.html
     |       ├── helloWorld.js
     |       └── index.js
     ├── server
     |   ├── src
     |   |   ├── index.js
     |   |   └── hello-service.js
     |   └── tests
     |       └── hello-service.test.js
     ├── README.md
     └── package.json
     ```
  - J'ai une application front minimaliste avec un index.html qui utilise zetapush-sdk.js
  - Je peux dès à présent faire des appels sur ZetaPush
  - Un compte a été automatiquement créé pour moi avec un espace pour mon application
  - Je connais l'identifiant de mon application et les credentials ZetaPush
  - Mon application est configurée avec cet identifiant
  - Je suis alerté que l'application automatiquement créée sur ZetaPush est valable X jours
  - Je peux me connecter avec les credentials auto-générés par ZetaPush pour transformer mon application temporaire en application permanente et choisir mes vrais identifiants
  - Je peux créer des méthodes dans mon back-end appelables via mon front.
  - J'ai un README.md avec les informations m'indiquant comment démarrer (utilisation de la CLI, les bonnes pratiques ZetaPush, les liens vers la documentation)
  - J'ai un exemple de service type "Welcome/HelloWorld" dans mon front
  - J'ai un exemple de service custom `hello-service.js`
  - La console m'indique que je peux lancer ma première application avec `zeta start`


### ETQ dev full-stack je créé ma première application via la CLI avec une arborescence spécifique

*GIVEN*
  - J'ai un gestionnaire de package installé (npm ou yarn par exemple)
  - J'ai installé la CLI ZetaPush (via npm ou yarn)

*WHEN*
  - Lorsque que j'init un nouveau projet, exemple:
  ```$> zeta new --front=app/www --server=zeta-app```

*THEN*
  - J'obtient l'arborescence suivante : 

     ```
     .
     ├── node_modules/...
     ├── app
     |   └── www
     |       ├── index.html
     |       ├── helloWorld.js
     |       └── index.js
     ├── zeta-app
     |   ├── src
     |   |   ├── index.js
     |   |   └── hello-service.js
     |   └── tests
     |       └── hello-service.test.js
     ├── README.md
     └── package.json
     ```
  - Le package.json contient la configuration permettant le mapping des dossiers :
  ```
      ...
      "zeta": {
        "front": "app/www",
        "server": "zeta-app"
      }
      ...
  ```
  - J'ai une application front minimaliste avec un index.html qui utilise zetapush-sdk.js
  - Je peux dès à présent faire des appels sur ZetaPush
  - Un compte a été automatiquement créé pour moi avec un espace pour mon application
  - Je connais l'identifiant de mon application et les credentials ZetaPush
  - Mon application est configurée avec cet identifiant
  - Je suis alerté que l'application automatiquement créée sur ZetaPush est valable X jours
  - Je peux me connecter avec les credentials auto-générés par ZetaPush pour transformer mon application temporaire en application permanente et choisir mes vrais identifiants
  - Je peux créer des méthodes dans mon back-end appelables via mon front.
  - J'ai un README.md avec les informations m'indiquant comment démarrer (utilisation de la CLI, les bonnes pratiques ZetaPush, les liens vers la documentation)
  - J'ai un exemple de service type "Welcome/HelloWorld" dans mon front
  - J'ai un exemple de service custom `hello-service.js`
  - La console m'indique que je peux lancer ma première application avec `zeta start`




### ETQ full-stack j'ajoute le projet de services custom utilisé par mon application Angular existante

TODO

### ETQ full-stack j'ajoute le projet de services custom utilisé par mes deux applications Angular existantes avec une arborescence spécifique

*GIVEN*
  - J'ai un gestionnaire de package installé (npm ou yarn par exemple)
  - J'ai installé la CLI ZetaPush (via npm ou yarn)
  - J'ai deux projets Angular existants :
    - Un dashboard d'administration avec l'arborescence suivante :
      ```
       dashboard
        ├── node_modules/...
        ├── src
        |   └── app
        |       ├── app.component.html
        |       └── app.module.ts
        ├── dist
        |   ├── index.html
        |   ├── index.css
        |   └── index.js
        └── package.json
      ```
      Dont le nom est `dragons-dashboard` (le nom est configuré dans le package.json)
    - Une application mobile avec l'arborescence suivante :
      ```
       mobileapp
        ├── node_modules/...
        ├── src
        |   └── app
        |       ├── app.component.html
        |       └── app.module.ts
        ├── www
        |   ├── index.html
        |   ├── index.css
        |   └── index.js
        └── package.json
       ```  
       Dont le nom est `dragons-mobileapp` (le nom est configuré dans le package.json)
   - Les deux projets sont dans un dossier nommé `dragons`
  
*WHEN*
  - Lorsque que j'init un nouveau projet dans le dossier `dragons`:
  ```$> zeta new --server=zeta-app```

*THEN*
  - J'ai l'arborescence suivante : 
   ```
     dragons
     ├── node_modules/...
     ├── dashboard
     |   ├── node_modules/...
     |   ├── src
     |   |   └── app
     |   |       ├── app.component.html
     |   |       └── app.module.ts
     |   ├── dist
     |   |   ├── index.html
     |   |   ├── index.css
     |   |   └── index.js
     |   └── package.json
     ├── mobileapp
     |   ├── node_modules/...
     |   ├── src
     |   |   └── app
     |   |       ├── app.component.html
     |   |       └── app.module.ts
     |   ├── dist
     |   |   ├── index.html
     |   |   ├── index.css
     |   |   └── index.js
     |   └── package.json
     ├── zeta-app
     |   ├── src
     |   |   ├── index.js
     |   |   └── hello-service.js
     |   └── tests
     |       └── hello-service.test.js
     ├── README.md
     └── package.json
     ```  
  - Le package.json racine contient la configuration permettant le mapping des dossiers :
  ```
      ...
      "zeta": {
        "front": ["dashboard/dist", "mobileapp/dist"],
        "server": "zeta-app"
      }
      ...
      ...
      "zeta": {
        "front": {
          "dashboard": "dashboard/dist",
          "mobileapp": "mobileapp/dist"
        },
        "server": "zeta-app"
      }
      ...
  ```
  - Je peux dès à présent faire des appels sur ZetaPush
  - Un compte a été automatiquement créé pour moi avec un espace pour mon application
  - Je connais l'identifiant de mon application et les credentials ZetaPush
  - Mon application est configurée avec cet identifiant
  - Je suis alerté que l'application automatiquement créée sur ZetaPush est valable X jours
  - Je peux me connecter avec les credentials auto-générés par ZetaPush pour transformer mon application temporaire en application permanente et choisir mes vrais identifiants
  - Je peux créer des méthodes dans mon back-end appelables via mon front.
  - J'ai un README.md avec les informations m'indiquant comment démarrer (utilisation de la CLI, les bonnes pratiques ZetaPush, les liens vers la documentation)
  - J'ai un exemple de service custom `hello-service.js`
  - La console m'indique que je peux lancer ma première application avec `zeta start`

