ça peut avoir un interet d'avoir l'IPS/IDS sur le firewall (moins de latence éventuellement)
MAIS
ça expose les couches bas niveau

Virtualisé:
ça expose des trucs
perte de perf (checksum offloading)

### 1. **Concurrence pour les ressources**

- **CPU, RAM, et bande passante** sont partagés entre les deux systèmes.
    
- IDS/IPS peut être très gourmand (analyse de paquets en profondeur, inspection comportementale).
    
- Cela peut entraîner des ralentissements, des délais de traitement, voire des pertes de paquets.
    

---

### 🔻 2. **Point de défaillance unique**

- Si la machine tombe en panne ou est compromise, **les deux systèmes sont affectés**.
    
- Cela rend le réseau **plus vulnérable** qu’avec une architecture distribuée.
    

---

### 🔻 3. **Moins de flexibilité dans la gestion**

- Il est plus difficile de configurer, maintenir et mettre à jour deux systèmes critiques sur la même machine.
    
- Problèmes potentiels de **compatibilité logicielle** (ex. : conflits de règles, interfaces réseau partagées).
    

---

### 🔻 4. **Réduction de la visibilité IDS/IPS**

- Si l’IDS/IPS est **installé derrière le pare-feu**, il ne verra **que le trafic filtré**, et non tout le trafic entrant/sortant brut.
    
- Cela **limite l’efficacité** de la détection (surtout pour les menaces que le pare-feu laisse passer).
    

---

### 🔻 5. **Sécurité réduite**

- Un attaquant qui compromet le système a **accès à deux fonctions critiques** : filtrage et détection.
    
- Mieux vaut **séparer les rôles** pour limiter l’impact d’un incident.
    

---

### 🔻 6. **Scalabilité réduite**

- Si ton réseau grandit, cette solution deviendra rapidement un **goulot d’étranglement**.
    
- Les solutions modulaires (pare-feu dédié + IDS/IPS séparé) sont plus évolutives.