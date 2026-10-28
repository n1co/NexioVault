# Mise en place d'une PKI sur Debian

> **Environnement cible :** Debian 12 (Bookworm) — adaptable à Debian 11  
> **Outil principal :** OpenSSL  
> **Architecture :** CA racine (Root CA) → CA intermédiaire (Intermediate CA) → Certificats finaux

---

## Architecture de la PKI

```
Root CA (hors ligne recommandé)
    └── Intermediate CA (en ligne)
            ├── Certificat serveur (TLS/HTTPS)
            ├── Certificat client (authentification)
            └── Certificat de signature de code
```

---

## Étape 1 — Prérequis et préparation

```bash
# Mettre à jour le système
sudo apt update && sudo apt upgrade -y

# Installer OpenSSL (généralement déjà présent)
sudo apt install openssl -y

# Vérifier la version
openssl version
```

Créer la structure de répertoires :

```bash
# Répertoire de travail principal
sudo mkdir -p /etc/pki/{root-ca,intermediate-ca}

# Structure Root CA
sudo mkdir -p /etc/pki/root-ca/{certs,crl,newcerts,private,requests}
sudo chmod 700 /etc/pki/root-ca/private
sudo touch /etc/pki/root-ca/index.txt
echo "1000" | sudo tee /etc/pki/root-ca/serial
echo "1000" | sudo tee /etc/pki/root-ca/crlnumber

# Structure Intermediate CA
sudo mkdir -p /etc/pki/intermediate-ca/{certs,crl,newcerts,private,requests}
sudo chmod 700 /etc/pki/intermediate-ca/private
sudo touch /etc/pki/intermediate-ca/index.txt
echo "1000" | sudo tee /etc/pki/intermediate-ca/serial
echo "1000" | sudo tee /etc/pki/intermediate-ca/crlnumber
```

---

## Étape 2 — Configuration OpenSSL pour la Root CA

Créer le fichier de configuration `/etc/pki/root-ca/openssl.cnf` :

```ini
[ ca ]
default_ca = CA_default

[ CA_default ]
dir               = /etc/pki/root-ca
certs             = $dir/certs
crl_dir           = $dir/crl
new_certs_dir     = $dir/newcerts
database          = $dir/index.txt
serial            = $dir/serial
RANDFILE          = $dir/private/.rand

private_key       = $dir/private/ca.key.pem
certificate       = $dir/certs/ca.cert.pem

crlnumber         = $dir/crlnumber
crl               = $dir/crl/ca.crl.pem
crl_extensions    = crl_ext
default_crl_days  = 30

default_md        = sha256
name_opt          = ca_default
cert_opt          = ca_default
default_days      = 3650
preserve          = no
policy            = policy_strict

[ policy_strict ]
countryName             = match
stateOrProvinceName     = match
organizationName        = match
organizationalUnitName  = optional
commonName              = supplied
emailAddress            = optional

[ policy_loose ]
countryName             = optional
stateOrProvinceName     = optional
localityName            = optional
organizationName        = optional
organizationalUnitName  = optional
commonName              = supplied
emailAddress            = optional

[ req ]
default_bits        = 4096
distinguished_name  = req_distinguished_name
string_mask         = utf8only
default_md          = sha256
x509_extensions     = v3_ca
prompt              = no

[ req_distinguished_name ]
countryName                     = FR
stateOrProvinceName             = Ile-de-France
localityName                    = Paris
0.organizationName              = MonEntreprise
organizationalUnitName          = IT
commonName                      = MonEntreprise Root CA
emailAddress                    = pki@monentreprise.fr

[ v3_ca ]
subjectKeyIdentifier  = hash
authorityKeyIdentifier = keyid:always,issuer
basicConstraints      = critical, CA:true
keyUsage              = critical, digitalSignature, cRLSign, keyCertSign

[ v3_intermediate_ca ]
subjectKeyIdentifier  = hash
authorityKeyIdentifier = keyid:always,issuer
basicConstraints      = critical, CA:true, pathlen:0
keyUsage              = critical, digitalSignature, cRLSign, keyCertSign

[ usr_cert ]
basicConstraints      = CA:FALSE
nsCertType            = client, email
nsComment             = "OpenSSL Generated Client Certificate"
subjectKeyIdentifier  = hash
authorityKeyIdentifier = keyid,issuer
keyUsage              = critical, nonRepudiation, digitalSignature, keyEncipherment
extendedKeyUsage      = clientAuth, emailProtection

[ server_cert ]
basicConstraints      = CA:FALSE
nsCertType            = server
nsComment             = "OpenSSL Generated Server Certificate"
subjectKeyIdentifier  = hash
authorityKeyIdentifier = keyid,issuer
keyUsage              = critical, digitalSignature, keyEncipherment
extendedKeyUsage      = serverAuth

[ crl_ext ]
authorityKeyIdentifier = keyid:always

[ ocsp ]
basicConstraints      = CA:FALSE
subjectKeyIdentifier  = hash
authorityKeyIdentifier = keyid,issuer
keyUsage              = critical, digitalSignature
extendedKeyUsage      = critical, OCSPSigning
```

---

## Étape 3 — Création de la Root CA

### 3.1 Générer la clé privée Root CA

```bash
cd /etc/pki/root-ca

# Générer une clé RSA 4096 bits chiffrée avec AES-256
sudo openssl genrsa -aes256 -out private/ca.key.pem 4096

# Sécuriser les permissions
sudo chmod 400 private/ca.key.pem
```

> **Important :** Le mot de passe saisi ici protège la clé racine. Choisissez-en un fort et conservez-le précieusement.

### 3.2 Créer le certificat Root CA auto-signé

```bash
sudo openssl req -config openssl.cnf \
    -key private/ca.key.pem \
    -new -x509 \
    -days 7300 \
    -sha256 \
    -extensions v3_ca \
    -out certs/ca.cert.pem

# Sécuriser le certificat
sudo chmod 444 certs/ca.cert.pem
```

### 3.3 Vérifier le certificat Root CA

```bash
sudo openssl x509 -noout -text -in certs/ca.cert.pem
```

Vérifier notamment :

- `Issuer` et `Subject` identiques (auto-signé)
- `CA:TRUE` dans les extensions
- Durée de validité (20 ans)

---

## Étape 4 — Configuration OpenSSL pour la CA intermédiaire

Créer `/etc/pki/intermediate-ca/openssl.cnf` :

```ini
[ ca ]
default_ca = CA_default

[ CA_default ]
dir               = /etc/pki/intermediate-ca
certs             = $dir/certs
crl_dir           = $dir/crl
new_certs_dir     = $dir/newcerts
database          = $dir/index.txt
serial            = $dir/serial
RANDFILE          = $dir/private/.rand

private_key       = $dir/private/intermediate.key.pem
certificate       = $dir/certs/intermediate.cert.pem

crlnumber         = $dir/crlnumber
crl               = $dir/crl/intermediate.crl.pem
crl_extensions    = crl_ext
default_crl_days  = 30

default_md        = sha256
name_opt          = ca_default
cert_opt          = ca_default
default_days      = 375
preserve          = no
policy            = policy_loose

[ policy_strict ]
countryName             = match
stateOrProvinceName     = match
organizationName        = match
organizationalUnitName  = optional
commonName              = supplied
emailAddress            = optional

[ policy_loose ]
countryName             = optional
stateOrProvinceName     = optional
localityName            = optional
organizationName        = optional
organizationalUnitName  = optional
commonName              = supplied
emailAddress            = optional

[ req ]
default_bits        = 4096
distinguished_name  = req_distinguished_name
string_mask         = utf8only
default_md          = sha256
x509_extensions     = v3_ca
prompt              = no

[ req_distinguished_name ]
countryName                     = FR
stateOrProvinceName             = Ile-de-France
localityName                    = Paris
0.organizationName              = MonEntreprise
organizationalUnitName          = IT
commonName                      = MonEntreprise Intermediate CA
emailAddress                    = pki@monentreprise.fr

[ v3_ca ]
subjectKeyIdentifier  = hash
authorityKeyIdentifier = keyid:always,issuer
basicConstraints      = critical, CA:true
keyUsage              = critical, digitalSignature, cRLSign, keyCertSign

[ v3_intermediate_ca ]
subjectKeyIdentifier  = hash
authorityKeyIdentifier = keyid:always,issuer
basicConstraints      = critical, CA:true, pathlen:0
keyUsage              = critical, digitalSignature, cRLSign, keyCertSign

[ usr_cert ]
basicConstraints      = CA:FALSE
nsCertType            = client, email
nsComment             = "OpenSSL Generated Client Certificate"
subjectKeyIdentifier  = hash
authorityKeyIdentifier = keyid,issuer
keyUsage              = critical, nonRepudiation, digitalSignature, keyEncipherment
extendedKeyUsage      = clientAuth, emailProtection

[ server_cert ]
basicConstraints      = CA:FALSE
nsCertType            = server
nsComment             = "OpenSSL Generated Server Certificate"
subjectKeyIdentifier  = hash
authorityKeyIdentifier = keyid,issuer
keyUsage              = critical, digitalSignature, keyEncipherment
extendedKeyUsage      = serverAuth

[ crl_ext ]
authorityKeyIdentifier = keyid:always

[ ocsp ]
basicConstraints      = CA:FALSE
subjectKeyIdentifier  = hash
authorityKeyIdentifier = keyid,issuer
keyUsage              = critical, digitalSignature
extendedKeyUsage      = critical, OCSPSigning
```

---

## Étape 5 — Création de la CA intermédiaire

### 5.1 Générer la clé privée intermédiaire

```bash
cd /etc/pki/intermediate-ca

sudo openssl genrsa -aes256 -out private/intermediate.key.pem 4096
sudo chmod 400 private/intermediate.key.pem
```

### 5.2 Créer la CSR (Certificate Signing Request)

```bash
sudo openssl req -config openssl.cnf \
    -new -sha256 \
    -key private/intermediate.key.pem \
    -out requests/intermediate.csr.pem
```

### 5.3 Signer la CSR avec la Root CA

```bash
cd /etc/pki/root-ca

sudo openssl ca -config openssl.cnf \
    -extensions v3_intermediate_ca \
    -days 3650 \
    -notext \
    -md sha256 \
    -in /etc/pki/intermediate-ca/requests/intermediate.csr.pem \
    -out /etc/pki/intermediate-ca/certs/intermediate.cert.pem

sudo chmod 444 /etc/pki/intermediate-ca/certs/intermediate.cert.pem
```

### 5.4 Vérifier le certificat intermédiaire

```bash
# Vérifier le contenu
sudo openssl x509 -noout -text \
    -in /etc/pki/intermediate-ca/certs/intermediate.cert.pem

# Vérifier la chaîne de confiance
sudo openssl verify \
    -CAfile /etc/pki/root-ca/certs/ca.cert.pem \
    /etc/pki/intermediate-ca/certs/intermediate.cert.pem
```

### 5.5 Créer la chaîne de certificats (bundle)

```bash
sudo cat /etc/pki/intermediate-ca/certs/intermediate.cert.pem \
         /etc/pki/root-ca/certs/ca.cert.pem \
    | sudo tee /etc/pki/intermediate-ca/certs/ca-chain.cert.pem

sudo chmod 444 /etc/pki/intermediate-ca/certs/ca-chain.cert.pem
```

---

## Étape 6 — Émettre un certificat serveur (exemple : serveur web)

### 6.1 Générer la clé du serveur

```bash
cd /etc/pki/intermediate-ca

# Sans chiffrement (pour les services automatisés)
sudo openssl genrsa -out private/monserveur.key.pem 2048
sudo chmod 400 private/monserveur.key.pem
```

### 6.2 Créer la CSR avec SAN (Subject Alternative Names)

Créer un fichier de configuration dédié `/etc/pki/intermediate-ca/requests/monserveur.cnf` :

```ini
[ req ]
default_bits        = 2048
distinguished_name  = req_distinguished_name
req_extensions      = req_ext
prompt              = no

[ req_distinguished_name ]
countryName         = FR
stateOrProvinceName = Ile-de-France
localityName        = Paris
organizationName    = MonEntreprise
commonName          = monserveur.monentreprise.fr

[ req_ext ]
subjectAltName = @alt_names

[ alt_names ]
DNS.1   = monserveur.monentreprise.fr
DNS.2   = www.monserveur.monentreprise.fr
IP.1    = 192.168.1.10
```

```bash
sudo openssl req -config requests/monserveur.cnf \
    -key private/monserveur.key.pem \
    -new -sha256 \
    -out requests/monserveur.csr.pem
```

### 6.3 Signer avec la CA intermédiaire

```bash
sudo openssl ca -config openssl.cnf \
    -extensions server_cert \
    -days 375 \
    -notext \
    -md sha256 \
    -in requests/monserveur.csr.pem \
    -out certs/monserveur.cert.pem

sudo chmod 444 certs/monserveur.cert.pem
```

### 6.4 Vérifier le certificat serveur

```bash
# Contenu du certificat
sudo openssl x509 -noout -text -in certs/monserveur.cert.pem

# Vérification de la chaîne complète
sudo openssl verify \
    -CAfile certs/ca-chain.cert.pem \
    certs/monserveur.cert.pem
```

---

## Étape 7 — Émettre un certificat client

```bash
cd /etc/pki/intermediate-ca

# Clé client
sudo openssl genrsa -aes256 -out private/utilisateur.key.pem 2048
sudo chmod 400 private/utilisateur.key.pem

# CSR client
sudo openssl req -config openssl.cnf \
    -key private/utilisateur.key.pem \
    -new -sha256 \
    -out requests/utilisateur.csr.pem
# (renseigner CN = Prénom Nom)

# Signature
sudo openssl ca -config openssl.cnf \
    -extensions usr_cert \
    -days 375 \
    -notext \
    -md sha256 \
    -in requests/utilisateur.csr.pem \
    -out certs/utilisateur.cert.pem
```

---

## Étape 8 — Gestion de la révocation (CRL)

### 8.1 Révoquer un certificat

```bash
# Depuis la Root CA
cd /etc/pki/root-ca
sudo openssl ca -config openssl.cnf \
    -revoke /etc/pki/intermediate-ca/certs/intermediate.cert.pem

# Depuis la CA intermédiaire
cd /etc/pki/intermediate-ca
sudo openssl ca -config openssl.cnf \
    -revoke certs/monserveur.cert.pem
```

### 8.2 Générer la CRL

```bash
# CRL Root CA
cd /etc/pki/root-ca
sudo openssl ca -config openssl.cnf \
    -gencrl \
    -out crl/ca.crl.pem

# CRL CA intermédiaire
cd /etc/pki/intermediate-ca
sudo openssl ca -config openssl.cnf \
    -gencrl \
    -out crl/intermediate.crl.pem
```

### 8.3 Vérifier la CRL

```bash
sudo openssl crl -in /etc/pki/intermediate-ca/crl/intermediate.crl.pem \
    -noout -text
```

---

## Étape 9 — Déploiement de la Root CA sur les clients

### Sur les systèmes Debian/Ubuntu clients

```bash
# Copier le certificat Root CA
sudo cp /etc/pki/root-ca/certs/ca.cert.pem \
    /usr/local/share/ca-certificates/monentreprise-rootca.crt

# Mettre à jour le magasin de certificats
sudo update-ca-certificates
```

### Vérification

```bash
# Tester une connexion TLS vers le serveur signé
openssl s_client -connect monserveur.monentreprise.fr:443 \
    -CAfile /etc/pki/intermediate-ca/certs/ca-chain.cert.pem
```

---

## Récapitulatif des fichiers importants

| Fichier                                                 | Description                     | Sensibilité |
| ------------------------------------------------------- | ------------------------------- | ----------- |
| `/etc/pki/root-ca/private/ca.key.pem`                   | Clé privée Root CA              | Critique    |
| `/etc/pki/root-ca/certs/ca.cert.pem`                    | Certificat Root CA              | Public      |
| `/etc/pki/intermediate-ca/private/intermediate.key.pem` | Clé privée CA intermédiaire     | Critique    |
| `/etc/pki/intermediate-ca/certs/intermediate.cert.pem`  | Certificat CA intermédiaire     | Public      |
| `/etc/pki/intermediate-ca/certs/ca-chain.cert.pem`      | Chaîne complète                 | Public      |
| `/etc/pki/intermediate-ca/index.txt`                    | Base de données des certificats | Interne     |

---

## Bonnes pratiques de sécurité

- **Root CA hors ligne :** une fois la CA intermédiaire créée, stocker la Root CA sur un support chiffré déconnecté du réseau.
- **Mots de passe forts :** utiliser des passphrases longues (20+ caractères) pour les clés privées.
- **Sauvegardes chiffrées :** sauvegarder régulièrement `/etc/pki/` avec chiffrement (ex. GPG ou LUKS).
- **Journalisation :** activer l'audit des accès aux fichiers sensibles avec `auditd`.
- **Renouvellement :** planifier le renouvellement des certificats avant expiration (alertes à J-30).
- **Durées de validité :** Root CA 20 ans, CA intermédiaire 10 ans, certificats finaux 1 an maximum.