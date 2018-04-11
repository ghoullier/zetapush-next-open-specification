# _Cloud Services_ pour les développeurs en ESN

On part du principe qu'un développeur en ESN a déjà une stack technique à disposition qui lui permet d'être efficace. Nous devons alors lui fournir des services qui lui permettent de développer plus vite sur des cas d'usage commun. Par exemple le stockage ou la gestion d'utilisateur.

Voici la liste des _Cloud Services_ que nous mettons à disposition :

---

# **TODO : Revoir façon de faire et mettre en cas d'utilisations** 

---

## StorageService
_Gestion du stockage, de la récupération et de la recherche de données._

Ce service permet de :
- Stocker / Récupérer / Supprimer une données sous forme de clé/valeur
- Séparation des données en fonction des utilisateurs ou groupes d'utilisateurs
- Récupération / Suppression d'un ensemble de données en fonction d'une requête (fonction)
- Rechercher un ensemble de données en fonction d'une requête (fonction)
- Récupérer le nombre de données en résultat d'une fonction sans les récupérer

[Lien vers des exemples d'utilisation](./utilisation-storage.md)


## UserService
_Gestion des utilisateurs, de groupes ..._

Ce service permet de :
- Créer / Récupérer / Mettre à jour / Supprimer des utilisateurs
- Créer / Récupérer / Mettre à jour / Supprimer des groupes d'utilisateurs
- Affecter / Supprimer des utilisateurs à des groupes
- Récupérer les utilisateurs d'un groupe
- Récupérer l'ensemble des groupes auquel un utilisateur appartient
- Gestion de la présence d'un utilisateur

[Lien vers l'API](./api-users.md)

## SecurityService
_Gestion de la sécurité._

Ce service permet de :
- D'appliquer des règles d'accès aux différentes _cloud functions_

[Lien vers l'API](./api-security.md)

## PushService
_Envoi de push notifications._

Ce service permet de :
- Configurer son outils de push notification
- Envoyer des Push notifications

[Lien vers l'API](./api-push.md)

## SMSService
_Envoi de SMS._

Ce service permet de :
- Configurer son client d'envoi de sms
- Envoyer des sms

[Lien vers l'API](./api-sms.md)

## MailService
_Envoi d'email._

Ce service permet de :
- Configurer son client mail
- Envoyer des mails

[Lien vers l'API](./api-mail.md)

## HTTPService
_Envoi de requête HTTP._

Ce service permet de :
- Envoyer des requêtes HTTP

[Lien vers l'API](./api-http.md)

## FileService
_Gestion des fichiers, upload, stockage, récupération._

Ce service permet de :
- Uploader un fichier
- Sauvegarder des fichiers dans une arborescence précise
- Récupérer / Supprimer des fichiers en utilisant l'arborescence

[Lien vers l'API](./api-file.md)
