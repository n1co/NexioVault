Macs uniquement
mélange iMac / Macbooks
Freebox pro, tous clients en wifi

### NAS 192.168.10.106
Modèle TS-453BT3
3 stockages
* MKS-DATA -> 8.33 / 12.90 TB 
* MKD-DATA3 -> 11.57 / 16.02 TB
* DataVol1 -> 14.43 / 16.03 TB

Le nas a 4 baies + deux extentions (3x 4 disques)

2 interfaces 1GBps, une interface 10gbps,  deux utilisées (1 et 10)
Connexion directe d'un des pc au nas en ethernet, le reste en TB3

Partages réseau en AFP, voir un passage en SMB

### Réseau
Pas de switch, connexion directe au nas
Tout le monde en wifi

### Problèmes
Problèmes d'accès, tombe sans raison (ethernet ? TB?)
Lenteurs de transferts

### A prévoir
Un switch 10gbps
LACP du nas sur le switch
passer tout le monde en réseau 10gbps (adaptateurs tb -> ethernet) pour éviter le wifi
NAS en DHCP, prevoir ip fixe ? Pertes de connexion random, le nas ne passe pas par le routeur/switch


Ou:

Refonte complete avec serveur de staockage