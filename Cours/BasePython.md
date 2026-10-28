# Découverte de la Programmation avec Python


---

# Qu'est-ce que python ?

###### Python est le langage de programmation open source le plus employé par les informaticiens. 
###### Ce langage s’est propulsé en tête de la gestion d’infrastructure, d’analyse de données ou dans le domaine du développement de logiciels. 
###### En effet, parmi ses qualités, Python permet notamment aux développeurs de se concentrer sur ce qu’ils font plutôt que sur la manière dont ils le font. 
###### Il a libéré les développeurs des contraintes de formes qui occupaient leur temps avec les langages plus anciens. Ainsi, développer du code avec Python est plus rapide qu’avec d’autres langages.

---

# Ses avantages ?

##### - Sa facilité d'apprentissage et d'utilisation
##### - Multiplateformes, il fonctionne sur les principaux systèmes d'exploitation et plateformes informatiques
##### - Une communauté importante (Documentation importantes) et très présente sur Github
#####  - Sa versatilité, le nombre de librairies disponible (+ de 70 000) fait qu'il s'adapte à tous vos projets

---

# À quoi sert-il vraiment ?

##### - Développement Web
##### - “Applications de bureau” ou Desktop App
##### - Systèmes d’exploitation
##### - Data Science & Data Analyse
##### - Extraction de données ou Data Mining
##### - Machine learning
##### - Développement de jeux et graphiques 3D

---

### 1ère étape - Installation

Tout d'abord vous avez besoin de télécharger l'environnement python sur https://www.python.org/ puis de sélectionner la dernière version qui convient à votre OS dans la catégorie "Downloads".

Vous aurez ensuite besoin de télécharger un IDE (environnement de développement intégré) comme vscode ou code-oss que nous allons ici utilisé.

Nous allons donc suivre le tutoriel disponible sur https://code.visualstudio.com/docs/python/python-tutorial

---

Pour ces IDE, une fois installé, vous devez installer l'extension python :

![[Pasted image 20211103221932.png]]


---

Ensuite vérifier s'il est bien installé :
-Linux/macOS -> ouvrez vôtre terminal et tapez la commande :
```
python3 --version
```
-Windows -> ouvrez cmd et tapez la commande :
```
py -3 --version
```

Si l'installation s'est bien déroulée alors vous devriez avoir la version de python qui s'affiche à l'écran.

---

##### Lancer VSCode dans votre dossier python
Toujours en utilisant le terminal ou cmd :
```
cd *le_chemin_jusqu'à_votre_dossier*
code .
```
Ou s'il n'est pas encore créé :
```
cd *le_chemin_ou_vous_voulez_créer_votre_dossier*
mkdir python
cd python
code .
```

ou vous pouvez ouvrir votre dossier directement depuis vscode **File > Open Folder**

*PS: maintenant que vous êtes dans votre dossier n'oubliez pas terminer le nom des fichiers que vous allez créer en .py*

---

### Votre 1er programme python

Restons simple pour le moment, vous allez simplement créer un programme python qui affiche "Hello World" avec la commande print (print est une fonction qui sert à afficher quelque chose à l'écran).

Si vous avez des doutes je vous renvoi sur le lien https://code.visualstudio.com/docs/python/python-tutorial, sinon vous pouvez toujours poser vos questions. ;)

---

### Notion de programmation python

---

### Les variables
Une **variable** est une zone de la mémoire de l'ordinateur dans laquelle une **valeur** est stockée. Aux yeux du programmeur, cette variable est définie par un **nom**, alors que pour l'ordinateur, il s'agit en fait d'une adresse, c'est-à-dire d'une zone particulière de la mémoire.

En Python, la **déclaration** d'une variable et son **initialisation** (c'est-à-dire la première valeur que l'on va stocker dedans) se font en même temps.

---

```python
var = 2
print(var)
```
A la première ligne nous avons déclaré, puis initialisé la variable *var* avec la valeur 2. Notez bien qu'en réalité, il s'est passé plusieurs choses :
Python a « deviné » que la variable était un entier. On dit que Python est un langage au **typage dynamique**.
Python a alloué l'espace en mémoire pour y accueillir un entier. Chaque type de variable prend plus ou moins d'espace en mémoire. Python a aussi fait en sorte qu'on puisse retrouver la variable sous le nom *var*.
Enfin, Python a assigné la valeur 2 à la variable *var*.

---

Vous allez rencontrer différents types de variables, principalement :
-bool : qui signifie booléen, uniquement les *True* ou *False*
-int : qui signifie integer, un nombre entier
-float : qui signifie nombre flottant, un nombre à virgule
-str : qui signifie string, c'est une chaîne de caractère

Vous pouvez testez le type de vos variables avec la commande type():
```python
var = 2
print(type(var))
```
qui renvoi :
```
<class 'int'>
```

---

Maintenant vous pouvez essayé d'écrire un programme qui écrira simplement où var1 = 5 :
La valeur de la 1ere variable est 5

*Attention* : la difficulté est de tout mettre dans un seul print.
(réponse au prochain slide)

---

En effet si vous écrivez directement :
```python
print("La 1ere variable a une valeur de :" + var1)
```
on vous renvoie un erreur.
La bonne méthode serait :
```python
print("La 1ere variable a une valeur de :" + str(var1))
```
car ici on transforme le type de la variable pour qu'il corresponde à une chaîne de caractère.
*PS:*vous pouvez aussi l'écrire de façon à automatiser cette modification avec:
```python
print("La 1ere variable a une valeur de :{}".format(var1))
```

---

### Les conditions

La condition basique en python est de la forme:
*Si* condition
*Alors* je fais ceci
*Sinon* je fais cela
```python
if var1 < var2:
	print("var2 est plus grand")
else:
	print("var1 est plus grand")
```
Plusieurs opérateur vous permette d'identifier une condition:
*<* pour signifier inférieur à (<= inférieur ou égale)
*>* pour signifier supérieur à (>= supérieur ou égal)
*=*= pour vérifier une égalité
*!*= pour vérifier une différence

---

Si vous voulez ajouter des conditions supplémentaire de la forme:
*Si* condition 1
*Sinon Si* condition 2
...
*Sinon Si* condition n
*Sinon* je fais cela
en python:
```python
if var1 < var2:
elif var1 < var3:
elif var1 < varn:
else:
	print("var1 est plus grand")
```

---

Si vous voulez vérifier plusieurs conditions silmutanément de la forme:
*Si* condition 1 et/ou condition 2
*Sinon* je fais cela
```python
if var1 < var2 and/or var1 < var3 #ici on précise bien AND ou OR
	...
else
	print("var1 est plus grand")
```

---

Pour terminer avec les conditions sachez qu'il existe aussi ce qu'on appel les conditions ternaires :
var = ("Si condition vrai", Si condition fausse)[condition]
exemple:
```python
verif = ("Vous êtes majeur", "Vous êtes mineur")[age<majeur]
print(verif)
```

*PS:*vous pouvez aussi combiner ce qu'on a vu précedemment en faisant:
```python
verif = ("Vous êtes majeur depuis {} ans".format(age-majeur), "Vous êtes mineur")[age<majeur]
print(verif)
```

---

### Les listes

En python vos variables peuvent contenir des listes. (cf testlist.py)

Comment créer une liste en python :
```python
article_course = ["pomme", "lait", "oeufs", "sucre"]#valeur 0 puis 1 puis 2...
```
et l'afficher :
```python
print(article_course)
print(article_course[0])#affiche le 1er éléments
print(article_course[len(article_course) - 1])#affiche le dernier élément
```

---

##### Pour modifier ces éléments on dispose de plusieurs méthodes :

Modifier un élément :
```python
#modifier les éléments d'une liste
article_course[0] = "poire"

#plusieurs valeurs à la fois
article_course[1:3] = ["beurre", "amendes"]
```

---

Ajouter un élément :
```python
#ajouter un élément
article_course.insert(3, "farine")

#ajout d'une seule valeur à la fin
article_course.append("pâte feuilletée")

#ajouter plusieurs éléments à la liste
article_course.extend(["chocolat", "bananes"])#ajout de plusieurs val à la fin
```

---

Supprimer un élément :
```python
#suppression d'une valeur
article_course.pop(1)#supprime via le numéro
del article_course[1]#idem
article_course.remove("bananes")#supprime via le nom

#suppression de plusieurs valeurs
article_course.clear()
#supprime toutes les valeurs
del article_course[:]
#supprime toutes les valeur ou celles sélectionner avec le [:]
```

---

### Les boucles

En python vous utiliserez plusieurs types de boucles :

for ... in range -> pour une valeur de départ jusqu'à une valeur d'arriver :
```python
for nb in range(1, 5):#ici 5 est exclu
```
for each in ... -> pour chaque (each) valeur d'une liste :
```python
numeros = [1, 4, 8, 16]
for num in numeros:
```


*PS:*N'oubliez de mettre les ":" à la fin de chaque condition

---

while ... -> tant que la condition est vraie :
```python
var = 1
while var <= 5:
	print ("La valeur {} est inférieure ou égale".format(var))
	var += 2
```
*Attention aux boucles infinie*

De plus vous pouvez ajouter les fonction continu ou break dans ces différentes boucles.
continue s'utilise pour passer directement au tour de boucle suivant sans executé la suite de vos conditions alors que break vous fait sortir de la coule

---

### Travaux pratiques
Vous devrez finir le ou les tp que l'on vous donnera après avoir vu les bases de python.
Avec un peu de bon sens et de recherche vous réussirez ^^
Si jamais vous bloquez, sachez que je suis toujours présent pour répondre à vos questions ;)

---

### Les fonctions

Def : C'est comparable à un sous-programme qui va contenir une série d'instructions. On peut prendre l'exemple de la fonction start() ou check_win(). Elle réponde à un problème précis.
En python toutes vos fonctions doivent être appelées pour être executées. Vous devez d'abord créer la fonction puis *ensuite* l'appelé :
```python
def bienvenue():
	print("Bienvenue dans cette fonction")
	print("J'espère que vous allez bien")

bienvenue()
```
Vous pouvez appelé autant de fois que vous voulez les fonctiones que vous avez créer.

---

De plus vous pouvez envoyer des informations à vos fonctions :
```python
def how_are_you(nom):
	print("J'espère que vous allez bien", nom)
bienvenue(nom)
```
ou avec des variables globales :
```python
def age_prochain():
	global age
	age += 1
	print("l'année prochaine vous aurez ", age)
age = 20
```

---
Avec des valeur par défaut :
```python
def how_are_you(nom = "Romain"):
	print("J'espère que vous allez bien", nom)
how_are_you()
nom = "Alix"
how_are_you(nom)
```

---

Vos fonction peuvent aussi renvoyer des résultats :
```python
def sum():
	result = 11 + 11
	return result
def prod():
	return 20 * 20

print("La somme est", sum())
print("Le produit est", prod())
```

---

Et même des résultats différents en fonction de ce que vous voulez faire :
```python
def max(x, y):
	if x > y:
		return x
	else:
		return y
```

---

Dans certain cas vous devrez aussi utiliser des fonctions récursives, c'est à dire des fonctions qui s'appellent elle-même :
```python
def sum(x):
	x += 1
	print(x)
	if x < 50:
		sum(x)

sum (1)
```

---

### Les objets
Les objets en python sont une structure de plusieurs variables. Elle vont définir celui-ci, par exemple avec une personne :
```python
class Personne:
	nom = "Garé"
	prenom = "Romain"
	age = "24"
```
Défini en tant que *class* en python, cet objet vas donner le Nom, Prénom et l'âge d'un personne.

---

Pour les définir dynamiquement il faut écrire comme ceci :
```python
class Personne:
	def __init__(self, nom, prenom, age):
	print ("Bienvenue {}".format(nom, prenom))
```
Ici self correspond au contexte, comme une base de donnée qui permet aux éléments d'être injecté dans l'objet.

---

Les méthodes sont des fonctions mais utilisé dans le cadre d'une classe. Vous pouvez en identifier 3 grands types :
Les *ascesseurs*, pour récupérer des informations :
```python
class Personne:
	def __init__(self, nom, prenom, age):
		self.nom = nom
		self.prenom = prenom
		self.age = age
		print("Bienvenue", nom, self.prenom, ",", age, "ans.")
	def get_nom(self):
		return self.nom
personne = Personne("Garé", "Romain", "24")
print("Nom :", personne.get_nom())
```

---

Les *mutateurs*, qui nous permettent de modifier ces informations :
```python
class Personne:
	def __init__(self, nom, prenom, age):
		self.nom = nom
		self.prenom = prenom
		self.age = age
		print("Bienvenue", nom, self.prenom, ",", age, "ans.")
	def nb_annees(self, nb_annees):
		self.age += nb_annees
		print ("{} ans plus tard, vous avez {} ans".format(nb_annees, self.age))
personne = Personne("Garé", "Romain", "24")
print("Nom :", personne.get_nom())
personne.nb_annees(3)
```

---

Globalement toutes les autres qui permettent un tas de choses différentes, par exemple :
```python
class Personne:
	def __init__(self, nom, prenom, age):
		...
	def diff_age(self, personne_cible):
		return personne_cible.age - self.age
personne = Personne("Garé", "Romain", 24)
personne2 = Personne("Dupond", "Jean", 71)
print ("Il y a une différence de {} ans entre vous".format(personne.diff_age(personne2)))
```

---

Pour terminer avec les objets, vous pouvez créer des fichiers python ne comprenant que votre ou vos objet(s) et les utilisé dans vos programmes :
```python
from personne import Personne

personne5 = Personne("Julie", "Dupont", 22)
print("Bienvenue à vous", personne5.get_nom(), personne5.get_prenom(), ",", personne5.get_age(), "ans")
```

---

### L'héritage
*A remplir*


---

### La manipulation de fichiers

Tout d'abord vous pouvez créer un fichier ou l'ouvrir s'il existe avec la fonction open().
Cette fonction demande 2 arguments, le nom du fichier et le mode d'ouverture (w pour write)
```python
open("list.txt", "w+")
```

---

Pour écrire dans ce fichier rien de plus simple, on utilise la fonction write :
```python
file = open("list.txt", "w+")
file.write("Mot1\n")#sinon pas de retour chariot
file.close#sinon votre fichier attend de nouveau mots à écrire
```
Il est préférable de le mettre dans une variable pour gérer l'ouverture/l'écriture d'un fichier.

---

 Pour ajouter des données dans le fichier sans supprimé ce qui y étais présent (c'est la cas avec "w+"), on utilise "a+" (pour append) :
 ```python
with open("list.txt", "w+") as file:
	file.write("Test1\n")
	file.write("Test2\n")
	file.write("Test3\n")
```

---

On peut utiliser nos différentes connaissance pour donner quelques comme:
 ```python
list_mot = ["Bonjour", "ceci", "est", "un", "test"]
with open("list.txt", "w+") as file:
	file.write("Test1\n")
	file.write("Test2\n")
	file.write("Test3\n")
```

---

Pour lire un documents on utilise "r+" à la place ce qui donne :
 ```python
with open("list.txt", "r+") as file:
	print(file.readlines())
```
On oublie pas file.close(), c'est très important.

---

Si vous voulez vérifier que votre fichier existe : 
```python
import os
if os.path.exists("list.txt"):
	with open("list.txt", "r+") as file:
		print(file.readlines())
```

---

Pour copier ou déplacer vos fichiers on pourra utiliser la librairie shutil, ici copie:
```python
import os
import shutil #pour le copier coller

file = "list.txt"
cible = "testcopie/list.txt"

shutil.copy(file, cible)
```

---

Ici déplacement (copie puis suppression):
```python
import os
import shutil #pour le copier coller

file = "list.txt"
cible = "testcopie/list.txt"

shutil.copy(file, cible)
os.remove(file)
```

---

### Travaux pratique
On vous demande ici de créer un programme qui vas demander à l'utilisateur une couleur. 
On met ensuite ce nom de couleur dans un fichier "couleur.txt".
Si la couleur existe déjà, on invite l'utilisateur à en choisir une autre.
Si l'utilisateur tape le mot "liste" à la place d'une couleur vous devrez afficher toute la liste en présentant une couleur par ligne.
Bon courage et si jamais vous bloquez, sachez que je suis toujours présent pour répondre à vos questions ;)

---

