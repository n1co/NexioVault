# Projet Cybersécurité – Sécurisation d’un Serveur Linux

## Objectif

Vous faites partie d’une équipe de techniciens en cybersécurité. Votre mission est de préparer une **machine Linux sécurisée** destinée à héberger des **services web**.

Le but du projet est de **durcir** une machine Linux pour la rendre la plus sécurisée possible, en suivant les **bonnes pratiques** de la cybersécurité.

---

## Cahier des charges

### 1. Choix de la distribution

- Utilisez une **distribution Linux légère et fiable** (ex: ArchLinux, Alpine)
- L’installation doit être personnalisée pour la sécurité :
    - Partitionnement réfléchi
    - Suppression des services inutiles
    - Choix des packages minimaux

### 2. Accès et authentification

- **Connexion uniquement en SSH**
- **Interdiction des mots de passe** : connexion par **clé SSH uniquement**
- Ajoutez un **second facteur d’authentification (OTP)** avec par exemple **Google Authenticator**
- Le compte **root doit être désactivé**
- Créez un compte d’administration nommé `localadm` :
    - Ce compte utilisera `sudo`
    - L’usage de `sudo` doit exiger un **OTP**

---

## Configuration Web (Serveur web)

- Le serveur web doit :
    - Écouter sur **les ports 80 (HTTP) et 443 (HTTPS)**
    - Rediriger tout le trafic du port **80 vers le 443**
    - Afficher une **page de maintenance** si aucun site n’est encore installé
    - Mise en place d'un certificat pour le HTTPS
- Le répertoire de publication `/data/http` doit être :
    - Dans une partition **chiffrée**

---

## Mesures de sécurité attendues

Voici une liste **non exhaustive** des mesures à mettre en place (vous pouvez en ajouter d'autres si vous les trouvez pertinentes) :

- Pare-feu configuré (ex. : UFW, nftables)
- SSH durci (interdire root, mot de passe, port personnalisé, etc.)
- Services inutiles désactivés
- Journalisation active et surveillée
- Configuration stricte du serveur web (headers HTTP, désactivation des modules dangereux, etc.)
- Mise à jour régulière et sécurisée du système

---

## Détection d'intrusion

Vous devez **réfléchir à l’intégration de systèmes de protection**, en particulier :

- **Fail2ban** : empêche les attaques par force brute
- **ModSecurity** (facultatif mais recommandé) : module de sécurité pour le serveur web (si vous l’installez, cela améliorera votre note)

Expliquez :

- Leur rôle
- L’endroit idéal pour leur installation

---

## Livrable attendu : Rapport

Vous devez produire **un rapport écrit** contenant :

1. **Introduction** : Contexte du projet
2. **Choix techniques** : Distribution, services installés, architecture retenue
3. **Liste des mesures de sécurité mises en place** :
    - Présentation de chaque mesure
    - Commandes ou scripts utilisés
    - Étapes de vérification
4. **Détection d’intrusion** : Explication de fail2ban (et mod_security si utilisé)
5. **Améliorations possibles** : Que pourrait-on faire de plus si on avait plus de temps ou de compétences ?
6. **Conclusion**
7. **Annexes** : Scripts, fichiers de configuration, sources utilisée