# TP 2 — Sécurisation d'une infrastructure réseau avec VPC


---

## Architecture à réaliser

```
                Internet
                   |
            Internet Gateway
                   |
              Public Subnet
                   |
              EC2 Web Server
                   |
             Private Subnet
                   |
             Database Server
```

---

## Étapes

### 1. Créer un VPC

Paramètres :

```
Nom : Secure-VPC
CIDR : 10.0.0.0/16
```

---

### 2. Créer les sous-réseaux

Public :

```
10.0.1.0/24
```

Privé :

```
10.0.2.0/24
```

---

### 3. Security Group Web

Autoriser :

|Protocol|Port|Source|
|---|---|---|
|HTTP|80|0.0.0.0/0|
|HTTPS|443|0.0.0.0/0|
|SSH|22|IP étudiant|

---

### 4. Security Group Database

Autoriser :

```
MYSQL 3306
Source :
Security Group Web
```

---

## Questions

1. Pourquoi la base de données ne doit-elle pas être publique ?
2. Quelle différence entre Security Group et NACL ?
3. Pourquoi limiter SSH ?