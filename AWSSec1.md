## TP 1 — Gestion des identités et des accès avec IAM (Least Privilege)


---

## Partie 1 : Création des utilisateurs

Créer les utilisateurs suivants :

|Utilisateur|Rôle|
|---|---|
|alice|Administrateur système|
|bob|Développeur|
|charlie|Auditeur sécurité|

Créer les groupes :

- `Admins`
- `Developers`
- `SecurityAuditors`

---

## Partie 2 : Attribution des permissions

Associer les policies :

### Admins

Policy :

```
AdministratorAccess
```

### Developers

Créer une policy :

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:*",
        "s3:*"
      ],
      "Resource": "*"
    }
  ]
}
```

### Auditeurs

Créer :

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:Describe*",
        "s3:Get*",
        "cloudtrail:LookupEvents"
      ],
      "Resource": "*"
    }
  ]
}
```