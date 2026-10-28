### 🐳 **Docker**

> **C’est quoi ?**  
> Docker est un outil qui permet de **créer, déployer et exécuter des applications dans des conteneurs**.  
> Un conteneur = une mini-machine avec tout ce qu’il faut pour faire tourner ton app (code + dépendances + système).

> **À quoi ça sert ?**  
> ✅ Tu évites les problèmes du type "ça marche sur mon PC mais pas ailleurs"  
> ✅ Tu rends ton app portable et facile à déployer n’importe où

### 📦 **Dockerfile**

> **C’est quoi ?**  
> Un **Dockerfile** est un fichier texte avec des instructions pour construire une image Docker.

> **Exemple simple :**
```
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["node", "index.js"]

```

**À quoi ça sert ?**  
C’est la **recette** pour créer ton conteneur : quel système, quels fichiers copier, quelles commandes exécuter, etc.

### 🧩 **Docker Compose**

> **C’est quoi ?**  
> Un outil pour **orchestrer plusieurs conteneurs** en même temps, avec une simple commande.

> **Exemple :**  
> Tu as une app Node.js + une base de données PostgreSQL → tu peux les lancer ensemble, en un seul coup.

### 🆚 **`docker-compose` (avec tiret)**

- 👉 C’est **l’ancienne commande**, issue d’un **outil séparé** de Docker.
    
- 📦 Il fallait **l’installer à part** (`docker-compose` CLI).
    
- 📁 Utilise toujours le fichier `docker-compose.yml`.
    
- 🛠 Encore utilisé dans certains environnements (ou versions plus anciennes de Docker).
    

---

### ✅ **`docker compose` (avec espace)**

- 👉 C’est la **nouvelle version intégrée** dans Docker depuis Docker v20.10 (fin 2020).
    
- ✔️ **Inclus directement** dans `docker` (pas besoin d’install separate).
    
- 💡 Plus moderne, mieux intégré, et en développement actif.
    
- 📁 Utilise exactement le même fichier `docker-compose.yml`.
---

### 📄 **docker-compose.yml**

> **C’est quoi ?**  
> Un fichier YAML (lisible à l’œil) qui décrit **comment lancer et configurer plusieurs conteneurs**.

> **Exemple simple :**

```yml
version: '3'
services:
  web:
    build: .
    ports:
      - "3000:3000"
  db:
    image: postgres
    environment:
      POSTGRES_PASSWORD: example

```

> **À quoi ça sert ?**  
> Il te suffit de faire `docker-compose up` et tout se lance comme décrit dans ce fichier.

