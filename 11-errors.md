# Objectifs

L'objectif de ce fichier est de recencer l'ensemble des potentielles erreurs identifiables en utilisant ZetaPush Celtia.

# Cas d'usage

##  Déploiement - application non déployée

Ce cas d'usage correspond à un échec du déploiement d'une application sur la plateforme ZetaPush. Les erreurs citées ci-dessous seront celles qui peuvent survenir **avant** que le _worker_ tente de démarrer.


| Code | Message |
|:---:|:---:|
| NET-01 | No network connection available |
| NET-02 | Failed to access to the ZetaPush platform (Network issue) |
| INFO-01 | No developer login found |
| INFO-02 | No developer password found |
| INFO-03 | This account doesn't exists on this platform |
| INFO-04 | The developer password is wrong for this account |
| INFO-05 | This application name doesn't exists for this organization |
| RIGHT-01 | You can't deploy your code on this application : Access denied |
| SERV-01 | Failed to create the services |
| SERV-02 | Some custom cloud services have the same name |


## Déploiement - worker non démarré

Nous sommes ici dans le cas où la création du _worker_ a bien fonctionné mais que le démarrage de ce dernier n'a pas fonctionné.

> TODO : Voir tâche ZPV3-227 (US ZPV3-131)

