Retrouver le point d'extraction du programme

D'après l'excercice précedent, le malware lance un CMD via iexplore.exe

Regardons ce qui ce passe dans cette console.
![[Pasted image 20230502212719.png]]
La partie concernant l'image dump n'est pas très intressante.
Par contre la console au PID 1616 contient une trace de trois exécutable.
Et "tcprelay.exe"  détonne de par son nom.
On va donc extraire le dump de la mémoire pour voir si on peut en apprendre plus.

![[Pasted image 20230502213323.png]]
![[Pasted image 20230502213441.png]]
Et on découvre la ligne de coommande de rédirection.


Le dump de la mémoire était aussi faisable sur le processus iexplore PID 2772
![[Pasted image 20230502214011.png]]