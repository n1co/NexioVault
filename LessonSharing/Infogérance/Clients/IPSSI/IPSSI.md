# SQY

VLAN : 
On vire tous ce qu'il y a actuellement
on fait un vlan adminstration, étudiant, guest, management, formateurs
répartition par ssid
se configure dans unifi 4 réseau administratiuon, formateur, étudiant, guets pas management
ssid wifi a affecté à leur propres réseau,  tag vlan
pas ssid management caché 
connexion vpn entre vlan management et notre datacenter
baie server 2x 10 go vers baie 2e etage
entre chaque switch 48 ports, les DACS 2x 1Go, 4 Eth si assez de ports
identifier ports à  brassé et les brassé plus tard (2e etage car un switch part au 3è)
switch Juniper on l'enlève au 3eme

Prendre l'étiquetteuse
Affecter une couleur de câble pour chaque service
envoyer mail pY, diff service cisco et fortinet + eventuel connexion vpn intersite 
On vire le TP Link et le D Link (3e) on remonte le 24 ports du 2e et on fusionne les deux 24 ports
trunk SW 24 => tag VLANs
Acces réseau de formation à distance uniquement
_________
pas d'accès routeur sfr
Ouvcerture de port => appeler sfr, ticket => 24h 
50 euros par demande
Ouverture de port sur le ciso => facturé aussi
Pas d'autres opérateur dans ce bâtiment là
_________
Faire un vpn sur pfsense pour le contrôler à distance temporairement

# MLV :

Same VLAN même plage réseau même nom d'ssid même mode d'indentification

## BIS : 
freebox pro, 1 dac vers notre router
rrouter 1 dac vers SW 24, 1 Dac vers SW 48
13 ports restants -> sw à SW => LACP


recentrer patch panel vers le haut, mettre routeur au dessus de la freebox et on peut coller la freebox au routeur 
espace entre les patchs panel et premier sw et espace entre les deux sw

router ecole en dhcp
notre routeur client dhcp

## ONE : 

SW Aruba géré par un presta => 0 info => interconnexion vers PRS 

deux boitié blancs => router board => 
RAD => 
Vérifier les cables de la box port 3 qu'est ce qui est branché derriere
