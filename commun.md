# Objectif

Dans ce document, les différentes informations récurrentes ou répétitives seront présentées.

## Profils

Ensemble des profils analysés dans le cadre de ZetaPush V3 avec leur nommage dans l'ensemble du projet.

|                Profil                 |    Nommage    |
| :-----------------------------------: | :-----------: |
|         Développeur Front-End         |   dev front   |
|         Développeur Back-End          |   dev back    |
|        Développeur Full-Stack         | dev fullstack |
| Opérationnel / Administrateur système |      ops      |
|            Chef de projet             |      CP       |
|              Commercial               |  commercial   |
|                  CEO                  |      CEO      |
|                  CTO                  |      CTO      |
|        Client final d'une ESN         |    client     |

## Vocabulaire

* ETQ : En tant que
* dev : Terme générique pour dire dev front / back ou fullstack
* ZP : ZetaPush

### Services

Afin de bien comprendre les différents services que ZetaPush fournit, petite précision sur le nommage :

|          Nom           |                                                                                                                                                        Description                                                                                                                                                        |
| :--------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|    _Cloud service_     |                                                                          Classe regroupant un ensemble de _cloud functions_ du même domaine fournie par ZetaPush. Par exemple nous avons un _cloud service_ pour le chat, un autre pour la gestion d'utilisateurs...                                                                           |
|    _Cloud function_    |                                       Méthode d'une classe. Cela correspond à une fonction appelable via un _cloud service_. Par exemple dans le _cloud service_ de gestion des utilisateurs, nous avons les _cloud functions_ suivantes : `createUser()` / `createOrganization()`.                                       |
| _Custom cloud service_ | Correspond exactement à la même chose qu'un _cloud service_. La seule différence est que c'est le développeur qui l'a créé. Une fois déployé, le _custom cloud service_ est appelable de la même manière qu'un _cloud service_. Il inclut lui aussi un ensemble de _cloud functions_ que le développeur a défini lui même |

À noter que par abus de langage, nous parlerons parfois seulement de _service_ et de _function_ suivant le contexte si cela ne porte pas à confusion.