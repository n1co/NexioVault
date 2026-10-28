 
# TP1 Compter les voyelles

Écris un programme qui :
1. Demande à l’utilisateur une phrase.
2. Compte le nombre de voyelles (a, e, i, o, u, y).
3. Affiche le résultat.

Exemple :

`Entrez une phrase : Bonjour tout le monde`
`Nombre de voyelles : 8`

## correction

```python
phrase = input("Entrez une phrase : ")
voyelles = "aeiouyAEIOUY"
compteur = 0

for char in phrase:
    if char in voyelles:
        compteur += 1

print("Nombre de voyelles :", compteur)

```



# TP 2 – Deviner un nombre

### Objectif

- Utiliser une boucle `while`
- Comparaisons simples
- Gestion de la fin de boucle

---

## **Énoncé**

Écris un programme qui :

1. Choisit un nombre aléatoire entre 1 et 50.
    
2. Demande à l’utilisateur de deviner ce nombre.
    
3. Indique si la tentative est trop haute, trop basse ou correcte.
    
4. Continue jusqu’à ce que l’utilisateur trouve.
## correction

```python
import random

nombre = random.randint(1, 50)
choix = 0

while choix != nombre:
    choix = int(input("Devinez le nombre (1-50) : "))

    if choix < nombre:
        print("Trop bas.")
    elif choix > nombre:
        print("Trop haut.")
    else:
        print("Bravo, vous avez trouvé !")

```


# TP 3 – Générateur de mot de passe

### Objectif

- Manipulation des chaînes
- Boucles
- Utilisation du module `random`

## **Énoncé**

Écris un programme qui génère un mot de passe aléatoire :

1. L’utilisateur choisit la longueur.
2. Le mot de passe peut contenir :
    - lettres minuscules
    - lettres majuscules
    - chiffres
    - caractères spéciaux (`!?$@%`)

Affiche ensuite le mot de passe généré.


## correction

```python
import random

longueur = int(input("Longueur du mot de passe : "))

minuscules = "abcdefghijklmnopqrstuvwxyz"
majuscules = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
chiffres = "0123456789"
speciaux = "!?$@%"
tous = minuscules + majuscules + chiffres + speciaux

mdp = ""

for _ in range(longueur):
    mdp += random.choice(tous)

print("Mot de passe généré :", mdp)

```


# **TP 4 – Analyse d’une liste de nombres**

### Objectif

- Manipuler les listes
- Utiliser boucles et conditions
- Calculer min, max, moyenne "à la main"

---

## **Énoncé**

Demande à l’utilisateur de saisir 5 nombres.  
Stocke-les dans une liste, puis affiche :

- le plus grand
- le plus petit
- la moyenne

Interdiction d’utiliser `min()`, `max()` ou `sum()` dans la version de base.

## correction

```python
nombres = []

for i in range(5):
    n = float(input(f"Entrez le nombre {i+1} : "))
    nombres.append(n)

# Initialisation
mini = nombres[0]
maxi = nombres[0]
somme = 0

for n in nombres:
    if n < mini:
        mini = n
    if n > maxi:
        maxi = n
    somme += n

moyenne = somme / len(nombres)

print("Plus petit :", mini)
print("Plus grand :", maxi)
print("Moyenne :", moyenne)

```

# **TP 5 – Mini-système de gestion (menu + actions)**

### Objectif

- Gérer un menu en boucle
- Stocker des données dans une liste
- Manipuler l’entrée utilisateur

---

## **Énoncé**

Créer un mini-système qui permet :

1. D’ajouter un prénom dans une liste
2. D’afficher la liste
3. De supprimer un prénom
4. De quitter

Affiche le menu tant que l’utilisateur ne choisit pas "Quitter".

## correction
```python
prenoms = []
choix = ""

while choix != "4":
    print("\n--- Menu ---")
    print("1 - Ajouter un prénom")
    print("2 - Afficher les prénoms")
    print("3 - Supprimer un prénom")
    print("4 - Quitter")
    choix = input("Votre choix : ")

    if choix == "1":
        p = input("Entrez un prénom : ")
        prenoms.append(p)
        print("Ajouté.")
    elif choix == "2":
        print("Liste :", prenoms)
    elif choix == "3":
        p = input("Quel prénom supprimer ? ")
        if p in prenoms:
            prenoms.remove(p)
            print("Supprimé.")
        else:
            print("Ce prénom n'est pas dans la liste.")
    elif choix == "4":
        print("Au revoir !")
    else:
        print("Choix invalide.")

```