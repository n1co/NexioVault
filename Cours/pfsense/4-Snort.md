https://leblogdolivyeahh.wordpress.com/2020/08/27/pfsense-snort-detection-dintrusion/

sudo nmap 192.168.1.0/24 -sV -sS -p- -vv 


Dans **Snort**, les "modes de recherche" (search modes) déterminent les algorithmes utilisés pour effectuer la détection des correspondances de signatures dans le trafic réseau. Ces algorithmes sont optimisés pour des scénarios spécifiques, en tenant compte des compromis entre vitesse, utilisation de la mémoire et précision. Voici une explication des principaux modes mentionnés :

---

### 1. **AC-BNFA (Aho-Corasick with BNFA)**

**Description :**

- Basé sur l'algorithme **Aho-Corasick**, qui construit un automate fini pour trouver des motifs multiples dans un texte.
- "BNFA" signifie "Bit-mapped NFA" (Non-deterministic Finite Automaton). Ce mode utilise des structures compactes pour réduire la mémoire utilisée par les transitions de l'automate.

**Usage :**

- Adapté pour les environnements ayant des limitations de mémoire.
- Bon équilibre entre vitesse et utilisation de mémoire.

---

### 2. **AC-SPLIT**

**Description :**

- Variante de Aho-Corasick divisant l'automate en plusieurs sections.
- Optimise les performances en réduisant les coûts liés à la gestion des transitions.

**Usage :**

- Utile dans les environnements où la latence de détection est critique.

---

### 3. **LOWMEM (Low Memory)**

**Description :**

- Optimisé pour une faible consommation de mémoire.
- Réduit la taille de l'automate en simplifiant les transitions et les structures de données associées.

**Usage :**

- Idéal pour des systèmes avec peu de mémoire disponible.
- Sacrifie potentiellement la vitesse pour économiser de la mémoire.

---

### 4. **AC-STD (Aho-Corasick Standard)**

**Description :**

- Implémente l'algorithme **Aho-Corasick** standard sans optimisation particulière.
- Construit un arbre de transitions pour matcher efficacement des motifs multiples.

**Usage :**

- Performances générales solides.
- Convient aux systèmes avec suffisamment de ressources.

---

### 5. **AC (Aho-Corasick)**

**Description :**

- Algorithme de base Aho-Corasick.
- Très rapide pour des correspondances multiples, mais consomme plus de mémoire.

**Usage :**

- Meilleur choix lorsque la rapidité est prioritaire et que les ressources mémoire ne sont pas limitées.

---

### 6. **AC-NQ (Aho-Corasick No Queue)**

**Description :**

- Variante de l'algorithme Aho-Corasick qui évite l'utilisation de files d'attente pour réduire la surcharge mémoire.
- Utilise des structures alternatives pour la gestion des transitions.

**Usage :**

- Réduction de l'utilisation de mémoire sans trop sacrifier les performances.

---

### 7. **AC-BNFA-NQ (BNFA avec No Queue)**

**Description :**

- Combine l'optimisation BNFA avec la suppression des files d'attente.
- Réduit encore davantage la mémoire requise par rapport à AC-BNFA classique.

**Usage :**

- Environnements à mémoire très limitée, avec une priorité donnée à la conservation des ressources.

---

### 8. **LOWMEM-NQ (Low Memory No Queue)**

**Description :**

- Version optimisée de LOWMEM qui supprime l'utilisation des files d'attente pour économiser encore plus de mémoire.
- Sacrifie des performances supplémentaires.

**Usage :**

- Adapté aux appareils embarqués ou aux systèmes avec des ressources extrêmement restreintes.

---

### 9. **AC-BANDED**

**Description :**

- Divise les motifs en bandes pour mieux répartir les recherches et limiter les transitions inutiles.
- Optimise les performances dans les cas où les motifs peuvent être regroupés efficacement.

**Usage :**

- Environnements où les motifs peuvent être segmentés naturellement en groupes.

---

### 10. **AC-SPARSEBANDS**

**Description :**

- Variante de AC-BANDED avec une optimisation pour les motifs peu fréquents ou éparpillés.
- Évite de surcharger la mémoire avec des structures inutilisées.

**Usage :**

- Trafic contenant des signatures peu fréquentes ou des motifs distants.

---

### 11. **ACS (Aho-Corasick Sparse)**

**Description :**

- Basé sur une version allégée de Aho-Corasick.
- Économise de la mémoire en gérant les transitions de manière éparse (sparse).

**Usage :**

- Environnements nécessitant un équilibre entre mémoire et vitesse, mais sans les optimisations complètes des autres variantes.

---

### Résumé des choix :

- **Pour des performances maximales :** `AC`, `AC-STD`.
- **Pour économiser la mémoire :** `LOWMEM`, `AC-BNFA`, `LOWMEM-NQ`.
- **Pour des environnements limités :** `AC-NQ`, `LOWMEM-NQ`.
- **Pour des motifs peu fréquents :** `AC-SPARSEBANDS`.

Le choix dépend principalement des contraintes de votre environnement (mémoire disponible, charge réseau) et des priorités (rapidité ou économie de ressources).