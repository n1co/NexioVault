Avant toute recherche & éploitation des données, il est nécessaire de définir le type d'image du dump de la ram :
![[Pasted image 20230427191220.png]]
![[Pasted image 20230427191521.png]]

Une fois le profile de l'image identifié ont peux commencer à en extraire la donner à l'aide des différentes commandes que met à notre disposition Volatility.


Exercice 1 :
Trouver le mdp de John.
On récupe le hash des mots de passe stocker dans la ram :
![[Pasted image 20230430143832.png]]
NTLM Salt windows 
*NTLM est le hashage de mdp présent sur tous les windows récent, ce dernier est concidéré inutile tellement il est simple à casser*

https://crackstation.net/
![[Pasted image 20230430143854.png]]