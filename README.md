# ZetaPush Next Open Specification

> Ce projet contient l'ensemble des ressources relatives à la prochaine version majeure de ZetaPush (aka Celtia)

Sommaire

- [Objectifs](#objectifs)
- [Vocabulaire](#vocabulaire)
- [Schéma de principe](#schemas-de-principe)
- [Developer Experience](#parcours-utilisateurs)
- [Profils identifiés](#profils-identifies)
- [Roadmap](#roadmap)
- [Je veux du concret : Tutoriel](#tutoriels)


# Objectifs

## Objectifs de ZetaPush Celtia

Chez ZetaPush, nous sommes convaincus que le développement logiciel est actuellement trop coûteux et trop long. Les développeurs perdent trop de temps sur des problématiques techniques n'ayant aucune plus-value pour le client final (initialisation du poste de travail, installation, mise en production...).
Nous sommes également convaincus que la réussite d'un projet est extrêmement liée à l'ergonomie de l'application (autrement dit, l'utilisateur est au centre de toutes les décisions).

ZetaPush souhaite donc offrir une expérience de développement agréable et efficace pour une productivité accrue. Nous souhaitons que les développeurs se concentrent sur le code utile. Nous souhaitons également que les développeurs se focalisent sur la partie visible de l'iceberg (l'interface utilisateur - UI) dans le but de répondre efficacement aux besoins grandissants d'ergonomie.


## Objectifs de ce repository

Ce repository github trace nos réflexions, idées et propositions. Nous utilisons ce repository pour communiquer sur nos avancées. Ce repository est aussi la base pour que nos utilisateurs (vous) puissent aussi contribuer en terme de réflexion, d'idées et de propositions. Ce repository est ouvert à tous ceux qui partagent les mêmes convictions que nous.


# Vocabulaire

* ETQ : En tant que
* dev : Terme générique pour dire dev front / back ou fullstack
* ZP : ZetaPush

## Services

Afin de bien comprendre les différents services que ZetaPush fournit, petite précision sur le nommage :

|          Nom           |                                                                                                                                                        Description                                                                                                                                                        |
| :--------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|    _Cloud service_     |                                                                          Classe regroupant un ensemble de _cloud functions_ du même domaine fournie par ZetaPush. Par exemple nous avons un _cloud service_ pour le chat, un autre pour la gestion d'utilisateurs...                                                                           |
|    _Cloud function_    |                                       Méthode d'une classe. Cela correspond à une fonction appelable via un _cloud service_. Par exemple dans le _cloud service_ de gestion des utilisateurs, nous avons les _cloud functions_ suivantes : `createUser()` / `createOrganization()`.                                       |
| _Custom cloud service_ | Correspond exactement à la même chose qu'un _cloud service_. La seule différence est que c'est le développeur qui l'a créé. Une fois déployé, le _custom cloud service_ est appelable de la même manière qu'un _cloud service_. Il inclut lui aussi un ensemble de _cloud functions_ que le développeur a défini lui même |

À noter que par abus de langage, nous parlerons parfois seulement de _service_ et de _function_ suivant le contexte si cela ne porte pas à confusion.


# Schémas de principe

ZetaPush propose un ensemble de _cloud services_ dont l'objectif est de répondre aux usages standards/habituels.
Ces services ont pour but de répondre à vos besoins pour la plupart des situations et donc de vous laissez vous concentrer sur la partie UI/UX (interface utilisateur/ergonomie) :

![Développement avec seulement les _cloud services_ ZetaPush](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/principes-phase-dev-utilise-cloud-services.html)



Fournir des services prêts à l'emploi ne suffisent pas toujours. Il existe deux formes de situations non couvertes :
- Vous souhaitez utiliser un _cloud service_ mais celui-ci ne répond que partiellement à votre besoin
- Aucun des _cloud services_ fournis par ZetaPush n'est adapté à l'un de vos besoins spécifiques

Dans le premier cas, nous offrons la possibilité de configurer ou d'étendre les _cloud services_ existants pour les adapter à vos besoins.
Dans le second cas, nous vous permettons de développer vos propres _cloud services custom_.

![Développement avec seulement les _cloud services_ ZetaPush](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/principes-phase-dev-custom-cloud-services.html)


Au delà de la partie développement de votre application, ZetaPush se charge également de l'hébergement :

![Développement avec seulement les _cloud services_ ZetaPush](https://exp.draw.io/ImageExport4/export?url=https://raw.githubusercontent.com/zetapush/zetapush-next-open-specification/master/schemas/principes-prod.html)


ZetaPush n'impose aucun pré-requis technique. Nous souhaitons que vous puissiez utiliser les technologies avec lesquelles vous êtes les plus à l'aise. De même, ZetaPush se refuse d'impacter vos processus de travail mais cherche au contraire à s'adapter à votre workflow de travail.


# Parcours utilisateurs

Cette section a pour but de présenter l'ensemble des parcours utilisateurs envisagés dans le cadre de ZetaPush V3. Chaque partie correspond à un profil présenté [ci-dessous](#profils-identifies).

## Developer experience

### ![Parcours 1](https://img.shields.io/badge/parcours-dev%20front-00d0ff.svg) : Je développe une application front avec ZetaPush sans _custom cloud service_

Mon objectif est de réaliser une application rapidement. Je ne veux pas m'occuper de la partie backend, je souhaite me concentrer sur l'IHM uniquement. Les services proposés par ZetaPush correspondent parfaitement aux besoins de mon application (ex: gestion des utilisateurs, stockage de données, chat, ...).
Je ne souhaite pas m'occuper de la gestion de mon application en production. Une fois déployée, elle tourne et je ne m'en occupe plus.


- [Démarrage](./1-bootstrap.md#parcours-1)
- Cycle de développement
  - [Développement de fonctionnalité](./2-dev.md#parcours-1)
  - [Debug](./3-debug.md#parcours-1)
  - [Faire des tests](./4-test.md#parcours-1)
- [Build](./5-build.md#parcours-1)
- [Deploiement de l'application](./6-deploy.md#parcours-1)


### ![Parcours 2](https://img.shields.io/badge/parcours-dev%20full--stack-00d0ff.svg) : Je développe une application avec ZetaPush et des _custom cloud services_

Mon objectif est de réaliser une application rapidement. Certains services proposés par ZetaPush correspondent parfaitement aux besoins de mon application (ex: gestion des utilisateurs, stockage de données, chat, ...).
Cependant, mon application nécessite une certaine logique métier. Je souhaite donc pouvoir développer rapidement mon code métier. Ce code métier ne peut pas être codé directement dans l'IHM car je souhaite réaliser une application Web, iOS et Android. Il faut donc que ce code métier soit mutualisé (ajout de _custom cloud services_). Je souhaite que mon code métier soit simple à réaliser et puisse s'appuyer sur les services proposés par ZetaPush (stockage par exemple).
Je ne souhaite pas m'occuper de la gestion de mon application en production. Une fois déployée, elle tourne et je ne m'en occupe plus.

- [Démarrage](./1-bootstrap.md#parcours-2)
- Cycle de développement
  - [Développement de fonctionnalité](./2-dev.md#parcours-2)
  - [Debug](./3-debug.md#parcours-2)
  - [Faire des tests](./4-test.md#parcours-2)
- [Build](./5-build.md#parcours-2)
- [Deploiement de l'application](./6-deploy.md#parcours-2)


### ![Parcours 3](https://img.shields.io/badge/parcours-équipe%20front-00d0ff.svg) : Mon équipe développe une application front avec ZetaPush sans _custom cloud service_

Je travaille dans une entreprise et nous devons développer une application.
L'application peut être développée from scratch mais le coût serait trop élevé.
Nous souhaitons développer rapidement et nous concentrer sur l'IHM et ne pas perdre de temps sur la partie backend.
Les services proposés par ZetaPush correspondent parfaitement aux besoins de cette application (ex: gestion des utilisateurs, stockage de données, chat, ...).
Nous décidons donc d'utiliser ZetaPush pour gérer tout notre backend.

Je ne souhaite pas que ZetaPush nous impose une manière de travailler. Au contraire, je souhaite que ZetaPush s'inscrive dans notre processus de travail habituel :
L'équipe de développement développe des fonctionnalités. Nous disposons d'une Intégration Continue pour builder et packager notre application. Ce livrable généré est ensuite transmis à l'équipe d'exploitation pour être déployée en recette, pré-production ou production. Une fois le déploiement de l'application effectué, c'est habituellement cette équipe d'exploitant qui gère la production (monitoring, mises à jour de sécurité, ...). L'équipe d'exploitation souhaite pouvoir connaître la santé de l'application et également avoir des métriques sur les services ZetaPush utilisés (nombre d'appels, nombre de OK, nombre de KO, temps de réponse, ...).

Après quelques mois, l'application tourne correctement. Nous souhaitons l'améliorer et corriger les quelques bugs restants. Une nouvelle équipe prend le relais.
Cette nouvelle équipe de développement souhaite pouvoir rapidement remettre un environnement de développement en place. 
Pour déterminer l'origine de certains bugs, cette nouvelle équipe a besoin d'avoir accès aux logs de la production (les logs de l'IHM et les logs des services ZetaPush).


- [Démarrage](./1-bootstrap.md#parcours-3)
- Cycle de développement
  - [Développement de fonctionnalité](./2-dev.md#parcours-3)
  - [Debug](./3-debug.md#parcours-3)
  - [Faire des tests](./4-test.md#parcours-3)
- [Build](./5-build.md#parcours-3)
- [Deploiement de l'application](./6-deploy.md#parcours-3)
- [Des membres de mon équipe gèrent la production](./7-exploitation.md#parcours-3)
- [Une nouvelle équipe reprend la suite du développement](./8-evolution.md#parcours-3)


### ![Parcours 4](https://img.shields.io/badge/parcours-équipe%20full--stack-00d0ff.svg) : Mon équipe développe une application avec ZetaPush et des _custom cloud services_

Je travaille dans une entreprise et nous devons développer une application.
L'application peut être développée from scratch mais le coût serait trop élevé.
Nous souhaitons développer rapidement et nous concentrer sur l'IHM et ne pas perdre de temps sur la partie backend. Certains services proposés par ZetaPush correspondent parfaitement aux besoins de notre application (ex: gestion des utilisateurs, stockage de données, chat, ...).
Cependant, notre application nécessite une certaine logique métier. Nous souhaitons donc pouvoir développer rapidement notre code métier. Ce code métier ne peut pas être codé directement dans l'IHM carnous souhaitons réaliser une application Web, iOS et Android. Il faut donc que ce code métier soit mutualisé. Nous souhaitons que notre code métier soit simple à réaliser et puisse s'appuyer sur les services proposés par ZetaPush (stockage par exemple).
Nous décidons donc d'utiliser ZetaPush pour gérer tout notre backend.

Je ne souhaite pas que ZetaPush nous impose une manière de travailler. Au contraire, je souhaite que ZetaPush s'inscrive dans notre processus de travail habituel :
L'équipe de développement développe des fonctionnalités. Nous disposons d'une Intégration Continue pour builder et packager notre application. Ce livrable généré est ensuite transmis à l'équipe d'exploitation pour être déployée en recette, pré-production ou production. Une fois le déploiement de l'application effectué, c'est habituellement cette équipe d'exploitant qui gère la production (monitoring, mises à jour de sécurité, ...). L'équipe d'exploitation souhaite pouvoir connaître la santé de l'application et également avoir des métriques sur les services ZetaPush utilisés (nombre d'appels, nombre de OK, nombre de KO, temps de réponse, ...). L'équipe d'exploitation souhaite aussi pouvoir monitorer et suivre le comportement du code métier (services custom développés). Il faut donc qu'ils puissent avoir accès aux métriques des services custom (nombre d'appels, nombre de OK, nombre de KO, temps de réponse, ...) ainsi qu'un accès aux logs produits par les services custom.

Après quelques mois, l'application tourne correctement. Nous souhaitons l'améliorer et corriger les quelques bugs restants. Une nouvelle équipe prend le relais.
Cette nouvelle équipe de développement souhaite pouvoir rapidement remettre un environnement de développement en place. 
Pour déterminer l'origine de certains bugs, cette nouvelle équipe a besoin d'avoir accès aux logs de la production (les logs de l'IHM et les logs des services ZetaPush).

Une fois que les évolutions sont terminées, nous réutilisons notre Intégration Continue pour builder et packager notre application.
L'équipe d'exploitant 


- [Démarrage](./1-bootstrap.md#parcours-4)
- Cycle de développement
  - [Développement de fonctionnalité](./2-dev.md#parcours-4)
  - [Debug](./3-debug.md#parcours-4)
  - [Faire des tests](./4-test.md#parcours-4)
- [Build](./5-build.md#parcours-4)
- [Deploiement de l'application](./6-deploy.md#parcours-4)
- [Des membres de mon équipe gèrent la production](./7-exploitation.md#parcours-4)
- [Une nouvelle équipe reprend la suite du développement](./8-evolution.md#parcours-4)




# Profils identifiés


Ensemble des profils analysés dans le cadre de ZetaPush V3 avec leur nommage dans l'ensemble du projet.

|                Profil                 |    Nommage    | Description                           | Parcours correspondants                    |
| :-----------------------------------: | :-----------: | ------------------------------------- | ------------------------------------------ |
|         Développeur Front-End         |   dev front   |                                       | <ul><li>**Parcours 1** : Je développe une application front avec ZetaPush sans service custom</li><li>**Parcours 3** : Mon équipe développe une application front avec ZetaPush sans service custom</li></ul> |
|         Développeur Back-End          |   dev back    | TODO: souhaits et rôle d'un dev backend avec ZetaPush ? | <ul><li>**Parcours 2** : Je développe une application avec ZetaPush et des services custom</li><li>**Parcours 4** : Mon équipe développe une application avec ZetaPush et des services custom</li></ul> |
|        Développeur Full-Stack         | dev fullstack |                                       | <ul><li>**Parcours 1** : Je développe une application front avec ZetaPush sans service custom</li><li>**Parcours 2** : Je développe une application avec ZetaPush et des services custom</li><li>**Parcours 3** : Mon équipe développe une application front avec ZetaPush sans service custom</li><li>**Parcours 4** : Mon équipe développe une application avec ZetaPush et des services custom</li></ul> |
| Opérationnel / Administrateur système |      ops      | Gestion de la production :<ul><li>déploiement</li><li>mise à jour</li><li>monitoring/supervision/alerting</li></ul>
|            Chef de projet             |      CP       | Visibilité sur l'application :<ul><li>risques (TODO: pouvoir rassurer un chef de projet sur le choix ZetaPush)</li><li>coûts (TODO: savoir concrètement combien ZetaPush va lui coûter et combien il va économiser)</li><li>planification/avancement du projet (TODO: lien avec ZetaPush ? Visibilité sur la roadmap ZetaPush ?)</li><li>analytics (TODO: remonter des métriques pour que le chef de projet puisse savoir comment son application est utilisée : le nombre d'utilisateurs, parcours clients, ...)</li><li>dashboard projet (TODO: vision complète)</li></ul> |                                            |
|              Commercial               |  commercial   | <ul><li>évaluation des risques (TODO: pouvoir rassurer un chef de projet sur le choix ZetaPush)</li><li>évaluation des coûts (TODO: savoir concrètement combien ZetaPush va lui coûter et combien il va économiser)</li></ul> |                                            |
|                  CEO                  |      CEO      | <ul><li>évaluation des risques (TODO: pouvoir rassurer un chef de projet sur le choix ZetaPush)</li><li>évaluation des coûts (TODO: savoir concrètement combien ZetaPush va lui coûter et combien il va économiser)</li></ul>  |                                            |
|                  CTO                  |      CTO      | <ul><li>évaluation des services proposés (matching avec le besoin fonctionnel)</li></ul> |                                            |
|        Client final d'une ESN         |    client     | <ul><li>analytics (TODO: remonter des métriques pour que le chef de projet puisse savoir comment son application est utilisée : le nombre d'utilisateurs, parcours clients, ...)</li><li>suivi de l'application en production</li><li>monitoring</li></ul> |                                            |


# Roadmap

## ![celtia-alpha-1](https://img.shields.io/badge/milestone-celtia--alpha--1-blue.svg) ![progress](http://progressed.io/bar/10)

###       ![Parcours 1](https://img.shields.io/badge/parcours-dev%20front-00d0ff.svg) ![progress](http://progressed.io/bar/10)

       **Je développe une application front avec ZetaPush sans _custom cloud service_**



####             Démarrage ![progress](http://progressed.io/bar/10)

> - [ ] [**[P01-BOOT05] ETQ dev front j'utilise les Cloud Services dans mon application existante avec la CLI en utilisant mon compte ZetaPush**](./1-bootstrap.md#P01-BOOT05)
>   - [ ] Rédiger les specs
>   - [ ] Implémenter la gestion de `npm init @zetapush`
> - [ ] [**[P01-BOOT06] ETQ dev front j'utilise les Cloud Services dans mon application existante et une arborescence custom avec la CLI en utilisant mon compte ZetaPush**](./1-bootstrap.md#P01-BOOT06)
>   - [ ] Rédiger les specs
>   - [ ] Implémenter la gestion de `npm init @zetapush` avec un mapping custom


####             Développement ![progress](http://progressed.io/bar/10)

> - [ ] [**[P01-DEV01] ETQ dev front j'utilise un _cloud service_ et j'ai une réponse en retour**](./2-dev.md#P01-DEV01)
>   - [X] Rédiger les specs
>   - [ ] Documenter la création manuelle de compte via la console
>   - [ ] Documenter l'appel de _cloud service_ ZetaPush
>   - [ ] Lien vers la documentation de référence vers les _cloud service_ ZetaPush
>   - [ ] Documenter l'organisation de la documentation de référence actuelle
> - [ ] [**[P01-DEV02] ETQ dev front j'utilise un _cloud service_ et j'ai une erreur en retour**](./2-dev.md#P01-DEV02)
>   - [X] Rédiger les specs
> - [ ] [**[P01-DEV06] ETQ dev front j'utilise un _cloud service_ et j'ai une réponse en retour et je n'ai pas encore de compte ZetaPush**](./2-dev.md#P01-DEV06)
>   - [ ] Rédiger les specs
>   - [ ] Documenter l'initialisation du SDK
>   - [ ] Console : parcours de création de compte
>   - [ ] Console : parcours d'engistrement d'application
>   - [ ] SDK JS : afficher un message dans la console du navigateur


####             Debug ![progress](http://progressed.io/bar/100)

> Hors scope dans 'celtia-alpha-1'

####             Test ![progress](http://progressed.io/bar/100)

> Hors scope dans 'celtia-alpha-1'

####             Build ![progress](http://progressed.io/bar/100)

> Hors scope dans 'celtia-alpha-1'

####             Déploiement ![progress](http://progressed.io/bar/10)

> - [ ] [**[P01-DEPLOY01] ETQ dev front je déploie mon application en production**](./6-deploy.md#P01-DEPLOY01)
>   - [ ] Rédiger les specs
>   - [ ] Implémenter `zeta push --front`
>   - [ ] `zeta push` appelle automatiquement `zeta register` si besoin
>   - [ ] Implémenter l'hébergement du front
>   - [ ] Afficher la progression du déploiement



###       ![Parcours 2](https://img.shields.io/badge/parcours-dev%20full--stack-00d0ff.svg) ![progress](http://progressed.io/bar/10)

       **Je développe une application avec ZetaPush et des _custom cloud services_**

####             Démarrage ![progress](http://progressed.io/bar/10)

> - [ ] [**[P02-BOOT01] ETQ dev full-stack je créé une application sans CLI en utilisant mon compte ZetaPush**](./1-bootstrap.md#P02-BOOT01)
>   - [ ] Rédiger les specs
>   - [ ] Documenter le démarrage manuel
> - [ ] [**[P02-BOOT02] ETQ dev full-stack j'ajoute des Cloud Services et je créé des Custom Cloud Services au sein d'une application existante**](./1-bootstrap.md#P02-BOOT02)
>   - [ ] Rédiger les specs
>   - [ ] Documenter le démarrage manuel
> - [ ] [**[P02-BOOT06] ETQ dev full-stack j'ajoute des _Custom Cloud Services_ au sein d'une application existante avec la CLI en utilisant mon compte ZetaPush**](./1-bootstrap.md#P02-BOOT06)
>   - [ ] Rédiger les specs
>   - [ ] Implémenter la gestion de `npm init @zetapush`


####             Développement ![progress](http://progressed.io/bar/10)

> - [ ] [**[P02-DEV01] ETQ dev full-stack je développe sur mon environement local mon code métier dans une custom cloud function**](./2-dev.md#P02-DEV01)
>   - [ ] Rédiger les specs
>   - [ ] Implémenter la commande `zeta run`
>   - [ ] `zeta run` appelle automatiquement `zeta register` si besoin
>   - [ ] Implémenter la commande `zeta register`
>   - [ ] Décrire `zeta run` dans l'aide
>   - [ ] Documenter la commande `zeta run`
>   - [ ] Démarrer et configurer les _cloud services_ demandés
> - [ ] [**[P02-DEV02] ETQ dev full-stack j'utilise un _custom cloud service_ et j'ai une réponse en retour**](./2-dev.md#P02-DEV02)
>   - [ ] Rédiger les specs
>   - [ ] Documenter le développement d'un _custom cloud service_
>   - [ ] Documenter l'appel d'un _cloud service_ existant depuis un _custom cloud service_
> - [ ] [**[P02-DEV03] ETQ dev full-stack j'utilise un _custom cloud service_ et j'ai une erreur en retour**](./2-dev.md#P02-DEV03)
>   - [ ] Rédiger les specs

####             Debug ![progress](http://progressed.io/bar/100)

> Hors scope dans 'celtia-alpha-1'

####             Test ![progress](http://progressed.io/bar/100)

> Hors scope dans 'celtia-alpha-1'

####             Build ![progress](http://progressed.io/bar/100)

> Hors scope dans 'celtia-alpha-1'

####             Déploiement ![progress](http://progressed.io/bar/10)

> - [ ] [**[P02-DEPLOY01] ETQ dev full-stack je déploie mes services custom en production**](./6-deploy.md#P02-DEPLOY01)
>   - [ ] Rédiger les specs
>   - [ ] Implémenter `zeta push --worker`
>   - [X] Implémenter l'hébergement du worker
>   - [X] Afficher la progression du déploiement
>   - [ ] Documenter l'utilisation des _custom cloud services_ nouvellement déployés
> - [ ] [**[P02-DEPLOY02] ETQ dev full-stack je déploie mon application (front et service custom) en production**](./6-deploy.md#P02-DEPLOY02)
>   - [ ] Rédiger les specs
>   - [ ] Implémenter `zeta push`
>   - [ ] Afficher la progression du déploiement
> - [ ] [**[P02-DEPLOY06] ETQ dev je mets à jour mon application en production**](./6-deploy.md#P02-DEPLOY06)
>   - [ ] Rédiger les specs
>   - [ ] Implémenter `zeta push` pour mettre à jour le code
>   - [ ] Afficher la progression de la mise à jour
> - [ ] [**[P02-DEPLOY07] ETQ dev full-stack je sais lorsque mon worker n'a pas démarré**](./6-deploy.md#P02-DEPLOY07)
>   - [ ] Rédiger les specs
>   - [ ] Afficher un message d'aide

###       ![Parcours 3](https://img.shields.io/badge/parcours-équipe%20front-00d0ff.svg) ![progress](http://progressed.io/bar/10)


###       ![Parcours 4](https://img.shields.io/badge/parcours-équipe%20full--stack-00d0ff.svg) ![progress](http://progressed.io/bar/10)


---

## ![celtia-alpha-2](https://img.shields.io/badge/milestone-celtia--alpha--2-lightgrey.svg) ![progress](http://progressed.io/bar/0)

TODO

###       ![Parcours 1](https://img.shields.io/badge/parcours-dev%20front-00d0ff.svg) ![progress](http://progressed.io/bar/10)

       **Je développe une application front avec ZetaPush sans _custom cloud service_**


####             Démarrage ![progress](http://progressed.io/bar/10)

> - [ ] [**[P01-BOOT01] ETQ dev front je créé une application sans CLI en utilisant mon compte ZetaPush**](./1-bootstrap.md#P01-BOOT01)
>   - [ ] Rédiger les specs
>   - [ ] Documenter le démarrage manuel
> - [ ] [**[P01-BOOT02] ETQ dev front j'utilise les _Cloud Services_ dans mon application existante sans CLI en utilisant mon compte ZetaPush**](./1-bootstrap.md#P01-BOOT02)
>   - [ ] Rédiger les specs
>   - [ ] Documenter le démarrage manuel


---

## ![celtia-beta-1](https://img.shields.io/badge/milestone-celtia--beta--1-lightgrey.svg) ![progress](http://progressed.io/bar/0)

TODO

---

## ![celtia-beta-2](https://img.shields.io/badge/milestone-celtia--beta--2-lightgrey.svg) ![progress](http://progressed.io/bar/0)

TODO


# Tutoriels

- [Avengers Chat](./0-tutorial.md)
