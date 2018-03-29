# Objectifs

- Un développeur web doit pouvoir développer son front en utilisant les services ZetaPush et sans être obligé de développer de code backend spécifique. Il doit pouvoir déployer son front sur ZetaPush.
- Un développeur web doit pouvoir coder son propre métier pour simplifier le développement de son/ses front(s). Il doit pouvoir déployer ses services custom sur ZetaPush.
- Un développeur web ayant un front et des services custom doit pouvoir déployer son application sur ZetaPush (front et backend custom)


# Pré-requis

# <a name="parcours-1"></a> Parcours 1 : Je développe une application front avec ZetaPush sans service custom

## Vue d'ensemble

![Déploiement en production front seulement](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/dev-front-deploiement-prod-front-only.html)

## User stories

### ETQ dev front je déploie mon application en production

*GIVEN*
  - J'ai un compte sur ZetaPush (login=jeni@yopmail.com, password=zp-password)
  - Je n'appartient pas à une organisation (je développe seul)
  - J'ai l'identifiant de mon application (my-first-app)
  - J'ai un seul environnement fourni par ZetaPush (production)
  - J'ai un front que j'ai buildé à l'aide de mes outils habituels et le résultat est dans le répertoire `dist`
  - Mon front s'appelle `avengers-chat-web`

*WHEN*
  - J'exécute la commande : ```zeta push```

*THEN*
  - Le code présent dans `dist` est envoyé sur ZetaPush
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
  - Mon front est disponible sur le site `avengers-chat-web.prod.my-first-app.jeni.zetapush-apps.com`




### ETQ dev front je déploie mon application sans identifiants de connexion

*GIVEN*
  - Je n'ai pas explicitement créé de compte chez ZetaPush
  - Je n'ai pas explicitement choisi l'identifiant de mon application
  - Je n'ai pas connaissance d'un éventuel environnement de développement
  - J'ai un front que j'ai buildé à l'aide de mes outils habituels et le résultat est dans le répertoire `dist`
  - Mon front s'appelle `avengers-chat-web`

*WHEN*
  - J'éxécute la commande : ```zeta push```

*THEN*
  - Le code présent dans `dist` est envoyé sur ZetaPush
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

    Your web application is ready and available at https://avangers-chat.prod.my-first-app.fgfhjoh48971zfgq.zetapush-apps.com
    You can manage your application on "http://console.zetapush.com" using the following account:
      - login : "fgfhjoh48971zfgq" 
      - password "fzoqfhue9454nhd"
    The ID of your application is : "my-first-app"
    This application will expired in X days.
    ```
  - Mon front est disponible sur le site `avangers-chat.prod.my-first-app.fgfhjoh48971zfgq.zetapush-apps.com`
  - Un compte temporaire m'a été créé chez ZetaPush
  - Je sais comment gérer mon application, sachant qu'elle va expirer dans X jours


# <a name="parcours-2"></a> Parcours 2 : Je développe une application avec ZetaPush et des services custom

## Vue d'ensemble

J'ai développé sur ma machine avec mon propre NodeJS qui interagit avec ZetaPush.

![Développement local](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/dev-front-processus-developpement.html)


Mon application est prête à partir en production. Je la déploie depuis mon poste.

![Déploiement en production](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/dev-full-stack-deploiement-prod-server-only.html)


## User stories

### ETQ dev full-stack je déploie mes services custom en production

*GIVEN*
  - J'ai un compte sur ZetaPush (login=jeni@yopmail.com, password=zp-password)
  - Je n'appartient pas à une organisation (je développe seul)
  - J'ai l'identifiant de mon application (my-first-app)
  - J'ai un seul environnement fourni par ZetaPush
  - J'ai développé un service custom avec les fonctions suivantes :
    - ```createGame(player1, player2)```
    - ```gameAction(player, name, args)```
    - ```isFinished()```
    - ```getWinner()```
    - ```endGame()```
  - ZetaPush me met à disposition 3 noeuds en production et je n'ai rien configuré

*WHEN*
- J'exécute la commande : ```zeta push --server-only```

*THEN*
  - Mon code custom est envoyé sur ZetaPush
  - Je vois l'état d'avancement du déploiement global
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      | Publishing custom services on node 1   ██████░░░░░░
      - Publishing custom services on node 2   ████████░░░░
      / Publishing custom services on node 3   ██░░░░░░░░░░
    ```
  - Je sais lorsque mon application est prête à être utilisée
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      ✓ Custom services published on node 1
      ✓ Custom services published on node 2
      ✓ Custom services published on node 3

    Your custom services are ready and accessible through ZetaPush
    ```
  - Je peux utiliser mon frontend pour interagir avec mon service custom déployé en production
  - Je peux appeler la fonction `createGame` de mon service custom directement depuis mon frontend via le SDK JS ZetaPush avec les paramètres suivants :
    - ```player1 = {"name": "Georgesdelajungle"}```
    - ```player2 = {"name": "Aladdin"}```
  - ZetaPush gère le load-balancing entre les 3 noeuds (voir autres US)
  - Je peux visualiser les logs applicatifs de mon service custom (voir autres US)
  - Je peux consulter la santé des noeuds déployés par ZetaPush (voir autres US)

TODO: préciser comment on accède aux services custom au travers de ZetaPush ?


### ETQ dev full-stack je déploie mes services custom sans identifiants de connexion

*GIVEN*
  - Je n'ai pas explicitement créé de compte chez ZetaPush
  - Je n'ai pas explicitement choisi l'identifiant de mon application
  - Je n'ai pas connaissance d'un éventuel environnement de développement
  - J'ai développé un service custom avec les fonctions suivantes :
    - ```createGame(player1, player2)```
    - ```gameAction(player, name, args)```
    - ```isFinished()```
    - ```getWinner()```
    - ```endGame()```
  - ZetaPush me met à disposition 3 noeuds en production et je n'ai rien configuré
  - Mon front s'appelle `avengers-chat-web`

*WHEN*
  - J'exécute la commande : ```zeta push --server-only```

*THEN*
  - Mon code custom est envoyé sur ZetaPush
  - Je vois l'état d'avancement du déploiement global
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      | Publishing custom services on node 1   ██████░░░░░░
      - Publishing custom services on node 2   ████████░░░░
      / Publishing custom services on node 3   ██░░░░░░░░░░
    ```
  - Je sais lorsque mon application est prête à être utilisée
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      ✓ Custom services published on node 1
      ✓ Custom services published on node 2
      ✓ Custom services published on node 3

    Your custom services are ready and accessible through ZetaPush
    You can manage your application on "http://console.zetapush.com" using the following account:
      - login : "fgfhjoh48971zfgq" 
      - password "fzoqfhue9454nhd"
    The ID of your application is : "my-first-app"
    This application will expired in X days.
    ```
  - Je peux utiliser mon frontend pour interagir avec mon service custom déployé en production
  - Je peux appeler la fonction `createGame` de mon service custom directement depuis mon frontend via le SDK JS ZetaPush avec les paramètres suivants :
    - ```player1 = {"name": "Georgesdelajungle"}```
    - ```player2 = {"name": "Aladdin"}```
  - ZetaPush gère le load-balancing entre les 3 noeuds (voir autres US)
  - Je peux visualiser les logs applicatifs de mon service custom (voir autres US)
  - Je peux consulter la santé des noeuds déployés par ZetaPush (voir autres US)
  - Un compte temporaire m'a été créé chez ZetaPush
  - Je sais comment gérer mon application, sachant qu'elle va expirer dans X jours
  - J'ai un identifiant d'application qui m'a été donné pour l'utiliser sur la partie front


### ETQ dev full-stack je déploie mon application (front et service custom) en production

*GIVEN*
  - J'ai un compte sur ZetaPush (login=jeni@yopmail.com, password=zp-password)
  - J'ai l'identifiant de mon application (my-first-app)
  - J'ai un seul environnement fourni par ZetaPush
  - J'ai développé un service custom avec les fonctions suivantes :
    - ```createGame(player1, player2)```
    - ```gameAction(player, name, args)```
    - ```isFinished()```
    - ```getWinner()```
    - ```endGame()```
  - ZetaPush me met à disposition 3 noeuds en production et je n'ai rien configuré
  - J'ai un front que j'ai buildé à l'aide de mes outils habituels et le résultat est dans le répertoire /dist/front

*WHEN*
  - J'exécute la commande : ```zeta push```

*THEN*
  - Mon code custom est envoyé sur ZetaPush
  - Je vois l'état d'avancement du déploiement global
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      | Publishing web application             ██████░░░░░░
      / Publishing custom services on node 1   ██████░░░░░░
      - Publishing custom services on node 2   ████████░░░░
      \ Publishing custom services on node 3   ██░░░░░░░░░░
    ```
  - Je sais lorsque mon application est prête à être utilisée
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      ✓ Web application published
      ✓ Custom services published on node 1
      ✓ Custom services published on node 2
      ✓ Custom services published on node 3

    Your application is ready:
    - Your web application is ready and available at https://avengers-chat-web.prod.my-first-app.jeni.zetapush-apps.com
    - Your custom services are ready and accessible through ZetaPush
    ```
  - Mon frontend est envoyé sur ZetaPush
  - Mon front est disponible sur le site `avengers-chat-web.prod.my-first-app.jeni.zetapush-apps.com`
  - Mon frontend de production déployé utilise les services custom déployés
  - ZetaPush gère le load-balancing entre les 3 noeuds (voir autres US)
  - Je peux visualiser les logs applicatifs de mon service custom (voir autres US)
  - Je peux consulter la santé des noeuds déployés par ZetaPush (voir autres US)


TODO: autre visualisation possible (pipeline mais plus complexe à dev) :
    ```
    $ zeta push
    Deploying your application on production environment:
      
                          ┌──────────────┐
                          │ Upload code  │
               ┌──────────│              │─────────┐
               │          │ ✓ Done in 2s │         │
               │          └──────────────┘         │
               │                                   │
      ┌────────────────┐                 ┌───────────────────┐
      │ Publishing web │                 │ Publishing custom │
      │  application   │                 │      services     │
      │                │                 └───────────────────┘
      │ 3s             │                  /        │        \
      │ ██████░░░░░░   │           ┌────────┐ ┌────────┐ ┌────────┐
      └────────────────┘           │ node 1 │ │ node 2 │ │ node 3 │
                                   │        │ │        │ │        │
                                   │ 5s     │ │ 20s    │ │ 10s    │
                                   │████░░░░│ │██████░░│ │██░░░░░░│
                                   └────────┘ └────────┘ └────────┘
    ```

### ETQ dev je déploie mon application (front et service custom) sans identifiants de connexion

*GIVEN*
  - Je n'ai pas de compte chez ZetaPush
  - Je n'ai pas d'identifiant d'application
  - Je n'ai pas connaissance d'un éventuel environnement de développement
  - J'ai développé un service custom avec les fonctions suivantes :
    - ```createGame(player1, player2)```
    - ```gameAction(player, name, args)```
    - ```isFinished()```
    - ```getWinner()```
    - ```endGame()```
  - ZetaPush me met à disposition 3 noeuds en production et je n'ai rien configuré
  - J'ai un front que j'ai buildé à l'aide de mes outils habituels et le résultat est dans le répertoire `dist`

*WHEN*
  - J'exécute la commande : ```zeta push```

*THEN*
  - Mon code custom est envoyé sur ZetaPush
  - Je vois l'état d'avancement du déploiement global
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      | Publishing web application             ██████░░░░░░
      / Publishing custom services on node 1   ██████░░░░░░
      - Publishing custom services on node 2   ████████░░░░
      \ Publishing custom services on node 3   ██░░░░░░░░░░
    ```
  - Je sais lorsque mon application est prête à être utilisée
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      ✓ Web application published
      ✓ Custom services published on node 1
      ✓ Custom services published on node 2
      ✓ Custom services published on node 3

    Your application is ready:
    - Your web application is ready and available at https://avangers-chat.prod.my-first-app.fgfhjoh48971zfgq.zetapush-apps.com
    - Your custom services are ready and accessible through ZetaPush
    
    You can manage your application on "http://console.zetapush.com" using the following account:
      - login : "fgfhjoh48971zfgq" 
      - password "fzoqfhue9454nhd"
    The ID of your application is : "my-first-app"
    This application will expired in X days.
    ```
  - Mon frontend est envoyé sur ZetaPush
  - Mon front est disponible sur le site `https://avengers-chat-web.prod.my-first-app.fgfhjoh48971zfgq.zetapush-apps.com`
  - Mon frontend de production déployé utilise les services custom déployés
  - ZetaPush gère le load-balancing entre les 3 noeuds (voir autres US)
  - Je peux visualiser les logs applicatifs de mon service custom (voir autres US)
  - Je peux consulter la santé des noeuds déployés par ZetaPush (voir autres US)
  - Mon front est disponible sur le site `https://avengers-chat-web.prod.my-first-app.fgfhjoh48971zfgq.zetapush-apps.com`
  - Un compte temporaire m'a été créé chez ZetaPush
  - Je sais comment gérer mon application, sachant qu'elle va expirer dans X jours

### ETQ dev je suis aidé lorsque mon application (front et service custom) n'a pas pu être déployé en production


*GIVEN*
  - J'ai un compte sur ZetaPush (login=jeni@yopmail.com, password=zp-password)
  - J'ai l'identifiant de mon application (my-first-app)
  - J'ai un seul environnement fourni par ZetaPush
  - J'ai développé un service custom avec les fonctions suivantes :
    - ```createGame(player1, player2)```
    - ```gameAction(player, name, args)```
    - ```isFinished()```
    - ```getWinner()```
    - ```endGame()```
  - ZetaPush me met à disposition 3 noeuds en production et je n'ai rien configuré
  - J'ai un front que j'ai buildé à l'aide de mes outils habituels et le résultat est dans le répertoire `dist`
  - J'ai exécuté la commande : ```zeta push```
  - Mon code a bien été envoyé sur ZetaPush

*WHEN*
  - Le déploiement échoue

*THEN*
  - Je sais que mon application n'a pas pu être déployée
  - J'ai suffisamment d'information pour savoir ce qui n'a pas fonctionné :
    ```
    $ zeta push
    Deploying your application on production environment:
      ✓ Code uploaded
      ✓ Web application published
      x Custom services published on node 1
      ✓ Custom services published on node 2
      x Custom services published on node 3

    Your application couldn't be deployed. A rollback has been done to previous version.
    Here are the deployment logs:
      ...
      ...
      ...
    ```
  - Un rollback a été effectué pour me garantir une cohérence de déploiement
  - Mon front (ancienne version) est toujours disponible sur le site `avengers-chat-web.prod.my-first-app.jeni.zetapush-apps.com`
  - Mon frontend de production déployé utilise les services custom déployés pour la version précédente


### ETQ dev je déploie mon service custom en production avec une configuration dédiée à cet environnement avec les credentials externalisés


*GIVEN*
  - J'ai un compte sur ZetaPush (login=jeni@yopmail.com, password=zp-password)
  - J'ai l'identifiant de mon application (my-first-app)
  - J'ai deux environnements fournis par ZetaPush : 
    - `dev` pour le développement et les tests
    - `prod` pour déployer mon application
  - J'ai développé un service custom avec les fonctions suivantes :
    - ```createGame(player1, player2)```
    - ```gameAction(player, name, args)```
    - ```isFinished()```
    - ```getWinner()```
    - ```endGame()```
  - ZetaPush me met à disposition 3 noeuds en production et je n'ai rien configuré
  - J'ai plusieurs fichiers de configuration pour mes différents environnements :
    - ```src/server/environment.yml``` (valeurs par défaut pour le développement) avec le contenu suivant :
      ```yml
      stripe:
          url: 'https://api.stripe.com'
          token: 'sk_test_BQokikJOvBiI2HlWgH4olfQ2'
      ```
    - ```src/server/environment-prod.yml``` (surcharge pour l'environnement de production) avec le contenu suivant :
      ```yml
      stripe:
          token: 'sk_prod_dNuiVQyTlDMH5RdFYSD4nIV0'
      ```
  - Je ne précise aucune configuration concernant l'emplacement de mes fichiers (utilisation de la convention ZetaPush)

*WHEN*
  - J'exécute la commande : ```zeta push --server-only --prod```

*THEN*
  - Le code présent dans dist/server est envoyé sur ZetaPush
  - Je vois l'état d'avancement du déploiement global
  - Je sais lorsque mon application est prête à être utilisée
  - Mon application est correctement configurée pour utiliser l'environnement de prod :
    ```yml
    stripe:
        url: 'https://api.stripe.com'
        token: 'sk_test_BQokikJOvBiI2HlWgH4olfQ2'
    ```
  - ```src/server/environment-prod.yml``` (surcharge pour l'environnement de production) avec le contenu suivant :
    ```yml
    stripe:
        token: 'sk_prod_dNuiVQyTlDMH5RdFYSD4nIV0'
    ```
  - Je peux utiliser mon frontend pour interagir avec mon service custom déployé en production
  - Je peux appeler la fonction `createGame` de mon service custom directement depuis mon frontend via le SDK JS ZetaPush avec les paramètres suivants :
    - ```player1 = {"name": "Georgesdelajungle"}```
    - ```player2 = {"name": "Aladdin"}```
  - ZetaPush gère le load-balancing entre les 3 noeuds (voir autres US)
  - Je peux visualiser les logs applicatifs de mon service custom mis en production (voir autres US)
  - Je peux consulter la santé des noeuds déployés par ZetaPush mis en production (voir autres US)


### ETQ dev je vérifie l'état des mon application en production

TODO: ne pas se calquer sur une implémentation particulière !

TODO: donner un état global de la santé plutôt (il n'y a pas que les nodeJS, il faudrait peut-être afficher des statistiques/analytics, afficher les logs ou autre information utile)

*GIVEN*
  - J'ai une application en production
  - J'ai l'identification de mon application 'my-first-app'

*WHEN*
  - J'exécute la commande : ```zeta status```

*THEN*
  - Je visualise le nombre de noeuds actifs de mon application
  - Je visualise l'état de chaque noeud

| node1  | node2  | node3  | node4  | node5  |
|---|---|---|---|---|
| Running  | Running  | Pending  | Pending  | Pending |


### ETQ dev je mets à jour mon application en production

TODO: snapshot automatique faite par ZP avant l'upgrade pour backup des données en cas de code foireux ?

TODO: pouvoir skipper snapshot avec --no-snapshot-needed-im-the-best ?





# <a name="parcours-3"></a> Parcours 3 : Mon équipe développe une application front avec ZetaPush sans services custom


## Vue d'ensemble


## User stories


### ETQ exploitant je mets à disposition l'application web pour la qualification avec mes outils habituels


*GIVEN*
  - Mon entreprise a un compte chez ZetaPush (login=dragons@yopmail.com, password=zp-password)
  - Mon entreprise a créé une application dont l'identifiant est `avengers-chat`
  - Mon entreprise a souscrit plusieurs environnements sur ZetaPush (developpement, integration, recette, production) :
    - `dev` pour le développement et les tests
    - `integration` pour l'intégration continue
    - `recette` pour la qualification
    - `prod` pour déployer mon application
  - L'environnement de recette est configuré pour 4 noeuds pour cette application
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


### ETQ exploitant je mets à disposition l'application web pour la qualification avec les outils ZetaPush


### ETQ exploitant je mets à disposition l'application web en production avec mes outils habituels


*GIVEN*
  - Mon entreprise a un compte chez ZetaPush (login=dragons@yopmail.com, password=zp-password)
  - Mon entreprise a créé une application dont l'identifiant est `avengers-chat`
  - Mon entreprise a souscrit plusieurs environnements sur ZetaPush (developpement, integration, recette, production) :
    - `dev` pour le développement et les tests
    - `integration` pour l'intégration continue
    - `recette` pour la qualification
    - `prod` pour déployer mon application
  - L'environnement de production est configuré pour 5 noeuds pour cette application
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



### ETQ exploitant je mets à disposition l'application web en production avec les outils ZetaPush


# <a name="parcours-4"></a> Parcours 4 : Mon équipe développe une application avec ZetaPush et des services custom


## Vue d'ensemble

TODO: est que les services ZetaPush sont partagés en dev ? Risque de se marcher sur les pieds !
TODO: cette vue d'ensemble devrait être mutualisée et il faudrait se concentrer ici sur la partie déploiement uniquement

En phase de développement, chaque développeur travaille en local sur son poste. Il utilise son navigateur préféré ainsi que son nodeJS en local.
Son frontend et ses services custom interagissent avec ZetaPush pour bénéficier des services proposés par ZetaPush afin de lui faire gagner du temps.


Lorsque l'un des développeur a terminé le développement d'une fonctionnalité, il commite son code (sur son Git, SVN ou autre).


L'intégration continue se charge alors de construire l'application.


TODO: tests auto







## User stories

### ETQ exploitant je mets à disposition l'application web avec les services custom pour la qualification avec mes outils habituels


*GIVEN*
  - Mon entreprise a un compte chez ZetaPush (login=dragons@yopmail.com, password=zp-password)
  - Mon entreprise a créé une application dont l'identifiant est `avengers-chat`
  - Mon entreprise a souscrit plusieurs environnements sur ZetaPush (developpement, integration, recette, production) :
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
  - L'environnement de recette est configuré pour 4 noeuds pour cette application
  - L'intégration continue a généré un livrable contenant l'application web (`avengers-chat-front-2.0.1.zip`). Ce livrable est disponible sur un repository privé de l'entreprise.
  - J'ai téléchargé le livrable `avengers-chat-front-2.0.1.zip` sur mon poste (dans `~/avengers-chat`)
  - L'intégration continue a généré un livrable contenant les services custom (`avengers-chat-services-2.0.1.zip`). Ce livrable est disponible sur un repository privé de l'entreprise.
  - J'ai téléchargé le livrable `avengers-chat-services-2.0.1.zip` sur mon poste (dans `~/avengers-chat`)
  - J'ai plusieurs fichiers de configuration pour les différents environnements :
    - ```src/server/environment.yml``` (valeurs par défaut pour le développement directement contenu dans l'archive `avengers-chat-services-2.0.1.zip`) avec le contenu suivant :
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


### ETQ exploitant je mets à disposition l'application web avec les services custom pour la qualification avec les outils ZetaPush


### ETQ exploitant je mets à disposition l'application web avec les services custom en production avec mes outils habituels


*GIVEN*
  - Mon entreprise a un compte chez ZetaPush (login=dragons@yopmail.com, password=zp-password)
  - Mon entreprise a créé une application dont l'identifiant est `avengers-chat`
  - Mon entreprise a souscrit plusieurs environnements sur ZetaPush (developpement, integration, recette, production) :
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
  - L'environnement de production est configuré pour 5 noeuds pour cette application
  - L'intégration continue a généré un livrable contenant l'application web (`avengers-chat-front-2.0.1.zip`). Ce livrable est disponible sur un repository privé de l'entreprise.
  - L'intégration continue a généré un livrable contenant les services custom (`avengers-chat-services-2.0.1.zip`). Ce livrable est disponible sur un repository privé de l'entreprise.
  - La qualification de la version 2.0.1 est terminée et le livrable 2.0.1 est accepté pour être utilisé en production
  - J'ai téléchargé le livrable `avengers-chat-front-2.0.1.zip` sur mon poste (dans `~/avengers-chat`)
  - J'ai téléchargé le livrable `avengers-chat-services-2.0.1.zip` sur mon poste (dans `~/avengers-chat`)
  - J'ai plusieurs fichiers de configuration pour les différents environnements :
    - ```src/server/environment.yml``` (valeurs par défaut pour le développement directement contenu dans l'archive `avengers-chat-services-2.0.1.zip`) avec le contenu suivant :
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

### ETQ exploitant je mets à disposition l'application web avec les services custom en production avec les outils ZetaPush





### ETQ ... j'utilise mon propre domaine existant pour l'hébergement de mon front



### ETQ ... j'utilise mon propre domaine existant pour l'hébergement de mon front en HTTPs

TODO: import du certificat client


---

TODO: gestion des versions
TODO: mise à jour






