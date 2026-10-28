1. Installer les mises à jour
    
    ```
    sudo apt update
    sudo apt upgrade
    ```
    
2. Installer les paquets de sécurité recommandés
    
    ```
    sudo apt install unattended-upgrades
    sudo dpkg-reconfigure --priority=low unattended-upgrades
    ```
    
3. Configurer le pare-feu (UFW)
    
    ```
    sudo apt install ufw
    sudo ufw default deny incoming
    sudo ufw default allow outgoing
    sudo ufw allow ssh
    sudo ufw enable
    ```
    
4. Désactiver les services inutiles
    
    ```
    sudo systemctl stop apparmor
    sudo systemctl disable apparmor
    sudo systemctl stop avahi-daemon.socket
    sudo systemctl disable avahi-daemon.socket
    sudo systemctl stop cups.service
    sudo systemctl disable cups.service
    ```
    
5. Configurer SELinux (optionnel)
    
    ```
    sudo apt install selinux-utils
    sudo selinux-activate
    sudo selinux-config-enforcing
    ```
    
6. Configurer l'audit
    
    ```
    sudo apt install auditd
    sudo auditctl -e 1
    sudo auditctl -a exit,always -F arch=b64 -S execve -k command
    ```
    
7. Retirer les paquets non utilisés
    
    ```
    sudo apt autoremove
    ```
    
8. Sécuriser les fichiers système
    
    ```
    sudo chmod 644 /etc/passwd
    sudo chmod 644 /etc/shadow
    sudo chmod 644 /etc/group
    sudo chmod 644 /etc/gshadow
    sudo chown root:root /etc/passwd
    sudo chown root:shadow /etc/shadow
    sudo chown root:root /etc/group
    sudo chown root:shadow /etc/gshadow
    ```
    
9. Configurer les journaux système
    
    ```
    sudo nano /etc/rsyslog.conf // Décommentez ou ajoutez les lignes suivantes
    *.emerg :omusrmsg:*
    auth,authpriv.* /var/log/auth.log
    cron.* /var/log/cron.log
    kern.* /var/log/kern.log
    mail.* /var/log/mail.log
    user.* /var/log/user.log
    ```
    
10. Configurer sudo
    
    ```
    sudo nano /etc/sudoers // Ajoutez la ligne suivante
    Defaults use_pty
    ```
    

11. Configurer l'authentification forte pour SSH
    
    ```
    sudo nano /etc/ssh/sshd_config // Modifiez les lignes suivantes
    PasswordAuthentication no
    ChallengeResponseAuthentication no
    UsePAM yes
    PubkeyAuthentication yes
    AuthenticationMethods publickey
    ```
    
12. Configurer la rotation des journaux système
    
    ```
    sudo nano /etc/logrotate.conf // Ajoutez les lignes suivantes
    /var/log/syslog
    {
        rotate 7
        daily
        missingok
        notifempty
        compress
        delaycompress
        sharedscripts
        postrotate
            systemctl reload rsyslog.service > /dev/null
        endscript
    }
    ```
    
13. Installer et configurer Fail2ban
    
    ```
    sudo apt install fail2ban
    sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local // Copiez la configuration par défaut en tant que fichier local
    sudo nano /etc/fail2ban/jail.local // Modifiez la configuration selon vos besoins
    ```
    
14. Installer et configurer une solution de détection d'intrusion
    
    ```
    sudo apt install ossec-hids-server
    sudo nano /var/ossec/etc/ossec.conf // Modifiez la configuration selon vos besoins
    ```
    
15. Configurer la politique de sécurité avancée (AppArmor)
    
    ```
    sudo apt install apparmor-profiles apparmor-utils
    sudo apparmor_status // Affichez le statut d'AppArmor
    sudo aa-enforce /etc/apparmor.d/* // Activez l'application des politiques de sécurité
    ```
    
16. Configurer la surveillance de l'intégrité du système
    
    ```
    sudo apt install aide
    sudo aideinit // Initialisez le système de surveillance
    sudo nano /etc/aide/aide.conf // Modifiez la configuration selon vos besoins
    sudo aide --check // Vérifiez l'intégrité du système
    ```

**Installation d'auditd :** Pour installer `auditd` sur Ubuntu 20.04 LTS, suivez les étapes suivantes :

1. Ouvrez un terminal.
    
2. Mettez à jour les référentiels de paquets avec la commande suivante :
    

sqlCopy code

`sudo apt update`

3. Installez le paquet `auditd` avec la commande suivante :

Copy code

`sudo apt install auditd`

4. Une fois l'installation terminée, le démon `auditd` démarrera automatiquement et sera exécuté à chaque démarrage du système.

**Utilisation de `auditd` :** Maintenant que `auditd` est installé, voici quelques exemples de commandes et de configurations courantes :

1. Vérifier l'état d'auditd :

luaCopy code

`sudo systemctl status auditd`

2. Activer `auditd` :

bashCopy code

`sudo systemctl enable auditd`

3. Démarrer `auditd` :

sqlCopy code

`sudo systemctl start auditd`

4. Arrêter `auditd` :

arduinoCopy code

`sudo systemctl stop auditd`

5. Redémarrer `auditd` :

Copy code

`sudo systemctl restart auditd`

6. Configurer les règles d'audit : Les règles d'audit définissent les événements à surveiller. Elles sont définies dans le fichier `/etc/audit/rules.d/audit.rules`. Vous pouvez éditer ce fichier pour ajouter ou modifier les règles. Voici un exemple de règle pour surveiller les tentatives de connexion SSH :

cCopy code

`-w /var/log/auth.log -p wa -k ssh_logs`

Cette règle surveille le fichier `/var/log/auth.log`, enregistre les événements d'écriture et d'accès, et ajoute une clé d'audit `ssh_logs`.

7. Redémarrer `auditd` pour appliquer les modifications de règles :

Copy code

`sudo systemctl restart auditd`

**TP - Travaux Pratiques :**

1. Vérifier l'état d'auditd sur votre système.
    
2. Vérifier si le fichier `/etc/audit/rules.d/audit.rules` existe sur votre système et affichez son contenu.
    
3. Ajouter une règle d'audit dans le fichier `/etc/audit/rules.d/audit.rules` pour surveiller un fichier ou un répertoire de votre choix. Par exemple, surveillez le fichier `/etc/passwd` et enregistrez tous les événements d'accès.
    
4. Redémarrez `auditd` pour appliquer les modifications de règles.
    
5. Vérifiez les journaux d'audit à l'aide de la commande `ausearch` pour voir les événements enregistrés liés à votre règle d

La commande `auditctl` est utilisée pour configurer les règles d'audit du noyau Linux. Pour surveiller les modifications apportées au fichier `/etc/passwd`, vous pouvez utiliser la commande `auditctl` avec les options appropriées. Voici un exemple de commande `auditctl` pour surveiller le fichier `/etc/passwd` :

shellCopy code

`sudo auditctl -w /etc/passwd -p wa -k etc_passwd_changes`

Explications de la commande :

- `sudo` : exécute la commande en tant qu'administrateur (superutilisateur) pour accéder aux fonctionnalités d'audit.
- `auditctl` : commande pour configurer les règles d'audit.
- `-w /etc/passwd` : spécifie le chemin du fichier à surveiller. Dans cet exemple, nous surveillons le fichier `/etc/passwd`.
- `-p wa` : définit les permissions de lecture (w) et d'écriture (a) pour le fichier.
- `-k etc_passwd_changes` : ajoute une clé (étiquette) personnalisée pour identifier cette règle d'audit. Vous pouvez choisir un nom significatif pour la clé.

Après avoir exécuté cette commande, le système commencera à surveiller les modifications apportées au fichier `/etc/passwd`. Chaque fois qu'une modification est effectuée sur le fichier, elle sera enregistrée dans les journaux d'audit.

Pour afficher les entrées d'audit correspondantes, vous pouvez utiliser la commande `ausearch` :

shellCopy code

`sudo ausearch -k etc_passwd_changes`

Cela affichera les événements d'audit liés aux modifications du fichier `/etc/passwd` qui ont été enregistrés dans les journaux d'audit.

N'oubliez pas que l'utilisation de `auditctl` nécessite des privilèges administratifs, donc vous devrez exécuter ces commandes en tant que superutilisateur ou en utilisant `sudo`.

**Introduction à ModSecurity :**

ModSecurity est un module de pare-feu d'application Web (Web Application Firewall - WAF) open source qui s'intègre à Apache HTTP Server. Il fournit une couche de sécurité supplémentaire en inspectant le trafic HTTP/HTTPS et en filtrant les requêtes malveillantes ou suspectes pour protéger les applications Web contre les attaques.

**Installation de ModSecurity :**

Pour installer ModSecurity sur Apache, suivez les étapes ci-dessous :

1. Assurez-vous que Apache est déjà installé sur votre système. Si Apache n'est pas installé, vous pouvez l'installer avec la commande suivante :

Copy code

`sudo apt install apache2`

2. Installez le module ModSecurity pour Apache en utilisant la commande suivante :

luaCopy code

`sudo apt install libapache2-mod-security2`

3. Une fois l'installation terminée, redémarrez Apache pour prendre en compte les modifications :

Copy code

`sudo systemctl restart apache2`

**Configuration de ModSecurity :**

ModSecurity utilise un fichier de configuration principal appelé `modsecurity.conf`. Vous pouvez modifier ce fichier pour personnaliser les règles de sécurité selon vos besoins. Voici quelques directives de configuration courantes :

1. Emplacement du fichier de configuration de ModSecurity : Le fichier de configuration `modsecurity.conf` se trouve généralement dans le répertoire `/etc/modsecurity/`. Vous pouvez l'éditer en utilisant votre éditeur de texte préféré.
    
2. Activation de ModSecurity dans Apache : Par défaut, ModSecurity est désactivé. Pour l'activer, vous devez inclure le module ModSecurity et charger ses règles dans la configuration d'Apache. Ajoutez les lignes suivantes dans votre fichier de configuration d'Apache (`/etc/apache2/apache2.conf` ou un fichier de configuration spécifique) :
    

phpCopy code

`<IfModule mod_security2.c>     SecRuleEngine On     Include /etc/modsecurity/modsecurity.conf </IfModule>`

3. Personnalisation des règles de sécurité : Le fichier `modsecurity.conf` contient des règles de sécurité par défaut. Vous pouvez les modifier ou ajouter vos propres règles pour répondre à vos besoins spécifiques. Assurez-vous de comprendre les implications de chaque règle avant de les modifier.
    
4. Redémarrage d'Apache : Après avoir apporté des modifications à la configuration de ModSecurity, redémarrez Apache pour appliquer les modifications :
    

Copy code

`sudo systemctl restart apache2`


Préparation :

1. Téléchargez le Guide de Hardening du Système de l'ANSI et familiarisez-vous avec son contenu.

Étape 1 : Configuration initiale

1. Mettez à jour votre système :
    
    shellCopy code
    
    `sudo apt update sudo apt upgrade`
    
2. Activez le pare-feu :
    
    shellCopy code
    
    `sudo ufw enable`
    
3. Vérifiez si des services inutiles sont en cours d'exécution :
    
    shellCopy code
    
    `sudo service --status-all`
    
4. Désactivez les services inutiles :
    
    shellCopy code
    
    `sudo systemctl disable <service-name>`
    

Étape 2 : Gestion des utilisateurs et des privilèges

1. Vérifiez les utilisateurs existants :
    
    shellCopy code
    
    `cat /etc/passwd`
    
2. Supprimez les comptes d'utilisateurs inutiles :
    
    shellCopy code
    
    `sudo userdel <username>`
    
3. Renforcez les politiques de mot de passe :
    
    shellCopy code
    
    `sudo nano /etc/login.defs`
    
    Modifiez les paramètres relatifs aux mots de passe, tels que la longueur minimale, les caractères spéciaux requis, etc.
    
4. Limitez les droits de superutilisateur :
    
    shellCopy code
    
    `sudo visudo`
    
    Ajoutez les utilisateurs autorisés à utiliser la commande `sudo` et limitez l'accès aux commandes sensibles.
    

Étape 3 : Sécurité des fichiers et des répertoires

1. Restreignez les autorisations des fichiers sensibles :
    
    shellCopy code
    
    `sudo chmod 600 <file>`
    
2. Assurez-vous que les répertoires sensibles sont accessibles uniquement par l'utilisateur root :
    
    shellCopy code
    
    `sudo chown root:root <directory> sudo chmod 700 <directory>`
    
3. Activez SELinux ou AppArmor pour renforcer la sécurité des fichiers et des processus.
    

Étape 4 : Sécurité du réseau

1. Désactivez les services réseau inutiles :
    
    shellCopy code
    
    `sudo systemctl disable <service-name>`
    
2. Configurez le pare-feu pour autoriser uniquement le trafic nécessaire :
    
    shellCopy code
    
    `sudo ufw allow <port>/<protocol>`
    
3. Utilisez un outil comme Fail2ban pour protéger contre les attaques de force brute.
    

Étape 5 : Surveillance et journaux

1. Configurez le journal système pour enregistrer les événements importants :
    
    shellCopy code
    
    `sudo nano /etc/rsyslog.conf`
    
    Décommentez ou ajoutez les lignes appropriées pour enregistrer les événements de sécurité.
    
2. Activez l'audit du système pour surveiller les activités suspectes :
    
    shellCopy code
    
    `sudo nano /etc/audit/audit.rules`
    
    Ajoutez des règles d'audit pour surveiller les fichiers