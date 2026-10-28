# nmap

nmap 10.0.0.4 
nmap -sV 10.0.0.4
nmap -sS -p1-65535 -T4 target.com 
nmap -sV -sC -p22,80,443 -oA scan_service target.com 
nmap -O --osscan-guess -Pn target.com 
nmap -sU -pU:1-2000 target.com 
nmap --script vuln -p80,443 target.com

# gobuster

`gobuster dir -u https://target.com -w /path/wordlists/common.txt -t 50 -x php,html,txt -o 
gobuster.txt gobuster vhost -u https://target.com -w /path/wordlists/vhosts.txt -t 30 -o vhosts.txt 
gobuster dns -d target.com -w /path/wordlists/dns.txt -o dns.txt`

# ffuf

`ffuf -u https://target.com/FUZZ -w /path/wordlists/common.txt -t 50 -e .php,.html -mc 200,301 -o ffuf.json 
ffuf -u https://FUZZ.target.com -w /path/wordlists/vhosts.txt -t 40 -o vhost_ffuf.json 
ffuf -w payloads.txt -u https://target.com/search?q=FUZZ -H "User-Agent: FUZZ" -fs 0`

# sqlmap

`sqlmap -u "http://target.com/page.php?id=1" --batch --level=3 --risk=2 --dbs sqlmap -u "http://target.com/page.php?id=1" -p id --batch -D database_name --tables 
sqlmap -u "http://target.com/page.php?id=1" -p id --batch -D db -T table --columns 
sqlmap -u "http://target.com/page.php?id=1" -p id --dump --batch
sqlmap -u "http://target.com/page.php?id=1" --os-shell 
sqlmap -u "http://target.com/page.php?id=1" --batch --tamper=space2comment`

# ssh2john

ssh2john.py id_rsa > id_rsa.hash # si outil dans PATH ssh2john.py id_rsa > id_rsa.hash`

# johntheripper

`john --wordlist=/path/wordlists/rockyou.txt id_rsa.hash 
john --format=sha512crypt --wordlist=/path/wordlists/rockyou.txt hashes.txt 
john --rules --wordlist=/path/wordlists/wordlist.txt hashes.txt 
john --show hashes.txt john --incremental hashes.txt`

## **kerbrute**

Objectif : tests d’authentification Kerberos (enum, bruteforce).  
Modes :

- `userenum` : vérifier l’existence de comptes.
    
- `passwordspray` : tester un mot de passe sur plusieurs comptes.
    
- `bruteforce` : tester plusieurs mots de passe sur un ou plusieurs comptes.  
    Types d’arguments :
    
- Domaine : `-d`.
    
- Fichier de comptes ou mots de passe.
    
- Debug/log : `-v`, `--log`.
    
- Threads : accélération contrôlée.
    

---

## **Impacket**

Suite de scripts interactifs pour divers protocoles.  
Catégories :

- SMB (auth, file service).
    
- Kerberos (tickets, requêtes).
    
- RPC et DCE-RPC.
    
- RDP, LDAP, MSSQL, etc.  
    Chaque script du type `impacket-xxx` possède généralement :
    
- Paramètres d’authentification (user, pass, hash, clé, domaine).
    
- Paramètres réseau (hôte, port).
    
- Options spécifiques au protocole (chaîne de connexion, requêtes).

## **Metasploit (msfconsole)**

Objectif : cadre modulaire d’exploitation contrôlée.  
Concepts/éléments :

- `search <mot>` : rechercher modules ou payloads.
    
- `use <module>` : sélectionner un module.
    
- `show options` : afficher les paramètres du module.
    
- `set <option> <valeur>` : configurer un paramètre.
    
- Types de modules : exploit, auxiliary, payload, post, encoder, evasion.
    
- Ressources : fichiers `.rc` pour automatiser une séquence d’actions (sans fournir de séquence opérationnelle).

## **arp-scan**

Objectif : découverte d’hôtes en réseau local via ARP.  
Options courantes (description uniquement) :

- `--interface` : spécifier l’interface réseau à utiliser.
    
- `--localnet` : scanner automatiquement le réseau local.
    
- `--retry` : nombre de tentatives d’envoi par hôte.
    
- `--ignoredups` : ignorer les réponses multiples.
    
- `--plain` : sortie simplifiée.


## Google Dork – Cheat-Sheet (OSINT / Recherche avancée)

### 🔹 Opérateurs de base

`"mot exact"          → recherche exacte OR                   → alternative -                    → exclure un terme *                    → joker`

### 🔹 Ciblage de sites & domaines

`site:example.com     → recherche dans un site précis site:.gov            → domaine spécifique`

### 🔹 Fichiers

`filetype:pdf ext:sql`

Exemples :

`filetype:xls "password" ext:env DB_PASSWORD`

### 🔹 URL & structure

`inurl:admin allinurl:login admin`

### 🔹 Contenu de pages

`intitle:"index of" allintitle:login password intext:"confidential"`

### 🔹 Infos sensibles (à usage légal uniquement)

`intitle:"index of" "backup" filetype:sql "INSERT INTO" ext:log password`

### 🔹 OSINT / dev / sécurité

`site:github.com "API_KEY" site:pastebin.com password "Authorization: Bearer"`

---

## ASM x86 – Cheat-Sheet (Bases)

### 🔹 Registres principaux (32 bits)

`EAX → accumulateur EBX → base ECX → compteur EDX → données ESI → source EDI → destination EBP → base stack ESP → sommet stack EIP → instruction courante`

_(En 64 bits : RAX, RBX, RCX, etc.)_

---

### 🔹 Syntaxe AT&T vs Intel

**Intel (le plus courant)**

`mov eax, ebx`

**AT&T**

`movl %ebx, %eax`

---

### 🔹 Instructions de base

`mov dest, src    → copie add dest, src    → addition sub dest, src    → soustraction mul / imul       → multiplication div / idiv       → division inc / dec        → +1 / -1`

---

### 🔹 Comparaison & sauts

`cmp a, b         → compare test a, b        → AND logique (flags)  je   → égal jne  → différent jg   → > jl   → < jge  → >= jle  → <= jmp  → saut inconditionnel`

---

### 🔹 Stack

`push eax pop eax`

Convention classique :

`ESP ↓ (stack grandit vers le bas)`

---

### 🔹 Appels de fonctions

`call func ret`

Prologue typique :

`push ebp mov ebp, esp`

Épilogue :

`mov esp, ebp pop ebp ret`

---

### 🔹 Accès mémoire

`mov eax, [ebx]        → valeur pointée mov eax, [ebx+4] mov eax, [ebx+ecx*4]`

---

### 🔹 Flags importants

`ZF → Zero Flag CF → Carry Flag SF → Sign Flag OF → Overflow Flag`

---

### 🔹 Syscall (Linux x86 32 bits)

`mov eax, 1    ; sys_exit mov ebx, 0 int 0x80`