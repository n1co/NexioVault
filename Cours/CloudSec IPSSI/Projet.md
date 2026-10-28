# Projet  – Architecture Cloud Sécurisée AWS pour **Black Mesa**

## Objectif du projet

Vous êtes missionnés comme **architectes sécurité cloud AWS** pour l’entreprise fictive **Black Mesa**, en pleine migration vers une infrastructure hybride (on-premise + cloud). Ce projet vise à :

- Concevoir une **infrastructure AWS sécurisée, modulaire, automatisée et conforme aux standards internationaux**
- Déployer cette infrastructure avec **Terraform**
- Documenter l’ensemble selon un **niveau professionnel** en intégrant les **standards de sécurité du Cloud** (NIST, CSA, ENISA)

---

## Contexte client

Black Mesa dispose d’une infrastructure locale vieillissante. Elle souhaite évoluer vers une **architecture hybride** en hébergeant ses **services critiques dans AWS**. Ses objectifs sont :

- Sécurité maximale (Zero Trust, DLP, IAM)
- Haute disponibilité pour certains services publics (ex. site vitrine)
- Microservices pour les applications internes (ex. Wordpress)
- Accès restreint et traçable pour les utilisateurs internes
- Connexions inter-sites (local ↔ AWS) via VPN
- Déploiement automatisé avec Terraform

---

## Contraintes et exigences techniques

### Sécurité – Normes et exigences à respecter :

🔹 **Modèle Zero Trust** : aucun accès n’est accordé par défaut  
🔹 **IAM & RBAC** : gestion fine des rôles et privilèges  
🔹 **Filtrage stateful + DPI** : NGFW (Next-Gen Firewall) recommandé  
🔹 **Chiffrement SSL/TLS** des flux et des stockages (EBS, S3)  
🔹 **MFA obligatoire** pour tous les accès privilégiés  
🔹 **Détection d’intrusion** (IDS/IPS, SIEM)  
🔹 **Journalisation complète** des accès et événements  
🔹 **Conformité DLP** : classification des données sensibles


### Composants techniques à implémenter dans AWS

| Composant                     | Spécifications                                      |
| ----------------------------- | --------------------------------------------------- |
| **VPC & Subnets**             | Multi-AZ, segmentation par zone de sécurité         |
| **Bastion Host**              | Pour accès admin SSH, loggué, MFA, en subnet public |
| **VPN site-to-site**          | Pour relier le site local à AWS                     |
| **Reverse proxy**             | Nginx/HAProxy en HA, SSL, pour Wordpress            |
| **Wordpress microservices**   | Conteneurisé (ECS ou EC2), relié à une DB RDS       |
| **Base de données sécurisée** | Chiffrement, audit activé, subnet privé             |
| **Monitoring**                |  alertes, Grafana                                   |
| **Anti-DDoS**                 | AWS Shield, WAF, throttling sur ALB                 |
| **Terraform**                 | Infrastructure codée, modulaire, réutilisable       |

### Mise en œuvre de sécurité à appliquer

|Couches de sécurité| Exemples concrets à mettre en œuvre                 |
|---|---|
|**Technologique**| TLS, MFA, logging, IPS/IDS, SGs                     |
|**Organisationnelle**| PSSI fictive, rôles étudiants simulés               |
|**Contractuelle**| Exigences RGPD, chiffrement, SLA simulés            |
|**Architecturale**| Isolation des environnements, bastions, VPC peering |

## Livrables obligatoires

### 1. Dossier de conception d’architecture

- Diagrammes réseaux (VPC, subnets, routes, VPN)
- Diagramme des flux réels
- Architecture logique des services (Wordpress, DB, Proxy)
- Politique d’accès IAM (RBAC, groupes)
- Politique de journalisation, surveillance, audit
- Détail des mécanismes Zero Trust et filtrage

### 2. Code Terraform

- Infrastructure AWS modulaire
- Séparation par environnements (ex : `prod`, `test`)
- README d’utilisation

### 3. Matrice de risque (format tableau)

- Identification des actifs critiques
- Analyse des menaces (ex : DDoS, IAM leak)
- Probabilité / Impact / Traitement
- Rédigée selon modèle ENISA

### 4. Rapport final professionnel

- Synthèse de la démarche, choix technos et sécurité
- Captures / démonstrations / logs de tests
- Auto-évaluation par les étudiants
- Annexes techniques : commandes, terraform plan, IAM policies

## Bonus (points supplémentaires)

- CI/CD pour Wordpress (GitHub Actions, CodePipeline)
- Mise en place d’un **SIEM open-source** (Wazuh, ELK)
- Architecture serverless ou Fargate
- Simulation d’incident de sécurité et réponse (rapport d'incident)