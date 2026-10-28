The generated password for the elastic built-in superuser is : vyHOGHrrNaPqFj0LEffX

If this node should join an existing cluster, you can reconfigure this with
'/usr/share/elasticsearch/bin/elasticsearch-reconfigure-node --enrollment-token <token-here>'
after creating an enrollment token on your existing cluster.

You can complete the following actions at any time:

Reset the password of the elastic built-in superuser with 
'/usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic'.

Generate an enrollment token for Kibana instances with 
 '/usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana'.

Generate an enrollment token for Elasticsearch nodes with 
'/usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s node'.

https://devopssec.fr/article/installation-configuration-elk#begin-article-section

# trucs
Installer la denriere version, site officiel > apt repo

# RAM
/etc/elasticsearch/jvm.options.d/jvm.options (creer)

```
-Xms8g
-Xmx8g
```

# cert kibana/ES
dans elasticsearch.yml recuperer le path du crt et le donner à kibana dans kibana.yml
/etc/elasticsearch/certs/http_ca.crt

ou 

xpack.security.enabled: false dans la conf ES

# filebeat
toujours activer le module system

# filebeat
Bien installer rsyslog ! sinon logs vides

Sortie vers logstash:  
filebeat setup --dashboards

penser à activer la conf logstash