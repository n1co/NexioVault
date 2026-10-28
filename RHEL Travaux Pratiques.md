#### **TP : Installation d'un système Red Hat Enterprise Linux (RHEL)**

**Objectif :** Installer une distribution RHEL en configurant le partitionnement et les options réseau de base.

- **Étapes :**
    1. Démarrer sur le média d’installation RHEL.
    2. Suivre l'assistant d'installation en définissant les paramètres suivants :
        - Langue et clavier.
        - Source d’installation et support matériel.
        - Sélection du partitionnement automatique ou manuel.
    3. Configurer un partitionnement manuel :
        - Créer une partition /boot.
        - Créer une partition racine (`/`) en utilisant le système de fichiers ext4.
        - Si possible, ajouter une partition de swap.
    4. Installer le gestionnaire de paquets YUM.
    5. Configurer l’utilisateur root et ajouter des utilisateurs supplémentaires.
    6. Vérifier la configuration réseau (via DHCP ou configuration manuelle).
    7. Terminer l'installation, redémarrer le système et vérifier le bon fonctionnement.
- **Validation :** Le système doit démarrer correctement, l'utilisateur doit pouvoir se connecter et utiliser le réseau.

---

#### **TP : Analyse du démarrage du système pas à pas**

**Objectif :** Comprendre et analyser le processus de démarrage d’un système Linux en mode “pas à pas”.

- **Étapes :**
    1. Redémarrer le système en sélectionnant l’option “Pas à pas” depuis le chargeur de démarrage GRUB.
    2. Analyser les différentes étapes du démarrage :
        - BIOS/UEFI et chargeur de démarrage.
        - Initialisation du noyau.
        - Analyse des fichiers de démarrage : `/etc/fstab`, `/sbin/init` (ou `systemd`).
        - Identification des services lancés au démarrage.
    3. Observer le rôle de `systemd` dans le démarrage et gérer les niveaux d’exécution.
- **Validation :** Documenter les étapes observées et identifier les fichiers critiques du processus de démarrage.

---

#### **TP1 : Personnalisation du fichier bashrc et création d’alias**

**Objectif :** Modifier l’environnement de travail bash pour inclure des alias et personnaliser le prompt.

- **Étapes :**
    1. Accéder au fichier `.bashrc` de votre répertoire personnel.
    2. Ajouter des alias pour simplifier certaines commandes courantes, par exemple :
        - `alias ll='ls -l'`
        - `alias update='sudo yum update'`
    3. Modifier le prompt bash pour afficher le nom de l’utilisateur et du répertoire courant.
    4. Sauvegarder les modifications et recharger le fichier `.bashrc` avec la commande `source ~/.bashrc`.
- **Validation :** Tester les alias créés et vérifier les modifications du prompt.

#### **TP1.1 : Prise en main de VIM**

**Objectif :** Maîtriser les commandes de base de l’éditeur Vim.

- **Étapes :**
    1. Ouvrir Vim avec un fichier de test (`vim test.txt`).
    2. Se familiariser avec les modes d’édition : mode normal, mode insertion, mode commande.
    3. Utiliser les commandes de base :
        - `i` pour insérer du texte.
        - `:w` pour enregistrer, `:q` pour quitter.
        - `dd` pour supprimer une ligne, `yy` pour copier une ligne, `p` pour coller.
    4. Explorer les fonctionnalités avancées (recherche, remplacements, etc.).
- **Validation :** Créer et modifier un fichier avec Vim, puis enregistrer et quitter.

---

#### **TP2 : Gestion des utilisateurs (Création et suppression d’utilisateurs et de groupes)**

**Objectif :** Apprendre à créer, modifier et supprimer des utilisateurs et des groupes locaux sous Linux.

- **Étapes :**
    1. Créer un utilisateur avec la commande `useradd` et attribuer un mot de passe avec `passwd`.
    2. Créer un groupe avec `groupadd` et ajouter des utilisateurs à ce groupe avec `usermod`.
    3. Supprimer un utilisateur avec `userdel` et un groupe avec `groupdel`.
    4. Explorer les fichiers de configuration des utilisateurs et groupes : `/etc/passwd`, `/etc/group`, `/etc/shadow`.
- **Validation :** Vérifier la création, suppression et modification des utilisateurs et groupes en listant les fichiers de configuration.

#### **TP2.1 : Connexion à un serveur LDAP avec PAM (optionnel)**

**Objectif :** Configurer l’authentification utilisateur via LDAP avec PAM si le temps le permet.

- **Étapes :**
    1. Installer les paquets nécessaires à la connexion LDAP (`pam_ldap`).
    2. Configurer le fichier `/etc/ldap.conf` avec les informations du serveur LDAP.
    3. Tester la connexion en tentant de s’authentifier sur le système avec un compte LDAP.
- **Validation :** Vérifier la connexion LDAP en se connectant avec un compte distant.

---

#### **TP3 : Création de l’arborescence d’un serveur Web avec liens symboliques**

**Objectif :** Organiser les fichiers et dossiers pour un serveur Web et créer des liens symboliques pertinents.

- **Étapes :**
    1. Créer l’arborescence de fichiers pour un serveur web (par exemple `/var/www/html/mon_site`).
    2. Ajouter des fichiers HTML/CSS dans les dossiers appropriés.
    3. Créer des liens symboliques vers des ressources partagées (par exemple, créer un lien symbolique de `/var/www/html/mon_site/images` vers un répertoire de ressources partagées).
- **Validation :** Naviguer dans l’arborescence et vérifier que les liens symboliques fonctionnent correctement.

#### **TP3.1 : Mise en place du serveur web utilisant cette arborescence**

**Objectif :** Installer et configurer un serveur Web (Apache) pour utiliser l’arborescence de fichiers créée.

- **Étapes :**
    1. Installer le serveur Apache (`httpd`).
    2. Configurer le fichier de configuration d’Apache pour pointer vers le répertoire `/var/www/html/mon_site`.
    3. Lancer le service Apache et tester l’accès au site web via un navigateur.
- **Validation :** Accéder au site web depuis un navigateur et vérifier que les fichiers HTML sont servis correctement.

---

#### **TP4 : Configuration réseau manuelle**

**Objectif :** Configurer manuellement les interfaces réseau d’un système Linux.

- **Étapes :**
    1. Lister les interfaces réseau disponibles avec la commande `ip a`.
    2. Configurer une adresse IP statique avec la commande `nmcli` ou en modifiant les fichiers de configuration réseau (`/etc/sysconfig/network-scripts/`).
    3. Tester la connectivité réseau avec des commandes comme `ping`, `traceroute`.
    4. Ajouter une passerelle et des serveurs DNS à la configuration.
- **Validation :** Tester la connexion réseau en accédant à des sites externes.

---

#### **TP5 : Réinstallation de RHEL avec partitionnement manuel et chiffrement LUKS**

**Objectif :** Réinstaller RHEL en configurant manuellement le partitionnement du disque et en activant le chiffrement LUKS.

- **Étapes :**
    1. Démarrer sur le média d'installation RHEL.
    2. Configurer manuellement les partitions, en incluant :
        - Une partition /boot non chiffrée.
        - Une partition racine `/` chiffrée avec LUKS.
    3. Suivre les étapes d’installation classiques et vérifier que le chiffrement est activé.
    4. Lors du redémarrage, entrer la clé de chiffrement pour déverrouiller les partitions protégées.
- **Validation :** Vérifier que le chiffrement LUKS fonctionne et que le système démarre correctement après installation.