# **1. Sujet du TP**

Vous devez créer un script nommé **`backup.sh`** ayant les caractéristiques suivantes :

## 1.1 Fonctionnalités obligatoires

1. **Sauvegarde d’un dossier source** vers un **répertoire de destination**.
2. La sauvegarde devra produire une **archive compressée** (format `.tar.gz`).
3. Le script doit **lire un fichier de configuration externe** :  
    Exemple : `backup.conf`  
    Avec les paramètres :
    `SOURCE_DIR=/chemin/a/sauvegarder BACKUP_DIR=/chemin/de/sauvegarde LOG_FILE=/chemin/log/backup.log RETENTION_DAYS=7`
    
4. Le script doit :
    - vérifier les chemins
    - afficher des erreurs claires
    - écrire un **journal d’exécution** (date, résultat, taille du backup)
    - supprimer les sauvegardes plus anciennes que **RETENTION_DAYS**

5. L’archive doit avoir un nom comportant :
    - la date
    - le hostname
    
    Exemple : `backup-hostname-2025-12-06.tar.gz`

## 1.2 Fonctionnalités bonus

- gestion des codes de retour
- coloration terminal (OK/ERROR)
- envoi optionnel d’un mail après backup réussi (via mailx)

## 1.3 Crontab

Vous devez également fournir :

- une ligne de crontab permettant d’exécuter votre script **tous les jours à 2h00 du matin**.

# **2. Correction proposée**

## **2.1 Exemple de fichier de configuration : `backup.conf`**

```conf
# Dossier à sauvegarder
SOURCE_DIR="/home/user/data"

# Destination des sauvegardes
BACKUP_DIR="/var/backups"

# Fichier de log
LOG_FILE="/var/log/backup.log"

# Suppression des backups de plus de X jours
RETENTION_DAYS=7

```

## 2.2 Script complet `backup.sh` (correction)

```bash
#!/bin/bash

# Chargement de la configuration
CONFIG_FILE="./backup.conf"

if [ ! -f "$CONFIG_FILE" ]; then
    echo "[ERROR] Fichier de configuration introuvable : $CONFIG_FILE"
    exit 1
fi

source "$CONFIG_FILE"

DATE=$(date +"%Y-%m-%d_%H-%M-%S")
HOST=$(hostname)

ARCHIVE_NAME="backup-${HOST}-${DATE}.tar.gz"
ARCHIVE_PATH="${BACKUP_DIR}/${ARCHIVE_NAME}"

# Vérification des répertoires
if [ ! -d "$SOURCE_DIR" ]; then
    echo "[ERROR] Répertoire source introuvable : $SOURCE_DIR"
    exit 2
fi

if [ ! -d "$BACKUP_DIR" ]; then
    echo "[INFO] Création du répertoire de backup : $BACKUP_DIR"
    mkdir -p "$BACKUP_DIR"
fi

# Lancement du backup
echo "$(date '+%Y-%m-%d %H:%M:%S') - Début du backup..." >> "$LOG_FILE"

tar -czf "$ARCHIVE_PATH" "$SOURCE_DIR" 2>>"$LOG_FILE"

if [ $? -ne 0 ]; then
    echo "$(date '+%Y-%m-%d %H:%M:%S') - [ERROR] Échec de la création de l'archive." >> "$LOG_FILE"
    exit 3
fi

SIZE=$(du -h "$ARCHIVE_PATH" | cut -f1)
echo "$(date '+%Y-%m-%d %H:%M:%S') - Archive créée : $ARCHIVE_NAME ($SIZE)" >> "$LOG_FILE"

# Gestion de la rétention
find "$BACKUP_DIR" -type f -name "backup-*.tar.gz" -mtime +"$RETENTION_DAYS" -exec rm {} \; \
    && echo "$(date '+%Y-%m-%d %H:%M:%S') - Fichiers anciens supprimés (+${RETENTION_DAYS} jours)" >> "$LOG_FILE"

echo "$(date '+%Y-%m-%d %H:%M:%S') - Backup terminé avec succès." >> "$LOG_FILE"

exit 0

```

## Exemple de ligne crontab
### Pour exécuter le script tous les jours à **02h00** :

```
0 2 * * * /chemin/vers/backup.sh
```

### Pour éditer votre crontab :
```
crontab -e
```

