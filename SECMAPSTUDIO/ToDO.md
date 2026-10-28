~~ctrl+s~~
~~notifications~~
~~raccourcis vim avec petite "barre" qui indique la commande~~
~~"keep me logged in" checkbox~~
support de masscan dans l'import complet (mais pas nmap) ?
dans le node exploit, ajouter "outil" pour sqlmap par exemple
# Redis
* rate limiter
* stockage sessions
* cache result SQL (?)

~~Partage par lien publique~~ 

Remove node editor 

integration logo ~/documents/secmaplogofinal.png

~~Donner un vrai titre aux pages autre que l'accueil, et dans l'éditeur de mindmap faire apparaître le titre de la map dans le titre de page~~
~~Globalement revoir le seo de l'application, peut être ajouter un robots.txt?~~

# Admin panel
* ~~gestion user~~
* changement du type d'abonnement???
* ~~changement du type dce compte user/admin~~
* ~~pagineation des users/classement par header~~
# panel de gestion d'une map

* ~~Ajoute une modale de gestion de mindmap (icone 'editer' a la place de editer/delete une map, ces boutons seront deportes vers cette modal de gestion de la map)~~

* ~~Possibilite de partager a des users, par email, quand on partage à quelqu'un on devra retrouver dans la modale d'édition de mindmap, la liste des users à qui on partage, et quand on partage à un user on doit pouvoir choisir lecture seule ou lecture / écriture, les users à qui on partage ne doivent pas pouvoir supprimer la map, juste se retirer du partage~~ 

* ~~travail collaboratif avec positions de la souris des collaborateurs en temps reel, mais egalement la creation/deplacement des nodes/lignes,  le systeme doit etre performant~~

# pro mode
tu vas ajouter des options SaaS à l'application, le paiement se fera avec stripe, la somme à payer devra être gérée côté serveur, l'application sera gratuite par défaut avec certaines options accessibles uniquement si on a un abonnement payant.
Pour le moment il y'aura les versions "free" et "plus" peut être qu'il y'aura d'autres abonnements plus tard, la version "plus" sera à 4.99€ par mois, si par la suite il y'a un autre plan, par exemple "pro" le fait d'avoir la version au dessus devra donner les avantages en dessous. les tokens stripe seront dans le .env côté serveur
Le paiement sera mensuel, il faut donc faire en sorte de perdre les privileges en fin d'abonnement si pas de renouvellement automatique.
Il faudra aussi ajouter un champ "vip" a la table user, si un user est "vip" il n'a pas besoin d'abonnement pour avoir toutes les fonctions payantes.
dans le panel admin il faudra aussi pouvoir passer quelqun VIP.
Attention, vip est un champ en plus, pas un role comme user ou admin
un admin est forcement VIP/pro
dans le panel admin tu ajoutera la possibilite de declancher une "periode gratuite" genre features pro gratuites pour tout le monde pendant un temps donne
# next

pro mode
~~admin panel~~
~~systeme de suggestions (bouton a cote de la version)~~
~~clic sur version = changelog (editable en MD dans l'admin)~~

~~import/export json (encode en b64 ?)~~

~~dans la gestion de compte, les champs nom prenom et entreprise n'ont pas le meme style que les autres champs, il faut le meme style que le change password~~

~~node screenshot, taille des autres blocs, bouton pour ouvrir en grand dans une modale image viewer~~

~~revoir liste des features, ajouter le travaiol collaboratif (version plus)~~


# tiers

## free
3 maps maximum
maximum 100 nodes par map

## plus 4.99
pas de limite de map / nodes
recup des CVE automatique dans le node vuln
## pro 9.99
travail collaboratif