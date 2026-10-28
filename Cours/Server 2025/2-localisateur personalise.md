
## **À quoi ça sert**

Le **DC Locator** est le mécanisme qu’utilisent les clients (Windows, serveurs, applications) pour trouver **le contrôleur de domaine le plus approprié** pour une requête LDAP, Kerberos ou d’authentification.

**Pourquoi un localisateur personnalisé ?**

- Dans des environnements multi-sites ou complexes, tu peux vouloir que certains clients utilisent **un DC spécifique** plutôt que de se baser sur la logique de site Active Directory par défaut.
    
- Pour la **résilience ou la performance**, par exemple :
    
    - Rediriger les clients vers un DC dans le même site ou réseau.
        
    - Filtrer certains DC pour des services particuliers (ex : applications spécifiques).
        
- Pour **tester ou forcer le routage** sans modifier la topologie AD globale.
    

---

## **2️⃣ Comment ça fonctionne**

Windows utilise principalement :

1. **DNS SRV Records**
    
    - Les clients interrogent `_ldap._tcp.dc._msdcs.<domaine>` pour obtenir la liste des DC disponibles.
        
2. **Site AD**
    
    - Le client tente de trouver un DC dans son site local pour réduire la latence.
        
3. **Stratégies de priorité**
    
    - Si aucun DC local n’est disponible, il prend un DC d’un autre site selon les coûts de site configurés dans AD Sites and Services.
        

Un **localisateur personnalisé** intervient généralement en **modifiant la façon dont le client résout ces DC**, soit via :

- **DNS** (redirection ou ajout de SRV records spécifiques).
    
- **GPO / registre** pour forcer un DC précis.
    
- **Scripts ou configuration d’application** pour utiliser un serveur LDAP spécifique.
    

---

## **3️⃣ Mise en place d’un localisateur de DC personnalisé**

### **Méthode 1 : via le registre (client Windows)**

1. Ouvre l’Éditeur de registre (`regedit`).
    
2. Navigue jusqu’à :
    

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters`

3. Crée ou modifie la valeur :
    

- **Name:** `DSDomainName` → le nom de ton domaine.
    
- **Name:** `DCName` → le nom complet du DC que tu veux forcer.
    

4. Redémarre le service **Netlogon** ou le PC pour que la configuration prenne effet.
    

> ⚠️ Attention : cette méthode force le client à **utiliser un DC spécifique**, ce qui peut poser problème si ce DC est indisponible.

---

### **Méthode 2 : via DNS personnalisé**

- Crée un enregistrement **SRV** spécifique pour ton DC personnalisé dans DNS.
    
- Les clients qui interrogent ce SRV pointeront vers ce DC.
    
- Utile si tu veux qu’une application spécifique trouve un DC particulier sans toucher aux clients Windows globalement.
    

---

### **Méthode 3 : via configuration d’application**

- Certaines applications (Exchange, SQL Server, etc.) permettent de **forcer le DC LDAP ou Global Catalog** via un fichier de configuration ou paramètre.
    
- C’est le moyen le plus sûr si tu ne veux pas modifier tous les clients.
    

---

## **4️⃣ Bonnes pratiques**

- Ne force le DC que si nécessaire, sinon laisse le **mécanisme automatique d’AD** choisir le meilleur DC.
    
- Assure-toi que le DC choisi est **répliqué et disponible**.
    
- Documente toujours les exceptions pour la maintenance.