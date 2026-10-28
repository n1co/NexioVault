
### General:
* Plateforme de dépot de flags de CTF
* Création de compte (emails @ecole-ipssi.com et ecole-ipssi.net uniquement)
* Impossible de créer ou rejoindre une équipe si un évènement est en cours
* Développé en nodejs pour le back et react pour le front
* Base de donnée sqlite3


### Partie admin:
* création d'un évènement
* Dans un évènement possibilité de creer les flags relatifs à l'évènement et uniquement celui la
* pour chaque flags, deux textbox, une pour le flag, une 2ème (int) pour le nombre de points que rapporte le flag
* La possibilité de déclencher le début d'un évènement avec un bouton, bouton qui permettra aussi de clore l'évènement si l'évènement est déjà en cours
* Possibilité de déplacer un utilisateur d'un groupe à un autre, dans une page globale de gestion utilisateur ou il sera possible de supprimer un compte.
* Les admins seront identifiés via un champ "admin" de la base de donnée

### Partie utilisateurs:
* Si l'utilisateur n'a pas d'équipe active, il pourra soit creer une nouvelle équipe, soit en rejoindre une existante via un dropdown
* Lors de la connexion, sera présentée la page de remise de flags, une seule boite de dialogue qui permet d'entrer un flag, et dessous un résumé des flags trouvés, avec un affichage type x/y x étant le nombre actuel de flags trouvés et y le maximum, avec barre de progression
* Si le participant récupère tous les flags de cet évènement, la barre de progression passe au vert, et impossible de remettre de nouveaux flags.

### Partie invités:
* Affichage du leaderboard basé sur le nombre de points total de chaque équipes
