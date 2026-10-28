# Notes


# ToDo
logo

~~Creer, Deplacer ou modifier un event peut call un hook~~
~~Champ client (list deroulante) avec une couleur par client + editeur de client~~
~~api google pour ajouter l'agenda perso~~
~~api google maps adresse~~
~~classer par heure de debut si plusieurs events~~
champ numero de contrat / id regvisor (optionnel)
bouton "envoyer un rdv" pour envoyer une invit google agenda a une personne ??

clic droit sur un event pour upload des justificatifs



Dans le back, tu vas faire en sorte que si la DB est vide au lancement du serveur, elle soit correctement initialisee avec les tables requises, tu vas egalement mettre en place un systeme au lancement du serveur pour qu'il fasse automatiquement les migrations si necessaire


# changelog
added google maps autocomplete


# todo

~~vue par formateur genre en voir un seul~~
~~clic droi sur les items pour genre delete~~
~~faire apparaitre le nom du client dans les bulles d'event~~
~~case a cocher sur un event pour dire si c'est une option, icone pour dire que c'est en attente/optiion couleur jaune qui ignore la couleur client~~
~~description visible que par les admins~~

~~cle api pour gaetan sans auth~~
# v2
systeme de hyerarchie, qui peut gerer le planning de qui
nouveau role gestionnaire

~~historique de changement, qui a fait quoi, on clique sur une case, historique de modif,~~
~~onglet commentaire sur un event~~
~~@username dans les commantiere et lui faire une notif~~
~~coche pour indiquer un commentaire sur un event,~~
~~pouvoir "clore" un commentaire~~
~~ajouter des "task" en plus des commentaires~~


# changelog

- Creation du dashboard
- refonte de certain styles
- systeme d'historique des events
- systeme de commentaire


Todo

nouvelle categorie archive pour les plannings des gens plus la
systeme de gestion des foramtions internes:
	creation dans l'agenda formateur et formé si un admin valide la formation
ls_internal en groupe keycloak a gerer pour formation internes


Validation d'une formation: vaertir que ;un des participants a deja un truc et demander ocnfirnmationd
Recap de la semaine par mail envoyé le dimanche midi (préciser sujet à modification )


Le JSON du calendar semble contenir beaucoup trop de donnees, genre les avatars en base64 ce qui rend enorme le json, il faut regler ca, verifie aussi que le json ne contienne rien de critique, il semble contenir des tokens de calendrier, assure toi qu'il n'y asi rien de critique/inutile dans le json envoye au TeamCalendar:

,"calendarToken":"mhjbi2mogdq6x413o52auyco","avatar":"data:image/png;base64,iVB 
y'a aussi "googleAccessToken, regle ca sans rien casser du TeamCalendar




# Todo

Option d'horaire pour les types teletravail, conges, absences, ecole, deplacement pro, ASTE
Pour les jours feries, deja integrer une case ou un truc du genre pour rendre ca plus visuel

# Changelog

## Nouvelles fonctionnalites
* Travail collaboratif en temps reel, plus besoin d'actualiser, les changements apparaissent en temps reel
* Nouveau types d'evenements, conges, maladie etc... mercid de ne plus creer de clients pour des types d'evenement, demandez moi !
* Acces pour les centres de formation externes pour un visu sur les plannings
* Nouveau dashboard admin pour y voir plus clair dans la gestion du planning

## Correction de bugs
- Correction des adresses, possibilite d'entrer une adresse meme si elle se complete pas toute seule