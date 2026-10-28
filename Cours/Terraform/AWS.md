VPC + EC2

VPC -> Gestion reseau
EC2 -> Gestion VM

Create VPC
Configurer un plan IP general 10.0.0.0/16

et subnets associs a un vpc 10.0.0.0/24 dans meme plan ip
impossible a changer apres

creer gateway, 1 par vpc attach to vpc

route table cree avec le vpc, une seule regle de routage de base, 10.0.0.0/16 est en local
autant de sous reseau qu'on veut

creer une route par defaut -> edit route pour passer par internet gateway en type

subnet prive 10.0.1.0/24 recupere la meme table de routage que le precedent (tablede raoutage principale)

possibilite d'associer les tables de routages aux subnets


#### security group
a accrocher au cartes reseau (pare feu devant la carte reseau)


#### ec2
creer des instances ec2
utiliser un sec group cree

![[Pasted image 20240621135916.png]]
`token de session dqns l'ui aws
![[Pasted image 20240621140200.png]]

TP:

