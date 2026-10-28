
## 📦 Images & Conteneurs

### 1. Lister les images disponibles
```bash
docker images
```
> Affiche les images Docker téléchargées localement.

---

### 2. Télécharger une image
```bash
docker pull <nom_image>
```
> Télécharge une image depuis Docker Hub.  
> Exemple : `docker pull nginx`

---

### 3. Créer & démarrer un conteneur
```bash
docker run <options> <image>
```
> Lance un conteneur basé sur une image.

Exemple basique :
```bash
docker run -it ubuntu
```
- `-i` : mode interactif  
- `-t` : attache un terminal

Exemple avec port :
```bash
docker run -d -p 8080:80 nginx
```
- `-d` : mode détaché (en arrière-plan)  
- `-p` : mappe le port 80 du conteneur sur le port 8080 local

---

### 4. Lister les conteneurs
```bash
docker ps
```
> Liste les conteneurs en cours d'exécution.

```bash
docker ps -a
```
> Liste **tous** les conteneurs (même arrêtés).

---

### 5. Arrêter un conteneur
```bash
docker stop <id|nom>
```
> Arrête un conteneur en cours.

---

### 6. Supprimer un conteneur
```bash
docker rm <id|nom>
```
> Supprime un conteneur (doit être arrêté avant).

---

### 7. Supprimer une image
```bash
docker rmi <nom_image>
```
> Supprime une image Docker.

---

### 8. Exécuter une commande dans un conteneur en cours
```bash
docker exec -it <id|nom> <commande>
```
> Par exemple :
```bash
docker exec -it mon_conteneur bash
```
> Pour ouvrir un terminal dans le conteneur.

---

## 🔧 Autres commandes utiles

### 9. Construire une image Docker
```bash
docker build -t mon_image .
```
> Crée une image Docker à partir d’un `Dockerfile` dans le répertoire courant.

---

### 10. Afficher les logs d’un conteneur
```bash
docker logs <id|nom>
```
> Très utile pour le debug.

---

### 11. Nettoyer les ressources inutilisées
```bash
docker system prune
```
> Supprime les conteneurs arrêtés, les images non utilisées, etc. (⚠️ attention, ça peut supprimer beaucoup de choses).

---

### 12. Copier un fichier entre host et conteneur
```bash
docker cp fichier.txt mon_conteneur:/chemin/
```

---

## 🧠 Bonus : Infos détaillées sur un conteneur
```bash
docker inspect <id|nom>
```
> Montre toutes les infos détaillées (IP, volumes, config…).
