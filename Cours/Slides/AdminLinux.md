---
theme: consult
enableChalkboard: "true"
height: "540"
margin: "0"
maxScale: "4"
---
<!-- slide template="[[default-title]]" -->
## UTILISATION ET ADMINISTRATION D'UN SERVEUR LINUX

---
<!-- slide template="[[default-template]]" -->
::: title
### Administration Linux
:::

### Linux est principalement utilisé pour la création de services informatiques. Environ 90% d’Internet est hébergé par des serveurs Linux. Les raisons de ce succès sont les performances, la robustesse et la sécurité de ces systèmes. A cela nous pouvons ajouter la gratuité de la plupart des distributions.

### Le système d’exploitation pour smartphones le plus utilisé dans le monde (environ 80%), Android, est également basé sur le noyau Linux. On note, d’un point de vue sécurité, que la majorité des logiciels malveillants (virus) n’ont pas d'impact sur les systèmes linux.

---
<!-- slide template="[[default-template]]" -->
::: title
### Administration Linux
:::

Le terminal, ou encore CLI (Commande Line Interface) est l’interface qui permet l’interaction avec votre système. Ces commandes vont ensuite être interprétées par le shell afin de les retranscrire à l’OS sous une forme qu’il pourra exploiter.

Pour ouvrir le terminal, appuyez sur Ctrl + Alt + T dans votre système Linux ou sinon vous pouvez chercher dans les applications le mot “terminal” puis lancer l’application dédiée pour le terminal.

---
<!-- slide template="[[default-template]]" -->
::: title
### Administration Linux: Quelque mots
:::
::: block
- Gestion de processus
- oui
- ps aux
- affiche la liste des process en cours d’exécution en liste
- htop
- installation: apt-get install htop
- monitoring des process en cours d’exécution
- Monitoring des ressources
- iftop -B -P -i eth0
- installation: apt-get install iftop
- monitoring des échanges réseaux
- lsof
- installation: apt-get install lsof
- monitoring sur les ressources utilisées (fichiers, sockets, pipe)
- Présentation de l’arborescence du FS racine d’un UNIX ou Linux
- Gestion des utilisateurs
:::

---
<!-- slide template="[[default-3-2]]" -->
::: title
### ADMINISTRATION LINUX : GESTION DES PROCESS
:::

::: right
1. Utilisateur exécutant le process
2. PID : le numéro du process
3. %CPU utilisé
4. %RAM utilisé
5. VSZ mémoire virtuelle utilisée (image mémoire sur disque en extension de la RAM, afin de l'alléger)
6. RSS mémoire résiduelle utilisée / non swappée, donnée en RAM
7. TTY utilisé (appelé “Shell”, interface avec le noyau)
8. STAT est l’état du process, en cours, stoppé, etc..
9. START date de lancement
10. TIME temps accumulé sur l’utilisation du CPU, du temps utilisateur + temps système
:::

::: left
![[Pasted image 20240705100025.png]]
:::

---
<!-- slide template="[[default-3-2]]" -->
::: title
### ADMINISTRATION LINUX : GESTION DES PROCESS
:::

::: right
N’hésitez pas à compléter votre commande avec “less” pour paginer la sortie :
```shell
ps faux | less
```
Puis utilisez vos flèches directionnelles haut ou bas pour vous déplacer dans vos pages.
:::

::: left
![[Pasted image 20240705100025.png]]
:::

---

<!-- slide template="[[default-3-2]]" -->
::: title
### ADMINISTRATION LINUX : GESTION DES PROCESS
:::

::: right
Exemple avec : htop

Vous trouverez les même colonnes de base que ps, mais présentées plus dynamiquement et administrable via votre clavier.

Les lignes vertes sont les processus fils légers (appelé thread) exécutés par un processus en cours (appelé processus parent).

Les lignes blanches descendant d’une autre ligne blanche correspond à un processus fils “lourd” (plus complet et plus complexe, généralement indépendant) exécutés par un processus parent.
:::

::: left
![](https://lh7-us.googleusercontent.com/slidesz/AGV_vUdIbM5kbYYiTFcRBXvhmvAuz0ZrtbPQXMES97FW2asseAxhAlfAK8bxs5sjTxv3sKbi21X23-houG1SJz1ZmBlm3rpKgXlqpiBFYf4UyfJ9qFhJ067vnHTyhOAZAMJV2IGqBsV2XwGf1rgJa2NEBuqamaFgUV7U=nw?key=PwXKZkDGSjOgprPetEjm3A)
:::