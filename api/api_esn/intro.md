# _Cloud Services_ pour les développeurs en ESN

On part du principe qu'un développeur en ESN a déjà une stack technique à disposition qui lui permet d'être efficace. Nous devons alors lui fournir des services qui lui permettent de développer plus vite sur des cas d'usage commun. Par exemple le stockage ou la gestion d'utilisateur.

Voici la liste des _Cloud Services_ que nous mettons à disposition. 
Pour chacun, nous allons décrire les cas d'utilisation du point de vue développeur que nous souhaitons implémenter.

## StorageService
_Gestion du stockage, de la récupération et de la recherche de données._

Ce service permet de :
- Stocker / Récupérer / Supprimer une données sous forme de clé/valeur
- Séparation des données en fonction de mes critères
- Récupération / Suppression d'un ensemble de données en fonction d'une requête (fonction)
- Rechercher un ensemble de données en fonction d'une requête (fonction)

[Lien vers des exemples d'utilisation](./utilisation-storage.md)


## UserService
_Gestion des utilisateurs, de groupes ..._

Ce service permet de :
- Créer / Récupérer / Mettre à jour / Supprimer des utilisateurs
- Gestion de la présence d'un utilisateur

[Lien vers des exemples d'utilisation](./utilisation-users.md)

## GroupService
_Gestion des groupes._

Ce service permet de :
- Créer / Récupérer / Supprimer / Mettre à jour des groupes
- Affecter / Enlever des utilisateurs à des groupes
- Récupérer la liste des utilisateurs par groupe
- Récupérer la liste des groupes auquel un utilisateur appartient

## SecurityService
_Gestion de la sécurité._

Ce service permet de :
- D'appliquer des règles d'accès aux différentes _cloud functions_

[Lien vers des exemples d'utilisation](./utilisation-security.md)

## PushService
_Envoi de push notifications._

Ce service permet de :
- Configurer son outils de push notification
- Envoyer des Push notifications

[Lien vers des exemples d'utilisation](./utilisation-push.md)

## SMSService
_Envoi de SMS._

Ce service permet de :
- Configurer son client d'envoi de sms
- Envoyer des sms

[Lien vers des exemples d'utilisation](./utilisation-sms.md)

## MailService
_Envoi d'email._

Ce service permet de :
- Configurer son client mail
- Envoyer des mails

[Lien vers des exemples d'utilisation](./utilisation-mail.md)

## HTTPService
_Envoi de requête HTTP._

Ce service permet de :
- Envoyer des requêtes HTTP

[Lien vers des exemples d'utilisation](./utilisation-http.md)

## FileService
_Gestion des fichiers, upload, stockage, récupération._

Ce service permet de :
- Uploader un fichier
- Sauvegarder des fichiers dans une arborescence précise
- Récupérer / Supprimer des fichiers en utilisant l'arborescence

[Lien vers des exemples d'utilisation](./utilisation-file.md)


## Gestion des environnements

Dans la plupart des développements, le développeur utilise plusieurs environnements.
Il est nécessaire de permettre au développeur de gérer ses environnements facilement et de pouvoir choisir l'implémentation de ses services au cas par cas.

Prenons le cas d'usage ou nous avons deux environnements, **dev** et **prod**. Nous voulons donc deux instances du `StorageService`.
Nous pouvons dans ce cas créer une instance de `StorageService` pour chaque environnement. Les instances seront complètement distinctes :

```javascript
// Create one instance of StorageService for each environment
const storageServiceForDev = new StorageService({ id: "storage-service-for-dev"});
const storageServiceForProd = new StorageService({ id: "storage-service-for-prod"});
```