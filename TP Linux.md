# **TP Linux – Mise en place d’un Serveur Web + Reverse Proxy Sécurisé**

**Deux VM Debian – Sécurisation avancée – SSH à clé**

---

## **1. Objectifs du TP**

Ce travail pratique a pour objectif de vous faire mettre en place une architecture Web sécurisée composée de deux serveurs Debian minimalistes :

- Un **serveur Web** (VM1) : `srv-webserver`
    
- Un **serveur Reverse Proxy** (VM2) : `srv-revproxy`
    

Vous devrez appliquer une politique de sécurité stricte sur les deux machines, installer les services nécessaires et configurer un accès SSH entièrement sécurisé.

---

## **2. Attendus en fin de projet**

À la fin du TP, vous devrez avoir :

### **Sécurisation et administration**

- Un utilisateur administrateur dédié, avec élévation de privilèges contrôlée.
- Le compte root **désactivé**
- Aucun accès administrateur autre que via sudo
- SSH configuré avec :
    - Authentification **exclusivement par clé** (pas de mot de passe).
    - Accès autorisé **uniquement depuis l’adresse IP du poste étudiant**.
    - Interdiction totale de la connexion root en SSH.

### **Serveur Web (srv-webserver)**

- Un service Web fonctionnel avec un site minimal personnalisé
- Un hôte virtuel configuré proprement (selon la technologie choisie)

### **Reverse Proxy (srv-revproxy)**

- Mise en place du reverse proxy de votre choix.
- Mise en place d’un certificat SSL **auto-signé**.
- Implémentation d’un accès **strictement HTTPS**, avec :
    - Redirection automatique de HTTP vers HTTPS.
    - Interdiction totale du HTTP simple.

### **Communication entre les deux serveurs**

- Le reverse proxy doit récupérer les pages depuis le serveur Web.
- L’utilisateur final doit accéder au site uniquement via le reverse proxy.

---

## **3. Architecture technique attendue**

- Deux machines virtuelles Debian installées en configuration minimale.
- Un réseau interne reliant les deux serveurs.
- Accès SSH possible uniquement depuis le poste étudiant vers chaque serveur.
- Le reverse proxy expose le site vers l’extérieur ; le serveur Web n’est pas accessible directement.

Un schéma d’architecture doit être ajouté dans votre rapport.

---

## **4. Travaux à réaliser**

### **4.1 Sécurisation des serveurs (obligatoire sur les deux VM)**

Vous devez :

1. Créer un utilisateur administrateur.
2. Activer l’usage de sudo pour cet utilisateur.
3. Désactiver le compte root.
4. Configurer SSH pour :
    - Interdire la connexion root.
    - Désactiver l’authentification par mot de passe.
    - Autoriser uniquement la connexion par certificat.
    - Restreindre l’accès SSH à l’adresse IP de votre poste.
    - Restreindre SSH uniquement à votre utilisateur administrateur.

Ces règles doivent être appliquées sur les deux machines.

---

### **4.2 Mise en place du serveur Web (srv-webserver)**

Vous devez :

- Installer la solution Web de votre choix (**Apache**, **Nginx**, ou autre technologie valide**).
- Créer un répertoire dédié pour votre site.
- Déployer une page d’accueil personnalisée contenant :
    - Nom et prénom
    - Nom du projet
    - Classe / groupe
- Mettre en place un hôte virtuel propre, qui pointera vers ce site.
- Vérifier que votre serveur Web renvoie correctement la page.

---

### **4.3 Mise en place du Reverse Proxy (srv-revproxy)**

Vous devez :

- Installer un reverse proxy de votre choix (ex. : **Nginx**, **Apache**, **HAProxy**, **Traefik**, etc.).
- Configurer un certificat SSL auto-signé (production du certificat + installation).
- Créer une configuration HTTPS permettant de :
    - Interroger le serveur Web en backend.
    - Fournir au client la page provenant du serveur Web.
- Mettre en place une politique stricte :
    - HTTP doit rediriger systématiquement vers HTTPS.
    - Le reverse proxy ne doit accepter **que** des connexions en HTTPS.

---

### **4.4 Tests fonctionnels**

Les tests à réaliser et à prouver dans votre rapport :

- Test SSH :    
    - Connexion réussie seulement avec la clé.
    - Tentative depuis une autre IP : échec.
- Test HTTP/HTTPS :
    - HTTP → doit rediriger vers HTTPS.
    - HTTPS → doit afficher correctement votre site.
- Vérification que le reverse proxy transmet bien les données du serveur Web.

---

## **5. Rapport professionnel à rendre**

Votre rapport doit être rédigé comme si vous vous adressiez à un **client professionnel**.  
Il doit être structuré, clair, propre, et contenir :

### Page de garde

### Sommaire automatique

### Introduction du projet

### Détail de l’architecture (schéma obligatoire)

### Démarche détaillée (sans copie de commandes brutes)

### Captures d’écran commentées

(démontrant la mise en place de chaque étape)

### Tests et validation (preuves, captures, explications)

### Conclusion et recommandations de sécurité supplémentaires

Toutes les images doivent être nettes, lisibles et accompagnées d’une explication.

---

## **6. Critères d’évaluation**

|Critère|Points|
|---|---|
|Sécurisation Linux (sudo, root désactivé, SSH sécurisé)|25|
|Mise en place du serveur Web|20|
|Mise en place du reverse proxy|25|
|HTTPS + politique de sécurité|20|
|Rapport professionnel et qualité des preuves|10|
|**Total**|**100**|