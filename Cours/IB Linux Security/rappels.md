  

# 🛡️ Récapitulatif Fin de Formation – Sécurité Linux

  

## 🔐 Connexion SSH par clé privée + Désactivation du mot de passe

  

```bash

ssh-keygen -t rsa -b 4096

ssh-copy-id user@serveur

```

  

Modifier `/etc/ssh/sshd_config` :

```bash

PasswordAuthentication no

PermitRootLogin no

```

  

```bash

sudo systemctl restart ssh

```

  

---

  

## 🔄 Remplacer HTTP par HTTPS dans les dépôts Ubuntu 24.04

  

```bash

sudo sed -i 's|http://|https://|g' /etc/apt/sources.list

sudo apt update

```

  

---

  

## 🔓 John + ssh2john

  

```bash

python3 /usr/share/john/ssh2john.py id_rsa > hash.txt

john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt

```

  

---

  

## 🎯 Gestion des ACL

  

```bash

setfacl -m u:alice:rwx fichier.txt

getfacl fichier.txt

```

  

---

  

## 🔒 SELinux – Base de gestion

  

```bash

sestatus

sudo setenforce 0 # permissif

sudo setenforce 1 # enforcing

```

  

Modifier `/etc/selinux/config`.

  

---

  

## 🔐 libpam_pwquality

  

```bash

sudo apt install libpam-pwquality

```

  

Modifier `/etc/pam.d/common-password` :

```

password requisite pam_pwquality.so retry=3 minlen=12 ucredit=-1 lcredit=-1 dcredit=-1 ocredit=-1

```

  

---

  

## 🌐 Apache + HTTPS

  

```bash

sudo apt install apache2

sudo a2enmod ssl

```

  

Créer certificat :

```bash

sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache.key -out /etc/ssl/certs/apache.crt

```

  

Modifier `/etc/apache2/sites-available/default-ssl.conf` et activer :

```bash

sudo a2ensite default-ssl

sudo systemctl reload apache2

```

  

---

  

## 🐙 Installer Squid

  

```bash

sudo apt install squid

sudo systemctl enable squid

sudo systemctl start squid

```

  

---

  

## 🔍 Auditd

  

```bash

sudo apt install auditd

sudo auditctl -w /etc/passwd -p wa

sudo ausearch -f /etc/passwd

```

  

---

  

## 🛡️ AIDE

  

```bash

sudo apt install aide

sudo aideinit

sudo mv /var/lib/aide/aide.db.new /var/lib/aide/aide.db

sudo aide --check

```

  

---

  

## 🌐 OpenVPN

  

```bash

sudo apt install openvpn

sudo openvpn --config client.ovpn

```

  

---

  

## 🔎 Lynis

  

```bash

sudo apt install lynis

sudo lynis audit system

```

  

---

  

## 🚫 Fail2ban

  

```bash

sudo apt install fail2ban

```

  

Fichier `/etc/fail2ban/jail.local` :

```ini

[sshd]

enabled = true

port = ssh

filter = sshd

logpath = /var/log/auth.log

maxretry = 5

```

  

```bash

sudo systemctl restart fail2ban

sudo fail2ban-client status sshd

```

  

---

  

## 🔥 Iptables et UFW

  

**iptables :**

```bash

sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

sudo iptables -A INPUT -j DROP

sudo iptables-save > /etc/iptables/rules.v4

```

  

**ufw :**

```bash

sudo ufw enable

sudo ufw allow 22

sudo ufw allow 443

sudo ufw status

```