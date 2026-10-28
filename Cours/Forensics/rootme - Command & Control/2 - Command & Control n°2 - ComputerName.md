Quel est le nom de la machine ?
On oublie pas d'Imageinfo le dump de la mèmoire afin d'obtenir son profile.

Pour trouver le nom de la machine on peut utiliser le paramètre 'envars'
fourni par Volatility qui nous liste les variables environnemental des process.
Déf Variables environnement :  Un jeux de variable fourni aux process. Donant du context sur la machine. 
Pas fiable car modifiable par le programme.
![[Pasted image 20230430103657.png]]
[etc..]
Vous pouvez rechercher à la main dedans avec un '' | less '' à la suite de votre commande.
Mais si vous connaissez déjà le nom de la variable vous pouvez utiliser | grep pour afficher que les lignes contenant la variable recherché.
![[Pasted image 20230430104026.png]]
[etc..]

Autre solution sans utiliser les paramètre fournis par Volatility.
On ressort toutes les lignes de texte du dump de la mémoire et on affiche les lignes qui contiennent le computername.
le paramètre '-i' est important pour ne prender en compte la casse lors de la recherche.
![[Pasted image 20230430104357.png]]

AUTRE SOLUTION :

On va regarder dans les registres de windows.
Volatility met à notre disposition ces dernières avec le paramètre 'hivelist'.
![[Pasted image 20230430212322.png]]

\\REGISTRY\\MACHINE\\SYSTEM

Le registre système \\REGISTRY\\MACHINE\\SYSTEM est une partie importante du registre Windows. Il contient des informations cruciales sur la configuration matérielle et les paramètres système de l'ordinateur. Les informations stockées dans ce registre incluent:

1.Les informations sur les périphériques matériels
2.Les paramètres du système: les paramètres du système
3.Les informations sur les utilisateurs

On utilise le paramètre printkey pour afficher les valeurs/ données spécifié dans le registre de clef.
Il est dont nécessaire de lui indiquer le registre cible.

![[Pasted image 20230430230634.png]]