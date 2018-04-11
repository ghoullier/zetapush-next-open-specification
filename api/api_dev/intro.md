# _Cloud Services_ pour les développeurs seuls

---

# **TODO : Revoir façon de faire et mettre en cas d'utilisations** 

---

On part du principe qu'un développeur seul n'a pas les mêmes besoins qu'une entreprise avec des process et une stack technique bien rodée. Dans ce cas, nous allons spécifier des _Cloud Services_ d'un point de vue plus fonctionnel. Chaque profil aura bien-sûr accès à tous les _Cloud Services_ mes ceux présentés ci-dessous seront plus pertinent pour un développeur seul.

## ChatService
_Fournit l'ensemble des méthodes utiles pour faire un chat temps réel._

Ce service permet de :
- Créer / supprimer / mettre à jour / récupérer une "room" de chat
- Ajouter / Supprimer des utilisateurs d'une room
- Récupérer la liste des utilisateurs de la room
- Récupérer la liste des rooms auquel un utilisateur appartient
- Envoyer un message à l'ensemble des utilisateurs de la room
- Envoyer un message à une personne précise
- Récupérer l'ensemble des messages (ou par utilisateur)
- Supprimer tous les messages (ou par utilisateur)
- Envoyer des messages techniques (par exemple pour de l'établissement de visio)
- Écouter les messages entrants