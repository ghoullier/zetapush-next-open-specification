# ZetaPush Next Open Specification

> Ce projet contient l'ensemble des ressources relatives à la prochaine version majeure de ZetaPush (aka V3)

Sommaire

- [Objectifs](#objectifs)
- [Schéma de principe](#schemas-de-principe.md)
- [Developer Experience](#developer-experience.md)
- [Profils identifiés](#profils-identifies.md)
- [Je veux du concret : Tutoriel](#tutoriel.md)


# Objectifs

## Objectifs de ZetaPush Celtia

Chez ZetaPush, nous sommes convaincus que le développement logiciel est actuellement trop coûteux et trop long. Les développeurs perdent trop de temps sur des problématiques techniques n'ayant aucune plus-value pour le client final (initialisation du poste de travail, installation, mise en production...).
Nous sommes également convaincus que la réussite d'un projet est extrèmement liée à l'ergonomie de l'application (autrement dit, l'utilisateur est au centre de toutes les décisions).

ZetaPush souhaite donc offrir une expérience de développement agréable et efficace pour une productivité accrue. Nous souhaitons que les développeurs se concentrent sur le code utile. Nous souhaitons également que les développeurs se focalisent sur la partie visible de l'iceberg (l'interface utilisateur - UI) dans le but de répondre efficacement aux besoins grandissants d'ergonomie.


## Objectifs de ce repository

Ce repository github trace nos réflexions, idées et propositions. Nous utilisons ce repository pour communiquer sur nos avancées. Ce repository est aussi la base pour que nos utilisateurs (vous) puissent aussi contribuer en terme de réflextion, d'idées et de propositions. Ce repository est ouvert à tous ceux qui partagent les mêmes convictions que nous.

# Schémas de principe

TODO


# Parcours utilisateurs

Cette section a pour but de présenter l'ensemble des parcours utilisateurs envisagé dans le cadre de ZetaPush V3. Chaque partie correspond à un profil présenté dans [commun.md](./commun.md).

## Developer experience

### Parcours 1 : Je développe une application front avec ZetaPush sans service custom

Mon objectif est de réaliser une application rapidement. Je ne veux pas m'occuper de la partie backend, je souhaite me concentrer sur l'IHM uniquement. Les services proposés par ZetaPush correspondent parfaitement aux besoins de mon applications (ex: gestion des utilisateurs, stockage de données, chat, ...).
Je ne souhaite pas m'occuper de la gestion de mon application en production. Une fois déployée, elle tourne et je ne m'en occupe plus.


- [Démarrage](./1-bootstrap.md#parcours-1)
- Cycle de développement
  - [Développement de fonctionnalité](./2-dev.md#parcours-1)
  - [Debug](./3-debug.md#parcours-1)
  - [Faire des tests](./4-test.md#parcours-1)
- [Build](./5-build.md#parcours-1)
- [Deploiement de l'application](./6-deploy.md#parcours-1)


### Parcours 2 : Je développe une application avec ZetaPush et des services custom

Mon objectif est de réaliser une application rapidement. Certains services proposés par ZetaPush correspondent parfaitement aux besoins de mon applications (ex: gestion des utilisateurs, stockage de données, chat, ...).
Cependant, mon application nécessite une certaine logique métier. Je souhaite donc pouvoir développer rapidement mon code métier. Ce code métier ne peut pas être codé directement dans l'IHM car je souhaite réaliser une application Web, iOS et Android. Il faut donc que ce code métier soit mutualisé (ajout de services custom). Je souhaite que mon code métier soit simple à réaliser et puisse s'appuyer sur les services proposés par ZetaPush (stockage par exemple).
Je ne souhaite pas m'occuper de la gestion de mon application en production. Une fois déployée, elle tourne et je ne m'en occupe plus.

- [Démarrage](./1-bootstrap.md#parcours-2)
- Cycle de développement
  - [Développement de fonctionnalité](./2-dev.md#parcours-2)
  - [Debug](./3-debug.md#parcours-2)
  - [Faire des tests](./4-test.md#parcours-2)
- [Build](./5-build.md#parcours-2)
- [Deploiement de l'application](./6-deploy.md#parcours-2)


### Parcours 3 : Mon équipe développe une application front avec ZetaPush sans services custom

Je travaille dans une entreprise et nous devons développer une application.
L'application peut être développée from scratch mais le coût serait trop élevé.
Nous souhaitons développer rapidement et nous concentrer sur l'IHM et ne pas perdre de temps sur la partie backend.
Les services proposés par ZetaPush correspondent parfaitement aux besoins de cette application (ex: gestion des utilisateurs, stockage de données, chat, ...).
Nous décidons donc d'utiliser ZetaPush pour gérer tout notre backend.

Je ne souhaite pas que ZetaPush nous impose une manière de travailler. Au contraire, je souhaite que ZetaPush s'inscrive dans notre processus de travail habituel :
L'équipe de développement développe des fonctionnalités. Nous disposons d'une Intégration Continue pour builder et packager notre application. Ce livrable généré est ensuite transmis à l'équipe d'exploitation pour être déployée en recette, pré-production ou production. Une fois le déploiement de l'application effectué, c'est cette équipe d'exploitant qui gère la production (monitoring, mises à jour de sécurité, ...). L'équipe d'exploitation souhaite pouvoir connaître la santé de l'application et également avoir des métriques sur les services ZetaPush utilisés (nombre d'appels, nombre de OK, nombre de KO, temps de réponse, ...).

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


### Parcours 4 : Mon équipe développe une application avec ZetaPush et des services custom

Je travaille dans une entreprise et nous devons développer une application.
L'application peut être développée from scratch mais le coût serait trop élevé.
Nous souhaitons développer rapidement et nous concentrer sur l'IHM et ne pas perdre de temps sur la partie backend. Certains services proposés par ZetaPush correspondent parfaitement aux besoins de notre applications (ex: gestion des utilisateurs, stockage de données, chat, ...).
Cependant, notre application nécessite une certaine logique métier. Nous souhaitons donc pouvoir développer rapidement notre code métier. Ce code métier ne peut pas être codé directement dans l'IHM carnous souhaitons réaliser une application Web, iOS et Android. Il faut donc que ce code métier soit mutualisé. Nous souhaitons que notre code métier soit simple à réaliser et puisse s'appuyer sur les services proposés par ZetaPush (stockage par exemple).
Nous décidons donc d'utiliser ZetaPush pour gérer tout notre backend.

Je ne souhaite pas que ZetaPush nous impose une manière de travailler. Au contraire, je souhaite que ZetaPush s'inscrive dans notre processus de travail habituel :
L'équipe de développement développe des fonctionnalités. Nous disposons d'une Intégration Continue pour builder et packager notre application. Ce livrable généré est ensuite transmis à l'équipe d'exploitation pour être déployée en recette, pré-production ou production. Une fois le déploiement de l'application effectué, c'est cette équipe d'exploitant qui gère la production (monitoring, mises à jour de sécurité, ...). L'équipe d'exploitation souhaite pouvoir connaître la santé de l'application et également avoir des métriques sur les services ZetaPush utilisés (nombre d'appels, nombre de OK, nombre de KO, temps de réponse, ...). L'équipe d'exploitation souhaite aussi pouvoir monitorer et suivre le comportement du code métier (services custom développés). Il faut donc qu'ils puissent avoir accès aux métriques des services custom (nombre d'appels, nombre de OK, nombre de KO, temps de réponse, ...) ainsi qu'un accès aux logs produits par les services custom.

Après quelques mois, l'application tourne correctement. Nous souhaitons l'améliorer et corriger les quelques bugs restants. Une nouvelle équipe prend le relais.
Cette nouvelle équipe de développement souhaite pouvoir rapidement remettre un environnement de développement en place. 
Pour déterminer l'origine de certains bugs, cette nouvelle équipe a besoin d'avoir accès aux logs de la production (les logs de l'IHM et les logs des services ZetaPush).

Une fois que les évolutions sont terminés, nous réutilisons notre Intégration Continue pour builder et packager notre application.
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

TODO: à compléter
TODO: reprendre les User Stories de chaque partie

## Profils principaux


### Développeur Front-End

Correspond aux parcours :
- Parcours 1 : Je développe une application front avec ZetaPush sans service custom
- Parcours 3 : Mon équipe développe une application front avec ZetaPush sans services custom

### Développeur Full-Stack

Correspond aux parcours :
- Parcours 2 : Je développe une application avec ZetaPush et des services custom
- Parcours 4 : Mon équipe développe une application avec ZetaPush et des services custom


### Exploitant/Administrateur système

Gestion de la production :
- déploiement
- mise à jour
- monitoring/supervision/alerting


## Autres profils identifiés


### Développeur Back-End (TODO)

TODO: souhaits et rôle d'un dev backend avec ZetaPush ?


### Chef de projet (TODO)

Visibilité sur l'application :
- risques (TODO: pouvoir rassurer un chef de projet sur le choix ZetaPush)
- coûts (TODO: savoir concrètement combien ZetaPush va lui coûter et combien il va économiser)
- planification/avancement du projet (TODO: lien avec ZetaPush ? Visibilité sur la roadmap ZetaPush ?)
- analytics (TODO: remonter des métriques pour que le chef de projet puisse savoir comment son application est utilisée : le nombre d'utilisateurs, parcours clients, ...)
- dashboard projet (TODO: vision complète)

### Commercial (TODO)

- évaluation des risques (TODO: pouvoir rassurer un chef de projet sur le choix ZetaPush)
- évaluation des coûts (TODO: savoir concrètement combien ZetaPush va lui coûter et combien il va économiser)

### CEO (TODO)

- évaluation des risques (TODO: pouvoir rassurer un chef de projet sur le choix ZetaPush)
- évaluation des coûts (TODO: savoir concrètement combien ZetaPush va lui coûter et combien il va économiser)


### CTO (TODO)

- évaluation des services proposés (matching avec le besoin fonctionnel)

### Client final (TODO)


- analytics (TODO: remonter des métriques pour que le chef de projet puisse savoir comment son application est utilisée : le nombre d'utilisateurs, parcours clients, ...)
- suivi de l'application en production
- monitoring

# Tutoriel

TODO: chat