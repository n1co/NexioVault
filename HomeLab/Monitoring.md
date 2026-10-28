# Runbook — Stack de monitoring homelab

Prometheus + Grafana en installation native dans un conteneur LXC Debian 12.
Pas de Docker.

---

## 1. Architecture

```
Machines surveillées                 CT de monitoring
─────────────────────                ────────────────
node_exporter    :9100  ──scrape──►  Prometheus  :9090
apache_exporter  :9117  ──scrape──►       │
                                          ▼
                                     Grafana     :3000
```

Prometheus **va chercher** les métriques (pull). Les exporters n'ont besoin de
connaître personne : ils exposent une page HTTP, c'est Prometheus qui détient la
liste des cibles.

| Composant | Port | Emplacement |
|---|---|---|
| node_exporter | 9100 | chaque machine surveillée |
| apache_exporter | 9117 | machines faisant tourner Apache |
| Prometheus | 9090 | CT de monitoring |
| Grafana | 3000 | CT de monitoring |

### Inventaire

| Rôle | Hôte | IP |
|---|---|---|
| Monitoring | `monitoring` | `192.168.0.___` |
| Reverse proxy | `reverse-proxy` | `192.168.0.202` |

> Compléter au fur et à mesure.

---

## 2. Installation initiale du CT de monitoring

Prérequis : LXC Debian 12, 2 Go de RAM, 8 Go de disque minimum.
Prometheus consomme surtout du disque, Grafana surtout de la RAM.

### 2.1 Préparation

```bash
apt update && apt upgrade -y
apt install -y curl gnupg apt-transport-https
```

### 2.2 Prometheus

```bash
apt install -y prometheus
systemctl status prometheus
curl -s localhost:9090/-/healthy
```

Debian 12 fige Prometheus en 2.42. Suffisant pour un homelab.

### 2.3 Rétention

Par défaut 15 jours. Dans `/etc/default/prometheus` :

```bash
ARGS="--storage.tsdb.retention.time=30d"
```

```bash
systemctl restart prometheus
```

Les données vivent dans `/var/lib/prometheus/metrics2/`.

### 2.4 node_exporter local

Le CT de monitoring doit se surveiller lui-même.

```bash
apt install -y prometheus-node-exporter
systemctl enable --now prometheus-node-exporter
curl -s localhost:9100/metrics | head -5
```

### 2.5 Grafana

Grafana n'est pas dans les dépôts Debian.

```bash
mkdir -p /etc/apt/keyrings
curl -fsSL https://apt.grafana.com/gpg.key | gpg --dearmor -o /etc/apt/keyrings/grafana.gpg
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" \
  > /etc/apt/sources.list.d/grafana.list
apt update
apt install -y grafana
systemctl daemon-reload
systemctl enable --now grafana-server
```

Le paquet `grafana` est la version OSS. Ne pas prendre `grafana-enterprise`,
qui contient des composants sous licence non libre.

### 2.6 Datasource Prometheus

Provisionner plutôt que cliquer dans l'UI.
Fichier `/etc/grafana/provisioning/datasources/prometheus.yml` :

```yaml
apiVersion: 1
datasources:
  - name: Prometheus
    type: prometheus
    access: proxy
    url: http://localhost:9090
    isDefault: true
```

```bash
chown root:grafana /etc/grafana/provisioning/datasources/prometheus.yml
chmod 640 /etc/grafana/provisioning/datasources/prometheus.yml
systemctl restart grafana-server
```

### 2.7 Premier accès

`http://<ip-du-CT>:3000` — login `admin` / `admin`, changement imposé au premier
accès.

Fermer l'inscription libre dans `/etc/grafana/grafana.ini` :

```ini
[users]
allow_sign_up = false
```

```bash
systemctl restart grafana-server
```

---

## 3. Ajouter une machine à surveiller

**C'est l'opération récurrente.** Trois étapes, deux minutes.

### 3.1 Sur la machine à surveiller

```bash
apt install -y prometheus-node-exporter
systemctl enable --now prometheus-node-exporter
```

Vérifier localement :

```bash
curl -s localhost:9100/metrics | head -3
```

### 3.2 Vérifier l'accès depuis le CT de monitoring

```bash
curl -s http://192.168.0.XXX:9100/metrics | head -3
```

Si ça échoue ici, c'est le réseau ou un pare-feu — inutile de continuer.

### 3.3 Déclarer la cible

Dans `/etc/prometheus/prometheus.yml`, ajouter la ligne au job `node` :

```yaml
scrape_configs:
  - job_name: prometheus
    static_configs:
      - targets: ['localhost:9090']

  - job_name: node
    static_configs:
      - targets:
          - 'localhost:9100'
          - '192.168.0.202:9100'
          - '192.168.0.XXX:9100'      # ← nouvelle machine
```

### 3.4 Recharger

Pas besoin de redémarrer, un SIGHUP suffit :

```bash
systemctl reload prometheus
```

### 3.5 Contrôler

`http://<ip-du-CT>:9090/targets` — la nouvelle cible doit être en **UP**.

Les dashboards existants (comme Node Exporter Full) verront la machine
automatiquement via leur variable `instance`.

---

## 4. Surveiller un Apache

Deux niveaux possibles. Le second est celui utilisé par le dashboard
« Apache — Reverse proxy ».

### 4.1 Niveau minimal : le service tourne-t-il ?

Activer le collector systemd de node_exporter. Dans
`/etc/default/prometheus-node-exporter` :

```bash
ARGS="--collector.systemd --collector.systemd.unit-include=(apache2|ssh|cron)\.service"
```

Le filtre `unit-include` est important : sans lui, l'état de **toutes** les units
remonte et le nombre de séries explose.

```bash
systemctl restart prometheus-node-exporter
```

Requête :

```promql
node_systemd_unit_state{name="apache2.service", state="active"}
```

Renvoie `1` si actif, `0` sinon.

### 4.2 Niveau complet : métriques Apache

#### Côté Apache

Activer le module :

```bash
a2enmod status
```

Configuration — **une seule** déclaration, au niveau global :

```apache
<Location "/server-status">
    SetHandler server-status
    Require local
</Location>

ExtendedStatus On
```

Deux points critiques :

- **`Require local`, pas `Require ip 127.0.0.1`.** L'exporter est un client Go
  qui résout `localhost` en préférant souvent `::1`. Avec une règle IPv4 seule,
  la requête prend un 403. Voir §7.2.
- **`ExtendedStatus On` au niveau global**, jamais à l'intérieur du `<Location>`.
  Sans lui : pas de `Total Accesses`, donc pas de trafic, pas de latence, pas de
  débit dans le dashboard.

Si Apache est un **reverse proxy** avec un `ProxyPass` fourre-tout, il faut
exclure `/server-status` **avant** le ProxyPass, sinon la requête part vers le
backend :

```apache
ProxyPass /server-status !

<Location "/server-status">
    SetHandler server-status
    Require local
</Location>

ProxyPass        / http://backend:8080/
ProxyPassReverse / http://backend:8080/
```

Appliquer :

```bash
apachectl configtest && systemctl reload apache2
```

#### Vérifier la sortie

```bash
curl -sS "http://localhost/server-status/?auto" | head -20
```

Sortie attendue :

```
localhost
ServerVersion: Apache/2.4.68 (Debian)
ServerMPM: event
...
Total Accesses: 98
Total kBytes: 176
Total Duration: 147
```

> La première ligne contenant le nom du serveur est **normale** en mode `?auto`.
> Ce n'est pas une anomalie, l'exporter sait la traiter.

Ce qui compte : la présence de `Total Accesses`, `Total kBytes` et
`Total Duration`. Sans eux, `ExtendedStatus` n'est pas actif.

#### Installer l'exporter

```bash
apt install -y prometheus-apache-exporter
systemctl enable --now prometheus-apache-exporter
```

Il écoute sur le **9117**. URL scrappée par défaut :
`http://localhost/server-status/?auto`. Pour la changer, éditer
`/etc/default/prometheus-apache-exporter` :

```bash
ARGS="--scrape_uri=http://localhost/server-status?auto"
```

#### Déclarer la cible

```yaml
  - job_name: apache
    static_configs:
      - targets: ['192.168.0.202:9117']
```

```bash
systemctl reload prometheus
```

#### Valider

```bash
curl -s localhost:9117/metrics | grep -c '^apache_'
```

Attendu : **une trentaine**. Si le compte est à **2** (`apache_up` et
`apache_exporter_build_info`), le parsing échoue — voir §7.2.

---

## 5. Dashboards

### 5.1 Dashboards publics

Grafana → Dashboards → New → Import → saisir l'ID :

| ID | Dashboard |
|---|---|
| 1860 | Node Exporter Full |
| 3662 | Prometheus 2.0 Overview |
| 3894 | Apache exporter |

### 5.2 Dashboard personnalisé

Depuis Grafana 13, l'onglet **JSON Model** des paramètres valide contre le schéma
V2 (`elements`, `layout`, `timeSettings`, `cursorSync`). Y coller un JSON au
format Classic produit des erreurs de propriétés manquantes.

**Utiliser la page Import**, pas l'onglet JSON Model :
Dashboards → New → **Import** → Upload JSON file.

Alternative en ligne de commande, via l'API historique qui accepte toujours le
Classic :

```bash
curl -u admin:MOT_DE_PASSE \
  -H "Content-Type: application/json" \
  -X POST http://localhost:3000/api/dashboards/db \
  -d @apache-dashboard-api-payload.json
```

### 5.3 Provisioning par fichier

Recommandé sur le long terme : versionnable dans Git, revient automatiquement
après réinstallation.

```bash
mkdir -p /var/lib/grafana/dashboards
cp mon-dashboard.json /var/lib/grafana/dashboards/
chown -R grafana:grafana /var/lib/grafana/dashboards
```

`/etc/grafana/provisioning/dashboards/local.yml` :

```yaml
apiVersion: 1
providers:
  - name: local
    type: file
    disableDeletion: false
    updateIntervalSeconds: 30
    options:
      path: /var/lib/grafana/dashboards
      foldersFromFilesStructure: false
```

> Depuis Grafana 13, l'export « Classic » a disparu de l'UI et le JSON exporté
> n'est plus directement réutilisable pour le provisioning (bug ouvert côté
> Grafana). Conséquence pratique : **éditer les fichiers directement**, ne pas
> faire d'aller-retour par l'interface.

---

## 6. Requêtes utiles

### Système

```promql
# CPU utilisé (%)
100 - (avg by (instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)

# RAM utilisée (%)
100 * (1 - node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes)

# Disque / restant (%)
100 * node_filesystem_avail_bytes{mountpoint="/"} / node_filesystem_size_bytes{mountpoint="/"}

# Machine injoignable
up == 0
```

### Apache

```promql
# mod_status répond
apache_up

# Requêtes par seconde
rate(apache_accesses_total[5m])

# Saturation workers (%) — dénominateur = MaxRequestWorkers
100 * apache_workers{state="busy"} / sum by (instance) (apache_scoreboard)

# Latence moyenne (ms) — reflète le backend sur un reverse proxy
rate(apache_duration_ms_total[5m]) / rate(apache_accesses_total[5m])

# Débit sortant (octets/s)
rate(apache_sent_kilobytes_total[5m]) * 1024
```

**Sur la saturation :** utiliser `sum(apache_scoreboard)` comme dénominateur,
pas `busy + idle`. Apache spawne ses processus à la demande, donc
`busy/(busy+idle)` affiche régulièrement 100 % alors qu'il reste des centaines
de slots libres. Le scoreboard total correspond à `MaxRequestWorkers`, c'est le
vrai plafond.

### Alertes prioritaires

```promql
up == 0                                                        # cible injoignable
100 * apache_workers{state="busy"} / sum by (instance) (apache_scoreboard) > 85
apache_up == 0                                                 # Apache à terre
100 * node_filesystem_avail_bytes{mountpoint="/"} / node_filesystem_size_bytes{mountpoint="/"} < 10
```

> `up` et `apache_up` sont complémentaires : `up` dit que **l'exporter** répond,
> `apache_up` dit que l'exporter **joint Apache**.

---

## 7. Dépannage

### 7.1 Une cible est DOWN dans /targets

Dans l'ordre :

```bash
# 1. L'exporter tourne-t-il ?
systemctl status prometheus-node-exporter

# 2. Répond-il localement ?
curl -s localhost:9100/metrics | head -3

# 3. Répond-il depuis le CT de monitoring ?
curl -s http://192.168.0.XXX:9100/metrics | head -3

# 4. La cible est-elle bien déclarée ?
grep -A10 'job_name: node' /etc/prometheus/prometheus.yml
```

L'étape qui échoue désigne la couche fautive.

### 7.2 apache_up vaut 1 mais aucune métrique apache_*

**Le piège principal.** `apache_up 1` signifie « la requête HTTP a abouti », pas
« j'ai réussi à lire le statut ». Le passage à 1 se fait avant le parsing.

Le compteur qui tranche :

```bash
curl -s localhost:9117/metrics | grep scrape_failures
```

Si `apache_exporter_scrape_failures_total` augmente à chaque scrape, la réponse
reçue n'est pas parsable. Causes par ordre de fréquence :

1. **`Require ip 127.0.0.1` au lieu de `Require local`** — l'exporter arrive en
   `::1`, prend un 403, reçoit une page d'erreur HTML.
2. **ProxyPass fourre-tout** — `/server-status` part vers le backend, qui répond
   200 avec du HTML.
3. **URL scrappée incorrecte** — décalage sur le slash final entre
   `--scrape_uri` et le `<Location>`.

Diagnostic :

```bash
# Que reçoit réellement l'exporter ?
grep server-status /var/log/apache2/access.log | tail -10

# Journal de l'exporter
journalctl -u prometheus-apache-exporter -n 30 --no-pager

# Tester les deux piles IP séparément
curl -sS -4 "http://localhost/server-status/?auto" | head -2
curl -sS -6 "http://localhost/server-status/?auto" | head -2

# Quelle URL est scrappée ?
cat /etc/default/prometheus-apache-exporter
```

Un 403 ou une source `::1` dans l'access log confirme la cause n°1.

### 7.3 Panneaux vides après import

Vérifier dans l'ordre :

1. Les variables en haut du dashboard pointent sur les bonnes cibles.
   Attention : `instance` diffère entre node_exporter (`:9100`) et
   apache_exporter (`:9117`).
2. Les métriques existent : dans Explore, lancer `{instance="192.168.0.202:9117"}`
   pour lister toutes les séries de cette cible.
3. Les noms de métriques correspondent à la version de l'exporter installée.

### 7.4 Le disque se remplit

```bash
du -sh /var/lib/prometheus/metrics2/
```

Réduire la rétention dans `/etc/default/prometheus`, ou augmenter
`scrape_interval` dans le bloc `global` du `prometheus.yml`.

---

## 8. Spécificités LXC

**node_exporter ne voit qu'une partie du matériel.** lxcfs cloisonne correctement
CPU et RAM, mais les températures, l'état SMART et certains compteurs réseau
remontent des valeurs de l'hôte ou restent vides. Pour du vrai monitoring
matériel, installer `prometheus-node-exporter` **directement sur l'hôte
Proxmox**.

**Docker dans un LXC** nécessite `pct set <VMID> -features nesting=1,keyctl=1`
côté hôte. Sans objet ici puisqu'on est en natif — c'est justement l'intérêt.

**Exposition réseau.** Prometheus et Grafana écoutent sur toutes les interfaces.
Si le CT est exposé, restreindre `--web.listen-address` (dans `ARGS`) et
`http_addr` dans `grafana.ini`, ou mettre un reverse proxy devant.

---

## 9. Maintenance

| Fréquence | Action |
|---|---|
| Après chaque modif de `prometheus.yml` | `systemctl reload prometheus` |
| Après ajout de cible | Contrôler `/targets` |
| Mensuel | `du -sh /var/lib/prometheus/metrics2/` |
| Mensuel | `apt update && apt upgrade` |

### Fichiers à sauvegarder

```
/etc/prometheus/prometheus.yml
/etc/default/prometheus
/etc/grafana/grafana.ini
/etc/grafana/provisioning/
/var/lib/grafana/dashboards/
/var/lib/grafana/grafana.db        # dashboards créés dans l'UI
```

Les données de métriques (`/var/lib/prometheus/`) ne se sauvegardent
généralement pas : volumineuses et à faible valeur historique pour un homelab.

---

## 10. Pistes d'évolution

**Logs.** Loki (serveur, sur le CT de monitoring) + Grafana Alloy (agent, sur
chaque machine). Ni l'un ni l'autre n'est packagé dans Debian : le dépôt apt de
Grafana fournit `alloy`, mais Loki demande un binaire GitHub et une unit systemd
écrite à la main. Utile surtout à partir de 3-4 machines, ou pour obtenir les
codes HTTP et les percentiles de latence — que mod_status ne fournit pas.

Alternative bien plus légère si le besoin est juste « tout centraliser » :
rsyslog en mode serveur, présent dans Debian, cinq lignes de configuration de
chaque côté.

**Notifications.** L'alerting intégré de Grafana suffit pour un homelab
(inutile de déployer Alertmanager). Destinations auto-hébergées : ntfy ou
Gotify.

**Exporters supplémentaires.**

| Exporter | Usage |
|---|---|
| `blackbox_exporter` | ping HTTP/TCP/ICMP, expiration des certificats TLS |
| `smartctl_exporter` | santé des disques |
| `snmp_exporter` | switch, routeur, onduleur |
| `pve-exporter` | hôte Proxmox |
