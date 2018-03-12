# Objectifs

- Un développeur web doit pouvoir développer son front en utilisant les services ZetaPush et sans être obligé de développer de code backend spécifique. Il doit pouvoir déployer son front sur ZetaPush.
- Un développeur web doit pouvoir coder son propre métier pour simplifier le développement de son/ses front(s). Il doit pouvoir déployer son backend custom sur ZetaPush.
- Un développeur web ayant un front et un backend custom doit pouvoir déployer son application sur ZetaPush (front et backend custom)


Les profils utilisés sont définis dans [commun.md](./commun.md).

# Pré-requis

J'ai un compte sur ZetaPush :
- je fourni mon login/password ou API key/token dans un fichier d'environnement
- j'indique l'identifiant de l'application que je vais déployer

Mon application est prête à être déployée :
- utilisation des outils standard pour builder mon front et générer un dossier www
- utilisation des outils standard pour builder mon backend custom (contenant le métier dédié à mon/mes front(s))



# Parcours 1 : développement rapide (backend custom)

## Vue d'ensemble

J'ai développé sur ma machine avec mon propre NodeJS qui interagit avec ZetaPush.

![Développement local](https://github.com/zetapush/zetapush-next-open-specification/raw/master/schemas/phase-developpement.png)

Mon application est prête à partir en production. Je la déploie depuis mon poste.

![Déploiement en production](https://github.com/zetapush/zetapush-next-open-specification/raw/master/schemas/deploiement-prod-simple.png)


## User stories

### ETQ dev je déploie mon backend en production

*GIVEN*
- J'ai un compte sur ZetaPush (login=jeni@yopmail.com, password=zp-password)
- J'ai l'identifiant de mon application (my-first-app)
- J'ai un seul environnement fourni par ZetaPush
- Mon backend fourni un service custom avec les fonctions suivantes :
  - ```createGame(player1, player2)```
  - ```gameAction(player, name, args)```
  - ```isFinished()```
  - ```getWinner()```
  - ```endGame()```
- J'ai buildé mon backend via npm et le résultat est disponible dans le dossier dist/server
- ZetaPush me met à disposition 3 noeuds en production et je n'ai rien configuré

*WHEN*
- J'exécute la commande : ```zeta push --server-only```

*THEN*
- Le code présent dans dist/server est envoyé sur ZetaPush
- Je vois l'état d'avancement du déploiement global
- Je sais lorsque mon application est prête à être utilisée
- Je peux utiliser mon frontend pour interagir avec mon backend de production
- Je peux appeler la fonction `createGame` de mon service custom directement depuis mon frontend via le SDK JS ZetaPush avec les paramètres suivants :
  - ```player1 = {"name": "Georgesdelajungle"}```
  - ```player2 = {"name": "Aladdin"}```
- ZetaPush gère le load-balancing entre les 3 noeuds
- Je peux visualiser les logs applicatifs de mon backend custom
- Je peux consulter la santé des noeuds déployés par ZetaPush


### ETQ dev je déploie mon backend en production avec une configuration dédié à cet environnement avec les credentials externalisés


*GIVEN*
- J'ai un compte sur ZetaPush (login=jeni@yopmail.com, password=zp-password)
- J'ai l'identifiant de mon application (my-first-app)
- J'ai deux environnements fournis par ZetaPush : 
  - `dev` pour le développement et les tests
  - `prod` pour déployer mon application
- J'ai les tokens pour chaque environnement (fournis par ZetaPush) :
  - `dev` : 1234
  - `prod` : 456789
- Mon backend fourni un service custom avec les fonctions suivantes :
  - ```createGame(player1, player2)```
  - ```gameAction(player, name, args)```
  - ```isFinished()```
  - ```getWinner()```
  - ```endGame()```
- J'ai buildé mon backend via npm et le résultat est disponible dans le dossier dist/server
- ZetaPush me met à disposition 3 noeuds en production et je n'ai rien configuré
- J'ai plusieurs fichiers de configuration pour mes différents environnements :
  - ```~/.zpcredentials/my-first-app/dev.yml``` :
    ```yml
      zp-token: '1234'
    ```
  - ```~/.zpcredentials/my-first-app/prod.yml``` :
    ```yml
      zp-token: '456789'
    ```
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
- Je ne précise aucun configuration concernant l'emplacement de mes fichiers (utilisation de la convention ZetaPush)

*WHEN*
- J'exécute la commande : ```zeta push --server-only --prod```

*THEN*
- Le code présent dans dist/server est envoyé sur ZetaPush en utilisant les credentials de production (`zp-token=456789`)
- Je vois l'état d'avancement du déploiement global
- Je sais lorsque mon application est prête à être utilisée
- Mon application est correctement configurée pour utiliser l'environnement de prod :
  ```yml
  stripe:
      url: 'https://api.stripe.com'
      token: 'sk_prod_dNuiVQyTlDMH5RdFYSD4nIV0'
  ```
- Je peux utiliser mon frontend pour interagir avec mon backend de production
- Je peux appeler la fonction `createGame` de mon service custom directement depuis mon frontend via le SDK JS ZetaPush avec les paramètres suivants :
  - ```player1 = {"name": "Georgesdelajungle"}```
  - ```player2 = {"name": "Aladdin"}```
- ZetaPush gère le load-balancing entre les 3 noeuds
- Je peux visualiser les logs applicatifs de mon backend custom mis en production
- Je peux consulter la santé des noeuds déployés par ZetaPush mis en production



### ETQ dev je déploie mon front en production


### ETQ dev je déploie mon application (front et backend) en production





# Parcours 2 : Intégration continue (backend custom)




# Parcours 3 : Déploiement continu (backend custom)





--
getsion des versions
mise à jour
