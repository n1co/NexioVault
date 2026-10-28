
```lua
                            +--------------------+
                            | Autorité Racine    |
                            | (Root CA)          |
                            | Contient :         |
                            | - Clé privée       |
                            | - Certificat de    |
                            |   confiance        |
                            +--------------------+
                                      |
                                      v
                            +--------------------+
                            | Autorité Intermédiaire|
                            | (Intermediate CA)     |
                            | Contient :            |
                            | - Clé privée          |
                            | - Certificat signé    |
                            +--------------------+
                                      |
                           Émission de certificats
                                      |
                 +---------------------------+
                 | Autorité d'enregistrement |
                 | (RA - Registration Auth)  |
                 | Vérifie l'identité du     |
                 | client/serveur.           |
                 +---------------------------+
                                      |
                             Demande de certificat
                                      |
+--------------------+         +--------------------+
| CLIENT             |         | SERVEUR           |
| Contient :         |         | Contient :        |
| - Clé privée       | <-----> | - Clé privée      |
| - Certificat signé |         | - Certificat signé|
| - Demande un       |         | - Protège les     |
|   certificat à la  |         |   ressources et   |
|   CA via la RA     |         |   données.        |
+--------------------+         +--------------------+

          | Communication Sécurisée (SSL/TLS) |
          +-----------------------------------+
                       Tunnel Chiffré

Validation des certificats :
- Liste de révocation des certificats (CRL) : vérifie si un certificat est invalide.
- Protocole OCSP (Online Certificate Status Protocol) : vérifie en temps réel si un certificat est valide.

```

### Explications des composants :

1. **Autorité Racine (Root CA)** : L'entité suprême de confiance. Elle contient :
    
    - Une **clé privée** très protégée pour signer les certificats des autorités intermédiaires ou des entités finales.
    - Un **certificat** qui garantit son identité.
2. **Autorité Intermédiaire (Intermediate CA)** : Délègue la création de certificats. Elle contient :
    
    - Sa propre **clé privée**.
    - Un **certificat** signé par l'autorité racine.
3. **Autorité d'enregistrement (RA)** : Vérifie l'identité des utilisateurs ou des serveurs avant d'envoyer leur demande à l'autorité de certification.
    
4. **Client** :
    
    - Contient une **clé privée** utilisée pour chiffrer et signer les données.
    - Possède un **certificat** délivré par une autorité de certification.
5. **Serveur** :
    
    - Contient une **clé privée** qui garantit que les communications sont sécurisées.
    - Possède un **certificat** utilisé pour prouver son identité aux clients.
6. **Communication SSL/TLS** :
    
    - Permet un échange sécurisé entre le client et le serveur en chiffrant les données.
    - Utilise les clés privées et les certificats de chaque partie.
7. **Validation des certificats** :
    
    - Le client vérifie le certificat du serveur via une **CRL** ou une requête **OCSP** pour s'assurer qu'il est toujours valide.