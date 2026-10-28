# 🧪 **1. Nœuds pour le Forensics (DFIR)**

## 📂 Acquisition & Préservation

- Image disque (type, outil, hash)
    
- Capture mémoire (RAM)
    
- Acquisition mobile
    
- Acquisition réseau (PCAP)
    
- Horodatage / Chaîne de conservation (chain of custody)

aazeaze
    

## 🔍 Analyse artefacts système

- Journaux système (Windows / Linux)
    
- Registre Windows (hives, run keys)
    
- Services & tâches planifiées
    
- Historique fichiers (LNK, Prefetch)
    
- Artefacts utilisateurs (browser history, cookies)
    
- Artefacts d’exécution (SRUM, Shimcache)
    

## 🕸️ Analyse réseau

- Sessions réseau détectées
    
- Anomalies de trafic
    
- Indicateurs de compromission (IOC) réseau
    
- Connexions persistantes / C2 suspected
    

## 🧬 Analyse malwares (sans exécution)

- Classification (trojan, dropper, loader…)
    
- Hashes & métadonnées
    
- Strings / comportements déclaratifs
    
- TTP liés (MITRE)
    

## 🛠️ Timeline

- Ligne du temps des événements
    
- Actions utilisateur vs actions système
    
- Pivot sur événements suspects
    

## 🧾 Reporting / Résumé

- Constat incident
    
- Impact & gravité
    
- Recommandations
    

---

# 📡 **2. Nœuds pour la Sécurité IoT**

## 📦 Dispositif & Architecture

- Type d’appareil (caméra, capteur, robot…)
    
- OS & firmware
    
- Protocoles supportés
    
- Architecture réseau autour de l’appareil
    

## 🔌 Interfaces et protocoles

- UART / JTAG / SWD (juste documentation)
    
- USB
    
- Wi-Fi / BLE / ZigBee / Z-Wave / LoRa
    
- Protocole applicatif (MQTT, CoAP, Modbus/TCP)
    

## 🔐 Sécurité de l’appareil

- Gestion des identifiants
    
- Chiffrement utilisé
    
- Hardening (ou absence)
    
- Mécanismes de mise à jour
    

## 📡 Analyse du Firmware (niveau métadonnées)

- Format (bin, img, squashfs…)
    
- Extraction réussie / non réussie
    
- Fichiers sensibles trouvés
    
- Certificats / clés exposés (sans détail technique)
    

## 📊 Interactions Cloud / API

- Endpoints découverts
    
- Authentification
    
- Permissions
    

## 🚨 Vulnérabilités & risques

- Exposition des services
    
- Points faibles de configuration
    
- Communication non sécurisée
    

---

# 🧬 **3. Nœuds pour le Reverse Engineering (orienté organisation du travail)**

## 🗂️ Artefact analysé

- Binaire / APK / Firmware
    
- Plateforme (ARM, x86, MIPS…)
    
- Format (ELF, PE, Mach-O)
    

## 🔍 Analyse statique (haute-level)

- Imports / librairies
    
- Sections importantes
    
- Obfuscation détectée
    
- Dépendances
    
- Strings principales
    

## 🧭 Cartographie logique

- Modules
    
- Classes / fonctions clés
    
- Flots de logique
    
- Schémas internes (state machine)
    

## 🔐 Sécurité & intégrité

- Signatures ou protections (hash, signature)
    
- Contrôles anti-debug / anti-tamper (mention sans expliquer contournement)
    
- Chiffrement (type, usage)
    

## 🧪 Analyse comportementale (sans exécution guidée)

- Permissions (mobile)
    
- Points d’entrée / triggers
    
- Communication réseau déclarative (domains, endpoints)
    

## 📚 Références / Liens MITRE

- Techniques rencontrées
    
- Groupes ou malwares associés
    

---

# 🛠️ **4. Nœuds transverses (utiles pour les 3 domaines)**

### **📚 Sources & documentation**

- Rapport initial
    
- Notes techniques
    
- Liens externes
    
- Livrables clients
    

### **🧩 Indicateurs de compromission (IOC)**

- Hashes
    
- Domains
    
- IP
    
- Fichiers
    
- Processus
    

### **👥 Collaborateurs / Rôles**

- Analyste SOC
    
- Reverse engineer
    
- Forensic analyst
    

### **📈 Statuts / Workflow**

- À analyser
    
- Analyse en cours
    
- Confirmé
    
- À reporter