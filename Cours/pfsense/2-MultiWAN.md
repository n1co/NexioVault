
https://provya.net/?d=2017/11/24/11/31/31-pfsense-configurer-un-dual-wan-plusieurs-connexions-internet

DOnner un DNS aux interfaces:
System > General Setup 

## 1. Créer un groupe de passerelles

  
Nous allons créer un **groupe de passerelles** comprenant la passerelle de l'interface WAN et la passerelle de l'interface WAN2.  
  
La création s'effectue depuis le menu System > Routing.

Se rendre dans l'onglet Gateway Groups.  
Puis cliquer sur le bouton "+ Add".  
  
Les éléments à configurer sont les suivants :  
  

- **Group Name** : le nom du groupe de passerelles. Dans notre exemple, nous choisissons "Groupe_Gateway" (attention, pas d'espace, tiret ou de caractères spéciaux dans le nom).
- **Gateway Priority** : pour chaque passerelle, nous donnons une priorité d'utilisation. La priorité la plus faible l'emporte toujours. C'est-à-dire que si pour la passerelle de l'interface WAN, vous choisissez une priorité 1 et pour la passerelle de l'interface WAN2 une priorité 2, alors le trafic s'écoulera exclusivement par la passerelle de l'interface WAN. Le trafic s'écoulera via la passerelle de l'interface WAN2 si et seulement si la passerelle de l'interface WAN est hors-service.
- 
**Lorsque vous sélectionnez le même niveau TIER aux deux liens, la fonction d’équilibrage de charge sera activée.**


- **Trigger Level** : permet de définir le déclencheur qui permettra à pfSense de choisir quand basculer vers un lien disposant d'une priorité plus faible. Il existe 4 valeurs possibles :

1. Member down : lorsqu'une passerelle est considérée comme non-joignable (c'est-à-dire lorsque l'adresse IP de monitoring associée n'est plus joignable par un ping)
2. Packet Loss : lorsque le taux de perte de paquets maximum configuré pour cette passerelle est atteint
3. High Latency : lorsque la latence maximale définie pour cette passerelle est atteinte
4. Packet Loss or High Latency : lorsque le taux de perte de paquets maximum ou la latence maximale est atteint

## 2. Mettre en service le dual-WAN

La (presque) dernière étape consiste à configurer le firewall pour lui indiquer par quelle passerelle (ou plutôt quel groupe de passerelles dans notre cas) faire passer le trafic. Comme vu en début d'article, sans précision de notre part, le firewall utilisera la passerelle par défaut. Il est évidemment possible de définir soi-même quelle est la passerelle par défaut. En revanche, il n'est pas possible de définir qu'il faut utiliser un groupe de passerelles par défaut.  
  
Il nous faut donc préciser dans chacune des règles du firewall que le trafic doit s'écouler par notre passerelle par défaut.  
  
Cette configuration se fait depuis le menu Firewall > Rules.

Ajout Widget
a la fin
https://techexpert.tips/fr/pfsense-fr/pfsense-multi-wan-lien-de-charge-equilibrage/