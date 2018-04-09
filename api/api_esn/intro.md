# _Cloud Services_ pour les développeurs en ESN

On part du principe qu'un développeur en ESN a déjà une stack technique à disposition qui lui permet d'être efficace. Nous devons alors lui fournir des services qui lui permettent de développer plus vite sur des cas d'usage commun. Par exemple le stockage ou la gestion d'utilisateur.

Voici la liste des _Cloud Services_ que nous mettons à disposition :

## StorageService
_Gestion du stockage, de la récupération et de la recherche de données._

Ce service permet de :
- Stocker / Récupérer / Supprimer une données sous forme de clé/valeur
- Séparation des données en fonction des utilisateurs ou groupes d'utilisateurs
- Récupération/Suppression d'un ensemble de données en fonction d'une requête (fonction)
- Rechercher un ensemble de données en fonction d'une requête (fonction)
- Récupérer le nombre de données en résultat d'une fonction sans les récupérer

[Lien vers l'API](./api-storage.md)


## UserService
_Gestion des utilisateurs, des droits, de groupes ..._

Ce service permet de :
- Créer / Mettre à jour / Supprimer des utilisateurs
- Créer / Mettre à jour / Supprimer des groupes d'utilisateurs
- Affecter / Supprimer des utilisateurs à des groupes
- Gestion de la présence d'un utilisateur

[Lien vers l'API](./api-users.md)

## SecurityService
_Gestion de la sécurité._

Ce service permet de :
- Créer des droits (utilisable dans tous les autres services par la suite)
- Utiliser des droits préféfinis (Stockage de données, lecture ...)
- Affecter des droits à des utilisateurs ou des groupes d'utilisateurs
- Appliquer des droits sur différents services
- Créer et appliquer des règles globales de sécurité

[Lien vers l'API](./api-security.md)

## CommunicationService
_Communication exterieure, email, SMS, push notifications..._

Ce service permet de :
- Envoyer un email
- Envoyer des SMS
- Envoyer des Push notifications
- Envoyer des requêtes HTTP

[Lien vers l'API](./api-communication.md)

## FileService
_Gestion des fichiers, upload, stockage, récupération._

Ce service permet de :
- Uploader un fichier
- Sauvegarder des fichiers dans une arborescence précise
- Récupérer / Supprimer des fichiers en utilisant l'arborescence

[Lien vers l'API](./api-file.md)