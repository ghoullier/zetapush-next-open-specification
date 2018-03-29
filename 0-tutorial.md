# Créer un chat temps-réel avec ZetaPush

## Sommaire

1. [Introduction](#introduction)
2. [Préparation de l'environnement](#préparation-de-lenvironnement)
3. [Initialisation du projet](#initialisation-du-projet)
4. [Création du design de l'application](#création-du-design-de-lapplication)
5. [Utilisation des _cloud services_](#utilisation-des-cloud-services)
6. [Déploiement de l'application](#déploiement-de-lapplication)
7. [Développement back avec ZetaPush](#développement-back-avec-zetapush)
8. [Utilisation d'un _custom cloud service_](#utilisation-dun-custom-cloud-service)
9. [Conclusion](#conclusion)

## Introduction

### Objectif

L'objectif de ce tutoriel est de construire une application de chat en utilisant ZetaPush depuis le démarrage du projet jusqu'à son déploiement.
Pour ceci tu vas découvrir comment utiliser les _cloud services_ de ZetaPush (chat, gestion des utilisateurs). Ensuite, tu vas voir comment étendre toi même ces services pour développer les fonctionnalités précises que tu souhaites.

### Pré-requis

Pour suivre ce tutoriel, tu as simplement besoin d'un éditeur de texte de type Visual Studio Code, Atom ou encore Vim. Tu peux utiliser l'IDE que tu souhaites. Si tu n'as pas ou peu de compétences en développement ce n'est pas grave, ce tutoriel est accessible à tous, quelque soit ton niveau.

À noter que dans tout ce tutoriel, tu écriras en _JavaScript_ pour plus de simplicité. En revanche pour tes futurs développements nous te recommandons d'utiliser _TypeScript_ puisque cela va te permettre d'utiliser d'avantage de fonctionnalités comme la génération de SDK ou de documentation par exemple. 

### Description du projet

Comme nous l'avons énoncé plus haut, tu vas créer une application de chat et plus précisément un **Avengers chat** ! Le but est d'avoir un chat en pouvant choisir son personnage des Avengers. Ce chat sera une application web qui sera déployée et accessible via une URL unique.

---
[CAPTURE ECRAN] Capture d'écran du chat lors de son utilisation avec plusieurs personnages et messages

---

Dans un premier temps tu vas préparer ton environnement de travail et initialiser un projet avec la CLI ZetaPush. 

---
[CAPTURE ECRAN] Capture d'écran de la sortie de CLI qui génère un squelette de ton projet

---

Ensuite, tu vas réaliser la première partie du chat. C'est à dire créer un chat temps réel sans pouvoir choisir son personnage au démarrage de l'application. Pour ceci tu vas d'abord te concentrer sur le design de ton application web, puis tu vas apprendre à utiliser les _cloud services_ pour ajouter la partie fonctionnelle du chat.

---
[CAPTURE ECRAN] Capture d'écran du design de l'application, sans le choix des personnages, il y aura donc les id des utilisateurs d'affichés pour chaque message envoyé

---

À ce moment ton chat est prêt et fonctionnel, donc tu souhaiteras sûrement déployer ton application pour qu'elle soit accessible via une URL. C'est ici que tu vas découvrir `zeta push` qui va te permettre d'exposer ton application en ligne.

---
[CAPTURE ECRAN] Capture d'écran de la sortie de la CLI après un `zeta push`

---

Ton chat est bien, mais ce que tu voulais c'est aussi de pouvoir choisir ton personnage des Avengers au lancement de ton application. Ce n'est pas un comportement fournit par défaut par ZetaPush, donc tu vas pouvoir créer cette fonctionnalité dans un _custom cloud service_.

Une fois que tu as écrit et déployé ta fonctionnalité, tu vas pouvoir l'utiliser et déployer la nouvelle version de ton application.

---
[CAPTURE ECRAN] Capture d'écran de l'écran de sélection d'un personnage d'avengers

---

Avec toutes ces étapes tu pourras chatter avec les Avengers !

---
[CAPTURE ECRAN] De retour la capture d'écran de l'application finie ?

---

## Préparation de l'environnement

Pour utiliser ZetaPush, tu as seulement besoin de _NodeJS_ (et implicitement _npm_). Il te faut donc installer _NodeJS_ via : https://nodejs.org

Une fois que c'est fait, tu vas pouvoir initialiser ton Avengers chat.


## Initialisation du projet

Pour initialiser ton application, tu as plusieurs possibilités. Tu peux utiliser le wizard disponible sur https://console.zetapush.com qui vas te guider pas à pas, utiliser la CLI ou encore démarrer en créant manuellement les fichiers nécessaires. Ici tu vas directement utiliser la CLI pour aller au plus vite.

Pour utiliser la CLI, il va te falloir la dépendance _npm_ `@zetapush/cli`. Commence alors par initialiser un projet _npm_, et d'y installer la dépendance à la CLI de ZetaPush :

```bash
$ cd ~/workspace/
$ mkdir avengersChat 
$ cd avengersChat/
$ npm init
$ npm install --save @zetapush/cli
```

Une fois ton dossier de prêt, lance la commande de génération d'un nouveau projet avec ZetaPush :

```bash
$ zeta new
```

Cette commande va te créer une arborescence de projet pour différencier ton code front et ton code back. Ce n'est pas obligatoire mais c'est une bonne pratique pour bien différencier les différentes composantes de ton application.

![Arborescence init projet](./images/arborescence-init-app.png)


À présent ton application est prête à ếtre développée ! Commence par créer le design.

## Création du design de l'application

## Utilisation des _cloud services_

## Déploiement de l'application

## Développement back avec ZetaPush

## Utilisation d'un _custom cloud service_

## Conclusion