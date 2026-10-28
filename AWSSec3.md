# TP 3 — Sécurité des données avec S3

## Objectifs

- Sécuriser le stockage Cloud
- Comprendre les erreurs fréquentes
- Utiliser le chiffrement

---

## Partie 1

Créer un bucket :

```
secure-data-etudiant
```

Activer :

Block Public Access  
Versioning  
Encryption AES-256

---

## Partie 2 : Mauvaise configuration

Créer une policy publique :

```
{
 "Effect":"Allow",
 "Principal":"*",
 "Action":"s3:GetObject",
 "Resource":"arn:aws:s3:::secure-data-etudiant/*"
}
```

Observer le risque.

---