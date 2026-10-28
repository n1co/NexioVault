### Ajouter ou modifier des permissions ACL

- **Donner à un utilisateur un accès en lecture seule à un fichier** :
``` setfacl -m u:alice:r-- fichier```

* ***Accorder à un groupe des permissions en lecture et écriture** :
```
setfacl -m g:developpeurs:rw- fichier.txt
```

* ***Appliquer des permissions à plusieurs fichiers et répertoires** :
```
setfacl -m u:alice:rx fichier1.txt fichier2.txt dossier1
```

### Supprimer des permissions ACL

- **Retirer les permissions ACL d'un utilisateur spécifique** :
```
setfacl -x u:alice fichier.txt
```

* ***Supprimer toutes les entrées ACL d'un fichier** :
```
setfacl -b fichier.txt
```

### 📁 Définir des permissions par défaut sur un répertoire

- **Définir des permissions par défaut pour les nouveaux fichiers dans un répertoire** :
```
setfacl -d -m u:alice:rw- dossier
```

Cette commande établit que tous les nouveaux fichiers créés dans `dossier` auront par défaut des permissions de lecture et d'écriture pour l'utilisateur `alice`.

* ***Appliquer des permissions par défaut de manière récursive** :
```
setfacl -R -d -m u:alice:rw- dossier
```

# SELinux
https://hostman.com/tutorials/install-selinux-on-ubuntu-22-04/