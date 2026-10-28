#### **1. Client Hello (Initiation du client)**

Le client envoie un message **ClientHello** au serveur, contenant :

- Une liste des **versions TLS** qu’il supporte (ex. TLS 1.2, TLS 1.3).
- Une liste des **suites cryptographiques** qu’il peut utiliser (ex. RSA, AES).
- Un **identifiant aléatoire** (appelé _client random_), qui sera utilisé pour générer la clé de session.

---

#### **2. Server Hello (Réponse du serveur)**

Le serveur répond avec un message **ServerHello**, contenant :

- La **version TLS** choisie.
- La **suite cryptographique** sélectionnée.
- Son propre **identifiant aléatoire** (_server random_).
- Le **certificat X.509** du serveur (inclut sa clé publique RSA).

Ce certificat prouve l’identité du serveur et contient la clé publique RSA, qui sera utilisée pour chiffrer les données.

---

#### **3. Vérification du certificat (par le client)**

Le client effectue plusieurs vérifications sur le certificat du serveur :

- Est-il signé par une **Autorité de Certification (CA)** de confiance ?
- Le certificat est-il encore valide (non expiré et non révoqué) ?
- Le nom de domaine correspond-il à celui dans le certificat ?

Si ces vérifications échouent, la connexion est interrompue.

---

#### **4. Génération et chiffrement de la clé de session (Pre-Master Secret)**

- Le client génère une valeur appelée **pre-master secret**.
- Cette valeur est ensuite chiffrée avec la **clé publique RSA** extraite du certificat du serveur.
- Le client envoie ce **pre-master secret chiffré** au serveur.

---

#### **5. Déchiffrement par le serveur**

- Le serveur utilise sa **clé privée RSA** pour déchiffrer le **pre-master secret**.
- Maintenant, le serveur et le client ont tous les deux accès au même **pre-master secret**.

---

#### **6. Génération de la clé de session**

À partir du **pre-master secret**, le client et le serveur utilisent un algorithme dérivé (généralement HMAC) pour générer une **clé de session symétrique**, en combinant :

- Le **pre-master secret**.
- Le **client random** et le **server random**.

Cette clé de session sera utilisée pour chiffrer toutes les communications futures avec un algorithme symétrique (ex. AES).

---

#### **7. Change Cipher Spec et Finished**

- Le client et le serveur envoient un message **ChangeCipherSpec** pour signaler qu’ils vont maintenant utiliser le chiffrement symétrique.
- Chaque partie envoie un message **Finished** (chiffré avec la clé de session) pour confirmer que le handshake s’est bien déroulé.

---