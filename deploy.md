# Objectifs

- Un développeur web doit pouvoir développer son front en utilisant les services ZetaPush et sans être obligé de développer de code backend spécifique. Il doit pouvoir déployer son front sur ZetaPush.
- Un développeur web doit pouvoir coder son propre métier pour simplifier le développement de son/ses front(s). Il doit pouvoir déployer son backend custom sur ZetaPush.
- Un développeur web ayant un front et un backend custom doit pouvoir déployer son application sur ZetaPush (front et backend custom)

# Vocabulaire

- ETQ : En tant que 


# Profils identifiés

- Développeur seul (sera nommé par la suite 'dev')
- Equipe de développement (sera nommé par la suite 'équipe')
- Personne dédié à la gestion de la production (sera nommé par la suite 'ops')

# Pré-requis

J'ai un compte sur ZetaPush :
- je fourni mon login/password ou API key/token dans un fichier d'environnement
- j'indique l'identifiant de l'application que je vais déployer

Mon application est prête à être déployée :
- utilisation des outils standard pour builder mon front et générer un dossier www
- utilisation des outils standard pour builder mon backend custom (contenant le métier dédié à mon/mes front(s))



# Process 1 : développement rapide (backend custom)

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
  - Mon backend fourni un service customl avec les fonctions suivantes :
    - ```createGame(player1, player2)```
    - ```gameAction(player, name, args)```
    - ```isFinished()```
    - ```getWinner()```
    - ```endGame()```
  - J'ai buildé mon backend via npm et le résultat est disponible dans le dossier dist/server
  - J'ai indiqué que je souhaitais utiliser tous les noeuds à disposition en production (3)

*WHEN*
  - J'exécute la commande : ```zeta push```

*THEN*
  - Le code présent dans dist/server est envoyé sur ZetaPush
  - Je vois l'état d'avancement du déploiement
  - Je sais lorsque mon application est prête à être utilisée
  - Je peux utiliser mon frontend pour interagir avec mon backend de production
  - Je peux appeler la fonction `createGame` de mon service custom directement depuis mon frontend via le SDK JS ZetaPush avec les paramètres suivants :
    - ```player1 = {"name": "Georgesdelajungle"}```
    - ```player2 = {"name": "Aladdin"}```


### ETQ dev je déploie mon backend en production avec une configuration dédié à cet environnement


### ETQ dev je déploie mon front en production


### ETQ dev je déploie mon application (front et backend) en production





# Process 2 : Intégration continue (backend custom)




# Process 3 : Déploiement continu (backend custom)





--
getsion des versions
mise à jour
