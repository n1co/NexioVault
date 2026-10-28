# Install

Définir un hostname, si pas de DNS, le définir dans le host:

```shell
echo "10.0.0.118 elk.truc.local" > /etc/hosts
```

Installer les dépendences et la clé du dépot:

```shell
apt install sudo gnupg2 apt-transport-https curl vim -y  
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | \  
gpg --dearmor > /etc/apt/trusted.gpg.d/elk.gpg
```

Ajout du dépot ELK8:

```shell
echo "deb https://artifacts.elastic.co/packages/8.x/apt stable main" \  
> /etc/apt/sources.list.d/elastic-8.list
```

Puis mise à jour des dépots:

```shell
apt update
```


L'ordre d'installation est important:

1. Elasticsearch
2. Kibana
3. Logstash
4. Beats

## Elastic

On commence par l'installation d'elasticsearch:

```shell
apt install elasticsearch -y
```

>Attention, lors de l'installation, un mot de passe pour le user "elastic" sera généré, notez le bien !


Il est possible de modifier la RAM utilisée par Elastic via les parametres Java:
En general, nous lui donnons maximum la moitié de la RAM de la vm/Machine

 ```shell
 echo -e '-Xms512m\n-Xmx512m' > /etc/elasticsearch/jvm.options.d/jvm-heap.options
 ```

Nous allons maintenant activer au boot le service Elastic:

```shell
systemctl daemon-reload  
systemctl enable --now elasticsearch
```

Il est possible de vérifier de plusieurs manière le bon fonctionnement du service:

En vérifiant le status du service: 
```shell
systemctl status elasticsearch
```

Mais attention, le service qui tourne ne signifie pas que le service est bien fonctionnel, vous pouvez le vérifier avec une commande curl:

```shell
curl https://localhost:9200 --cacert /etc/elasticsearch/certs/http_ca.crt -u elastic
```

Cette commande va curl le serveur elastic, avec le certificat généré, et avec l'utilisateur Elastic (le mot de passe à été généré lors de l'installation d'elastic)

Il est également possible de vérifier que le port est bien en écoute:

```shell
ss -altnp | grep 9200
```

## Kibana

Ensuite nous passons a l'installation de Kibana:

```shell
apt install kibana -y
```

Par défaut, kibana n'écoute que sur localhost, nous pouvons éditer sa config pour qu'il puisse écouter depuis d'autres IP/Réseaux:

```shell
vim /etc/kibana/kibana.yml
```

```
#server.host: "localhost"  
server.host: "10.0.0.90"
```

Kibana fonctionne sur un système de token pour ses communications internes, nous allons donc en générer un:

```shell
/usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana
```

Il nous faudra également les clés utilisées par Kibana:

- `xpack.encryptedSavedObjects.encryptionKey`: Utilisé pour le chiffrement des données du dashboard
- `xpack.reporting.encryptionKey`: Pour le chiffrement des données de reporting
- `xpack.security.encryptionKey:` Et pour le chiffrement des sessions

Nous allons donc générer ces clés de la manière suivante:

```shell
/usr/share/kibana/bin/kibana-encryption-keys generate
```

Ces cles seront ensuite mises a la fin de la config de kibana (/etc/kibana/kibana.yml)

Nous devrions maintenant etre en mesure d'acceder a l'interface web de gestion de Kibana, lors du premier acces a kibana, celui-ci nous demandera le enrollment token que nous avons cree plus tot.

>Pour rappel, ce token contient plusieurs elements, comme, ou trouver elastic (via son IP), les identifiants API pour parler avec Elastic, et enfin un fingerprint pour verifier l'identite du serveur elastic (pour eviter les attaques MITM nottament)

### Notes

Retrouver la signature d'un certificat:

```shell
openssl x509 -fingerprint -sha256 -in /etc/elasticsearch/certs/http_ca.cert
```

fingerprint filebeat:

```shell
ssl.ca_trusted_fingerprint: "xxxxxx"
```

+  + user & password