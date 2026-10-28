## Étape 2 — Forcer une structure compatible graphique

Même si tu vois `_time`, Splunk veut une structure “key/value” lisible par `timechart`.  
Ta recherche doit ressembler **exactement** à ceci :

`index=* ("Failed password" OR "Invalid user" OR "authentication failure") | rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+)" | timechart span=1h count by src_ip`

⚠️ Le mot-clé `timechart` est **ce qui déclenche la génération de graphiques**.  
Si tu utilises `stats count by _time, src_ip`, Splunk te montre une table, **mais pas de graphique par défaut**.

👉 Donc **remplace `stats` par `timechart`**.

---

## 🧭 Étape 3 — Vérifie le type de visualisation

Une fois que la recherche tourne :

- Clique sur **Visualization**.
    
- En haut à droite, tu devrais avoir un **menu déroulant “Visualization Type”**.
    
- Choisis **Line Chart**, **Area Chart**, ou **Column Chart**.
    

---

## ✅ Étape 4 — Sauvegarder dans un dashboard

Quand le graphique s’affiche bien :

1. Clique sur **Save As → Dashboard Panel**.
    
2. Sélectionne ton dashboard ou crée-en un nouveau.
    
3. Donne un titre (ex. `Échecs SSH dans le temps`).
    
4. Visualisation : `Line Chart`.
    
5. Sauvegarde ✅