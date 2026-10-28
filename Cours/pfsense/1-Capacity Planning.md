Le **Capacity Planning** sur pfSense consiste à évaluer et à allouer les ressources nécessaires (comme le processeur, la mémoire, et la bande passante) pour garantir des performances optimales de votre pare-feu/routeur en fonction des besoins actuels et futurs de votre réseau.

### Objectifs du Capacity Planning sur pfSense :

1. **Éviter les goulets d'étranglement** : Assurer que le pare-feu peut gérer la charge réseau (trafic entrant et sortant) sans ralentissement.
2. **Prévoir la montée en charge** : Anticiper les besoins futurs en cas d'augmentation du trafic ou d'ajout d'utilisateurs, de services ou de fonctionnalités.
3. **Optimiser les performances** : Dimensionner correctement le matériel (CPU, RAM, stockage) pour éviter des coûts excessifs ou une sous-utilisation des ressources.

---

### Étapes du Capacity Planning sur pfSense :

#### 1. **Analyse des besoins actuels**

- **Nombre d'utilisateurs** : Combien de périphériques ou d'utilisateurs connectés simultanément ?
- **Type de trafic** : Quels types de flux traversent pfSense ? (par exemple, navigation Web, VoIP, VPN, téléchargement P2P).
- **Débit réseau** : Quelle est la vitesse de connexion Internet et le trafic maximal prévu (en Mbit/s ou Gbit/s) ?
- **Services actifs** : Quels modules sont utilisés dans pfSense, tels que :
    - **VPN (OpenVPN, IPsec)** : Consommateurs de CPU pour le chiffrement/déchiffrement.
    - **IDS/IPS (Snort, Suricata)** : Besoin de RAM et de CPU élevé.
    - **Filtrage web (Squid, SquidGuard)** : Augmente l'utilisation du stockage et de la RAM.
    - **QoS (Limiters, Traffic Shaping)** : Exige une gestion efficace des ressources.
- **Haute disponibilité** : Si le système est configuré en mode CARP (failover), cela impacte la charge.

#### 2. **Évaluation matérielle**

- **Processeur (CPU)** :
    - Les fonctionnalités comme le VPN (chiffrement AES), IDS/IPS ou QoS nécessitent un processeur performant.
    - Préférez des processeurs avec plusieurs cœurs et des capacités de chiffrement matériel (ex. AES-NI).
- **Mémoire vive (RAM)** :
    - La quantité de RAM dépend du nombre de connexions simultanées et des services activés.
    - Exemples :
        - Environ 1 Go de RAM pour les fonctions de base.
        - Ajoutez 2 à 4 Go si vous utilisez des services comme IDS/IPS, VPN ou un proxy web.
- **Stockage** :
    - Les logs, les caches proxy ou les sauvegardes de configuration consomment de l'espace.
    - SSD recommandé pour une meilleure performance.
- **Interfaces réseau** :
    - Interfaces Gigabit ou supérieures en fonction du débit Internet et intranet.
    - Prévoir une carte réseau de qualité pour gérer le trafic élevé.

#### 3. **Simulation et tests**

- Effectuez une **simulation de charge** pour identifier les limites actuelles du matériel.
- Utilisez les outils intégrés de pfSense pour surveiller :
    - **Graphiques RRD** pour le CPU, la mémoire, et la bande passante.
    - **Statistiques d'état** pour surveiller le nombre de connexions actives.

#### 4. **Dimensionnement futur**

- Tenez compte de la croissance prévue du réseau :
    - Augmentation des utilisateurs.
    - Déploiement de nouveaux services (VPN supplémentaires, VoIP, etc.).
- Surdimensionnez légèrement pour gérer les pics de trafic.

#### 5. **Surveillance continue**

- Utilisez des outils comme **Zabbix** ou **Nagios** pour surveiller en permanence les performances.
- Analysez les tendances pour ajuster le matériel ou reconfigurer pfSense.

---

### Exemple pratique

Un réseau de 100 utilisateurs avec 1 Gbit/s de débit et utilisant un VPN pour 50 utilisateurs simultanés pourrait nécessiter :

- **Processeur** : Quad-core avec support AES-NI.
- **RAM** : 8 Go pour gérer les connexions et les services comme IDS/IPS.
- **Stockage** : SSD de 64 à 128 Go pour les logs et le cache proxy.
- **Interfaces réseau** : Cartes réseau Gigabit ou 10G en fonction de l'infrastructure.

---

Avec un bon **capacity planning**, pfSense peut évoluer avec les besoins de votre réseau tout en maintenant une performance stable et fiable.