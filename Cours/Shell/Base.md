Q: C'est quoi pour vous un script shell ?
R: Un script shell c'est pas bien compliqué, c'est beaucoup moins avancé que powershell, c'est juste un enchainement de commandes linux finalement

Q: On peut faire quoi avec des scripts shell ?
R: En même temps tout et rien, techniquement on peut tout faire avec un script shell, le problème c'est que c'est un language qui est dépendants des binaires qu'on a dans le système, par exemple powershell peut lire sans problème des fichiers json ou xml, alors que pour du script shell il faudrait ajouter des binaires expres pour la tache
Le problème en gros c'est qu'un script peut marcher sur mon pc mais pas sur le votre juste parcequ'on a pas installé les mêmes programmes

La tu commence a écrire un script:
Q: c'est quoi ça ? -> `#!/bin/bash`
R: c'est un "shebang", ça indique à votre OS comment executer un script, ou plutot avec quoi l'executer, techniquement c'est pas obligatoire, pourrquoi:

Y'a deux moyens d'executer un script shell:
 * `bash script.sh`
 * ou: le rendre executable avec `chmod +x script.sh`puis le lancer avec `./script.sh`
Si on lance le script avec ./script.sh il doit deja avoir été rendu executable et c'est la que le shebang devient très utile, vu qu'on lui donne pas "bash" directmeent il doit savoir comment l'executer, ou plus exactement avec quoi l'executer

Ensuite commence a montrer des exemples vriament débutant de ton script:
```bash
#!/bin/bash
echo "Hello world"
```
Tu leur explique que certaines commandes sont directement intégrées à bash, c'est le cas de echo qui n'est pas un programme mais une commande interne du shell

# Les bases

## Variables

Pour déclarer et utiliser une variable
>Attention, quand on déclare une variable il faut surtout pas d'espace entre le nom de la variable, le = et la valeur, sinon ça marche pas


>Une variable se déclare sans $ et s'utilise avec le $
```bash
nom="Alice"
echo "Bonjour $nom"
```

Une variable peut aussi être demandée à l'utilisateur:
```bash
read -p "Entrez votre nom : " nom
echo "Bonjour, $nom !"
```

Ici, "nom" a la fin de la commande read indique qu'on stocke dans la variable "nom" la valeur que l'utilisateur va taper

## Conditions
Les condition pourront vous aider pour vos conteneurs, c'est la logique de base d'un script

```bash
read -p "Entrez votre nom : " nom
if [ "$nom" = "Alice" ]; then
  echo "Bienvenue, Alice !"
else
  echo "Vous n’êtes pas Alice."
fi
```

## Boucles

Il existe deux types de boucles en shell, FOR et WHILE qui su'utilisent comme ça

```bash
compteur=1
while [ $compteur -le 5 ]
do
  echo "Compteur : $compteur"
  ((compteur++))
done
```

```bash
for i in 1 2 3
do
  echo "Nombre : $i"
done
```

Un petit exemple qui peut être utile si jamais on veut démarer plusieurs conteneurs similaires:
(pas besoin de l'executer, c'est juste pour leur donner une idée d'automatisation)

```bash
compteur=1
while [ $compteur -le 5 ]
do
  echo "Démarrage du conteneur : $compteur"
  docker run <options> <image>
  ((compteur++))
done
```

# Petit TP

Le but du tp c'est de faire un petit jeu qui s'appelle le "guess the number", ça a l'air con comme ça mais c'est super pour apprendre les différentes logiques de base du langage.
Le but c'est de faire un jeu qui ne s'arrête pas tant qu'on a pas gagné (tu peut les mettre sur la piste que forcement le jeu devra être dans une boucle)

Avant de lancer le TP, explique leur comment générer un nombre aleatoire:
Pour générer un nombre aleatoire en shell c'est facile, on va utiliser une variable d'environnement:
Un peu hors sujet mais important:
Q: C'est quoi une variable d'environnement ?
R: C'est plein de variables déja définies par votre systeme, y'en a plein, vous pouvez les lister avec la commande "env" qui va toute les lister, pour les utiliser c'est facile, juste $VARIABLE, petit exemple:
echo $USERNAME > affiche le nom actuel de l'utilisateur, pourquoi pas l'utiliser dans le jeu
echo $PWD > Affiche le dossier actuel comme la commande pwd

Et nous ce qui nous interesse c'est une variable d'environnement un peu spéciale, qui n'apparait même pas dans la commande env, c'est $RANDOM

La tu peut leur montrer ça:
echo $RANDOM
Et tu l'execute plusieurs fois pour leur montrer que ça genere bien un nombre aleatoire, mais que pour le jeu on veut que ça soit entre 1 et 100 donc la commande nous va pas elle genere entre 0 et 65000 en gros, donc pour régler ça on peut faire des maths, et tu leur montre ça:

`echo $(( RANDOM % 100 + 1 ))`

Pareil execute plusieurs fois pour leur montrer que ça genere bien entre 1 et 100 (le +1 a la fin est pour éviter que ça parte de zéro mais plutot de 1, donc avec le +1 ca genere bien entre 1 et 100 plutot que entre 0 et 99)

Apres tu peut lancer le TP, et tu passes dans les rangs pour voir ce qu'ils font et les mettre sur la piste, la meilleure aide que tu peut donner c'est de voir si ils font bien tout le code dans une boucle et leur expliquer "c'est pas mal mais attention la logique du jeu est forcement une boucle"

Consigne: Faire un script shell qui va générer un nombre aleatoire au debut et devra demander à l'utilisateur de taper un nombre, le script devra indiquer à l'utilisateur si c'est plus grand ou plus petit, et donner en cas de victoire le nombre d'essai qui a été fait.

APres le TP tu fais cette correction avec eux en expliquant ce que j'ai mis en commentaire (les #)

```bash
#!/bin/bash

# Génère un nombre aléatoire entre 1 et 100
target=$(( RANDOM % 100 + 1 ))
attempts=0
guess=0

echo "Bienvenue dans Guess the Number !"
echo "Je pense à un nombre entre 1 et 100. Devine-le !"

# Traduction / explication: on fait une boucle qui tourne tant que ce qui a été tapé par l'utilisateur n'est pas égal au nombre généré aleatoirement. ici le -ne veut dire "not equal" ou non égal 
while [[ $guess -ne $target ]]; do
    read -p "Ta proposition : " guess

    # Vérifie si la saisie est un nombre, tu peut expliquer que c'est une expression reguliere qui vérifie que c'est bien un nombre [0-9] indique qu'on cherche une valeur numerique, le + indique qu'on cherche 1 ou plus de cette valeur numerique et ^ et $ indiquent le début et la fin de l'expression pour rien avoir avant ou apres
    if ! [[ "$guess" =~ ^[0-9]+$ ]]; then
        echo "Veuillez entrer un nombre valide."
        continue
    fi

    ((attempts++))

    if (( guess < target )); then
        echo "C'est plus grand."
    elif (( guess > target )); then
        echo "C'est plus petit."
    else
        echo "Bravo ! Tu as trouvé le nombre en $attempts tentative(s) !"
    fi
done
```
