## Techniques
de hacking  
et contre-  
mesures  
Niveau 1  
Lot: 3-058

---

## Public cible et   Destiné aux RSSI, ingénieurs sécurité, pentesteurs
|  débutants/intermédiaires et administrateurs  

prérequis  |  réseaux.  
|  Prérequis : notions réseaux, systèmes  
|  (Linux/Windows) et bases en sécurité informatique.

---

## Objectifs pédagogiques

- Comprendre les techniques des hackers pour mieux se défendre contre leurs attaques.  
- Mesurer et évaluer la sécurité du Système d'Information (SI).  
- Réaliser des tests de pénétration pour identifier les vulnérabilités des systèmes.  
- Définir l'impact et la portée d'une vulnérabilité dans le SI et déterminer les actions correctives  
nécessaires.

---

Qu’est-ce que le hacking éthique ?  

Activité visant à   Identification des  |  Rôle important  
tester la sécurité  |  failles pour  |  dans la protection  
d’un système avec  |  prévenir les  |  des entreprises et  
|  autorisation  |  cyberattaques  |  infrastructures

---

## Le rôle du hacker éthique

|  Effectuer une veille  
Réaliser des tests  |  Participer à  |  Produire des  
|  technologique sur  
|  d’intrusion  |  l’amélioration de la  |  rapports et  
|  les nouvelles  
|  (pentests)  |  cybersécurité  |  recommandations  
|  menaces

---

## Acteurs malveillants

Black hats : attaquants cherchant profit ou nuisance  

Motivations : vol d’argent, espionnage, sabotage, défi, vengeance  

Conséquences : pertes financières, fuite de données, interruption d’activité  

Il existe de nombreux profils d’acteur malveillants, comme par exemples les  
groups APT, les hacktivites…

---

## Types d’attaques les plus courantes

Phishing / ingénierie sociale  
DDoS (attaque par déni de service)  
Injection SQL  
Attaques par force brute  
Malwares (ransomware, spyware…)

---

## Attaque par phishing

|  Tromper  |  Emails  |  Redirections vers  |  Très efficace car  
l’utilisateur pour   frauduleux, SMS  |  pages  |  cible l’humain et  
|  obtenir ses  |  suspects, faux   d’authentification  |  non la  
|  informations  |  sites web  |  falsifiées  |  technologie

---

## Attaque DDoS

Envoi massif de requêtes vers un serveur pour le saturer  

Souvent réalisés via botnets (appareils infectés)  

Impact : sites web inaccessibles, perte de clients,  
surcharge des réseaux

---

## Outils utilisés par les acteurs

- Analyse réseau : Wireshark, tcpdump  
- Scan de ports : Nmap  
- Exploitation de failles : Metasploit  
- Crack de mots de passe : Hydra, John the Ripper, hashcat…  
- Reconnaissance : Shodan, theHarvester

---

## Comprendre les
vulnérabilités  
des systèmes

---

## Qu’est-ce  |  Une vulnérabilité est une faiblesse dans un
|  système informatique qui peut être exploitée par  
|  un attaquant pour altérer sa confidentialité, son  
qu’une  |  intégrité ou sa disponibilité.  
|  Elle peut provenir d’erreurs de programmation, de  

vulnérabilité ?   mauvaises configurations, ou d’un manque de  
|  contrôles de sécurité.

---

## Les failles courantes : Buffer Overflow

Le buffer overflow survient lorsqu’un  
programme écrit plus de données dans un  
|  tampon que l’espace prévu.  
|  En pratique :  
Cela permet à un attaquant d’écraser la  
mémoire du système et d’injecter du code  
|  malveillant.  
|  • Exploitation souvent liée à des langages  
|  “non sécurisés” (C/C++).  
|  • Permet l’exécution de code arbitraire.  
|  • Peut ouvrir une porte vers une prise de  
|  contrôle complète du système.

---

## Les failles courantes : XSS (Cross-Site
Scripting)  
Le XSS permet à un attaquant d’injecter  
du code JavaScript dans une page web  
consultée par d’autres utilisateurs.  |  Conséquences possibles :  
Cela ne vise pas directement le serveur,  
mais les navigateurs des victimes.  
|  • Vol de cookies et sessions.  
|  • Redirections vers des sites frauduleux.  
|  • Défiguration de pages web.

---

## Les failles  |  Le CSRF force un utilisateur authentifié à
|  exécuter malgré lui une action qu’il n’a pas  
courantes :  |  demandée.  
|  Il exploite la confiance d’un site envers la session  
CSRF (Cross-  |  de la victime.  

Site Request  
Forgery)  
|  Actions frauduleuses possibles :  

|  Publication de  
|  Changement de  
|  Transfert d’argent  |  contenu non  
|  mot de passe  
|  désiré

---

## Comment les  |  Les attaquants utilisent une méthodologie bien définie
|  pour transformer une faille en intrusion réelle :  

acteurs exploitent  |  1. Analyse et reconnaissance  
|  Identification des failles via scans, fuzzing, ou observation  
|  manuelle.  

ces vulnérabilités  |  2. Exploitation  
|  Utilisation de payloads pour provoquer l’anomalie  

?  |  (exécution de code, injection, redirection…).  
|  3. Escalade  
|  Recherche d’un accès plus profond ou de privilèges  
|  étendus.  
|  4. Maintien de l’accès  
|  Installation de portes dérobées, création de comptes,  
|  persistance.

---

## Méthodologies d’audit en cybersécurité

Un audit de sécurité suit une démarche structurée visant à évaluer la robustesse d’un système.  
Il ne s’agit pas seulement de détecter des failles, mais d’analyser les risques, la maturité des processus, et  
la capacité de l’organisation à se défendre.  
Objectifs principaux :  
|  • Identifier les vulnérabilités techniques et organisationnelles  
|  • Évaluer les contrôles existants  
|  • Prioriser les risques  
|  • Proposer des mesures correctives réalistes

---

## Approches reconnues (normes et cadres)

Plusieurs méthodologies servent de référence pour assurer la qualité et la cohérence des audits.  
Parmi les plus utilisées :  
|  • ISO 27001 / 27002 : cadre global de gestion de la sécurité  
|  • OWASP Testing Guide : référence pour les tests d’applications web  
|  • NIST SP 800-115 : méthodologie de tests d’intrusion  
|  • PTES (Penetration Testing Execution Standard) : cadre opérationnel pour les pentests  

Chaque cadre apporte une structure permettant d’éviter les oublis, d’uniformiser les livrables et de garantir la  
rigueur de l’audit.

---

## L’importance de la mindmap

La mindmap est un outil central pour structurer l’audit.  
Elle sert à organiser les informations, suivre les découvertes et garder une vision d’ensemble.  
Avantages d’une mindmap :  
|  • Clarifie les relations entre éléments techniques  
|  • Permet de visualiser rapidement le système audité  
|  • Facilite la planification et la priorisation  
|  • Aide à éviter les angles morts  
|  • Sert de trace visuelle pour le rapport final  

C’est un support de réflexion qui complète parfaitement les outils d’analyse.

---

## La mindmap comme outil de
communication  
Au-delà de l’audit lui-même, la mindmap est un excellent vecteur de communication entre :  
|  • Les équipes techniques  
|  • La direction  
|  • Les équipes de conformité  
|  • Les développeurs  

Elle permet de présenter visuellement les risques et leurs impacts sans jargon complexe.

---

## Exemple
MindMap

---

Méthodologie   Qu’est-ce qu’un audit de sécurité ?  
|  • Analyse méthodique d’un système d’information  
|  pour évaluer son niveau de sécurité.  
de l’Audit  |  • Objectif : identifier les vulnérabilités, évaluer les  
|  risques et proposer des mesures correctives.  
|  • Un audit peut être organisationnel, technique ou  
|  physique.

---

## Méthodologie :   Un audit de sécurité est une évaluation
|  méthodique et documentée d’un système  

définition  |  d’information visant à identifier des vulnérabilités,  
|  évaluer des risques et proposer des mesures  
|  correctives. Il associe démarche technique et  
|  analyse de risque pour produire des  
|  recommandations exploitables.

---

Pourquoi auditer ?  

Auditer permet d’anticiper des attaques, assurer la  
conformité réglementaire, prioriser les investissements  
sécurité et améliorer la résilience opérationnelle. C’est  
également un outil pédagogique pour les équipes IT.

---

## Méthodologie
de l’Audit  |  Pourquoi  
|  réaliser un  
|  Détection  
|  proactive des  
|  failles avant un  
|  audit ?  |  véritable  
|  attaquant.  

|  Vérification de  
|  Augmenter la  
|  la conformité  
|  résilience  
|  réglementaire  
|  globale du  
|  (RGPD, ISO  
|  système  
|  27001, PCI-  
|  d’information.  
|  DSS…).

---

## Méthodologie de
l’Audit  
Comment se déroule un audit ?  
|  1. Définition du périmètre et des objectifs.  
|  2. Signature du mandat et cadre légal.  
|  3. Collecte d’informations et reconnaissance.  
|  4. Analyse des vulnérabilités.  
|  5. Exploitation contrôlée des failles identifiées.  
|  6. Rapport détaillé + plan d’action.

---

Objectifs et   Qu’est-ce qu’un Penetration Test ?  
|  • Simulation contrôlée d’une attaque réelle.  
types de Pen   • Menée par un auditeur autorisé pour tester la résistance du  
|  système.  

Test  |  Cycle d’un Pen Test  
|  • Planification & cadrage.  
|  • Reconnaissance.  
|  • Scan & identification des vulnérabilités.  
|  • Exploitation.  
|  • Maintien d’accès & post-exploitation.  
|  • Rapport & restitution.  

|  Typologie des attaquants  
|  • Script Kiddie, Cybercriminel, Insider, Hacktiviste, State-  
|  Sponsored (APT).

---

## Types
d’audits   Type  
|  Connaissance  
|  Avantage  
|  préalable  
|  Simule une attaque  
|  Boîte noire  |  Aucune  
|  externe réelle  
|  Boîte grise  |  Infos partielles   Réaliste & efficace  

|  Gain de temps,  
|  Boîte blanche   Infos complètes  
|  profondeur technique

---

## Concepts clés :  |  Une vulnérabilité est une faiblesse
|  exploitable ; une menace est un agent ou  
vulnérabilité,  |  événement susceptible d’exploiter la  
|  vulnérabilité ; le risque combine la  
menace, risque  |  probabilité et l’impact métier.  

|  Pour prioriser les corrections, il est  
|  essentiel de relier chaque vulnérabilité à  
|  ses conséquences réelles sur les actifs  
|  critiques.

---

## Objectifs et  |  Avantages du Pen Test
|  • Vision réaliste de la sécurité.  

types de PenTest  |  • Priorisation des actions de remédiation.  
|  • Amélioration de la sensibilisation sécurité.  

|  Limites  
|  • Périmètre limité.  
|  • Ne révèle pas toutes les failles.  
|  • Résultat ponctuel (photographie à l’instant T).  

|  Cas particuliers  
|  • Déni de service (DoS/DDoS) : souvent exclus pour  
|  éviter l’interruption de service.  
|  • Ingénierie sociale : nécessite une autorisation  
|  spécifique + communication interne.

---

## Reconnaissance passive vs active

|  PASSIVE : COLLECTE D’INFORMATIONS   ACTIVE : PROBES, SCANS, INTERACTIONS  
|  EXTERNES SANS INTERACTION DIRECTE   RÉSEAU — PLUS INTRUSIF ET SOUMIS AU  
|  (WHOIS, SOURCES OSINT).  |  PÉRIMÈTRE.

---

## Reconnaissance
passive :  |  La reconnaissance passive recense informations  
méthodes et  |  publiques (DNS, WHOIS, sous-domaines, foot-  
|  printing) sans interaction directe.  
outils  
|  Outils typiques : Shodan, Censys, theHarvester,  
|  Google dorking et moteurs de recherche  
|  spécialisés (comme dns dumpster).  

|  Cette phase fournit souvent des vecteurs  
|  inattendus (sous-domaines oubliés, projets  
|  externes).

---

## Reconnaissance
|  La reconnaissance active implique scans et  
active : principes  
|  interactions (Nmap, Masscan, dirb) et révèle  
et prudence  |  ports, services, bannières et versions.  

|  Elle est plus intrusive et présente un risque  
|  d’impact ; elle doit donc respecter le mandat  
|  et des horaires définis.  

|  Documenter chaque scan et conserver  
|  hashes des résultats pour traçabilité.

---

## Découverte de services et versioning

Identifier services et  |  Techniques : scan de  
|  Relever versions  
versions permet de  |  ports, banner grabbing,  
|  exactes réduit le bruit  
|  rechercher CVE et  |  fingerprinting applicatif  
|  d’analyse et accélère la  
|  modules d’exploit  |  (WhatWeb,  
|  recherche d’exploits.  
|  pertinents.  |  Wappalyzer).

---

## Analyse des vulnérabilités : outils et
méthodologie  

Utiliser scanners (Nessus,  
OpenVAS, Nexpose) pour  |  Prioriser en fonction de  
|  Documenter les preuves  
un premier inventaire, puis  |  l’exposition, de la facilité  
|  (captures, logs, sorties  
valider manuellement  |  d’exploitation et de  
|  d’outil).  
chaque découverte pour  |  l’impact métier.  
éliminer les faux positifs.

---

## Post-
|  Après accès, l’objectif est de mesurer l’étendue du  
exploitation  |  compromis : listes de comptes, secrets, fichiers  
|  sensibles, accès réseau interne et pivoting.  
: évaluer  
l’impact réel   Collecter preuves et indiquer chemins d’attaque  
|  possibles pour reproduire et corriger.  

|  Laisser le système dans son état initial ou  
|  restaurer d’après la procédure convenue (si  
|  applicable).

---

## Maintien  |  La persistence illustre comment un attaquant
d’accès et  |  pourrait revenir : création de comptes, clés SSH,  
|  tâches planifiées, rootkits.  
persistence  

|  Dans le cadre d’un pentest, démontrer la  
|  possibilité sans installer de backdoors  
|  permanentes et documenter les méthodes  
|  exactes pour permettre la suppression par  
|  l’équipe IT.

---

## Mouvement  |  Une fois un hôte compromis, l’attaquant peut
latéral et   se déplacer latéralement pour atteindre  
|  assets plus sensibles. Utilisez techniques de  
pivoting  |  tunneling (sshuttle, proxychains), pass-the-  
|  hash, ou exploitation de services internes.  

|  Le pentest doit montrer les chemins de pivot  
|  possibles et proposer des mesures de micro-  
|  segmentation.

---

## Techniques
d’élévation de  
privilèges  

|  Sur Linux et Windows, l’élévation exploite  |  Mimikatz, sudo misconfigurations, CVE locaux et  
|  misconfigurations, failles de noyau ou services  |  SUID mal gérés sont des vecteurs courants.  
|  mal configurés.  |  Documenter les preuves d’élévation et  
|  recommander des correctifs spécifiques.

---

Tests web :  
approche  
OWASP Top 10  

|  Les applications web sont fréquemment  |  Utiliser Burp Suite pour inspection des  
|  ciblées ; la méthodologie inclut injection,   flux, fuzzing et ré-écriture de requêtes, et  
|  auth flaws, XSS, CSRF, misconfigurations  |  SQLMap pour automatiser les injections  
|  et exposure d’APIs.  |  SQL.

---

## Tests API et   Les APIs REST exposent souvent des
services  |  endpoints non durcis.  
RESTful  
|  Vérifier authentification, autorisation,  
|  validation des entrées, rate limiting, et  
|  gestion d’erreurs.  

|  Tester aussi la sécurité des tokens  
|  (JWT), l’injection, et les endpoints  
|  cachés découverts via reconnaissance.

---

## Tests
|  Auditer SMB, RDP, SSH, FTP, SMTP,  
d’infrastructure   DNS et services propriétaires.  
: protocoles et  
services  |  Chacun présente des vecteurs (auth  
|  bruteforce, mauvaises configurations,  
critiques  |  vulnérabilités connues).  

|  Vérifier versioning, chiffrement et  
|  politiques de sécurité (ciphers, policy  
|  en SSH).

---

Tests de  |  Vérifier pratiques de durcissement :  
|  patchs, configuration de firewall,  
configuration et   politiques de mot de passe, MFA,  
durcissement  |  segmentation réseau, logging  
|  centralisé.  

|  Les lacunes de configuration sont  
|  souvent plus critiques que les  
|  vulnérabilités logicielles.

---

## Outils courants pour pentest (panorama)

Panoplie recommandée : Kali  
Linux, Nmap, Masscan, Burp  
|  Suite, Metasploit,  |  Choisir outils en fonction du  
Nessus/OpenVAS, sqlmap,  |  périmètre et des restrictions  
|  Wireshark, Mimikatz,  |  contractuelles.  
|  BloodHound, Empire,  
|  CrackMapExec.

---

## Gestion des preuves et traçabilité

|  Garder un journal de bord  
|  Collecter, hacher  
|  horodaté détaillant  
(SHA256) et stocker les  
|  chaque commande et sa  
|  artefacts (captures,  
|  sortie pour garantir  
dumps, scripts) dans un  
|  auditabilité et faciliter le  
|  dépôt chiffré.  
|  rapport final.

---

## Cycle  |  Le cycle comprend : cadrage/mandat,
|  reconnaissance passive, reconnaissance active,  

détaillé d’un   scan, analyse, exploitation, post-exploitation,  
|  documentation, rapport et restitution.  

pentest  
|  Chaque étape dispose de livrables clairs (journal  
|  d’activité, captures, PoC).  

|  Le processus est itératif : les découvertes peuvent  
|  repositionner le périmètre ou les priorités.

---

## Responsabilités juridiques et éthiques de
l’auditeur  

|  L’auditeur doit agir  
|  conformément à la loi,  
|  En France, l’accès non  
|  refuser actions contraires à  
autorisé est sanctionné ; le  
|  l’éthique, et s’assurer d’une  
mandat écrit et précis est la  
|  couverture d’assurance  
|  clef de légitimité.  
|  responsabilité civile  
|  professionnelle adaptée.

---

## Méthodologies &   Préparation
|  • Collecte d’informations (IP, noms de domaine, accès  

outils  
|  réseau).  
|  • Validation des outils utilisés.  
|  • Configuration d’environnements de test isolés.

---

## Méthodologies & outils

Phases techniques  
1. Reconnaissance active et passive : Whois, Shodan, Nmap.  
2. Scan de vulnérabilités : Nessus, OpenVAS, Nikto.  
3. Exploitation : Metasploit, SQLMap, Hydra.  
4. Élévation de privilèges : exploitation locale, kernel exploit.  
5. Maintien d’accès : backdoor, persistence.  
6. Exfiltration & preuves.

---

## Méthodologies   Cas particuliers
|  • Tests de DoS : uniquement sur environnement de  

& outils  |  test.  
|  • Ingénierie sociale : phishing, test d’appel  
|  frauduleux.  
|  • Habilitations : accès admin ou utilisateur test  
|  selon mandat.

---

## Rédaction du rapport : rôle et valeur
ajoutée  

Le rapport est le livrable  
|  Il doit être structuré,  
|  clé qui convertit  
|  pédagogique et prioriser  
découvertes techniques  
|  actions selon risque et  
|  en décisions  
|  criticité métier.  
|  opérationnelles.

---

## Structure recommandée d’un rapport
d’audit  

|  Page de garde, résumé  
|  exécutif, périmètre et  
méthodologie, découvertes  |  Chaque vulnérabilité doit avoir  
classées par criticité, preuves   reproduction steps et solution  
|  et PoC, recommandations  |  proposée.  
|  détaillées, plan d’action,  
annexes techniques et logs.

---

## Le résumé exécutif : communiquer aux
décideurs  

Le résumé doit présenter en  
3–5 paragraphes le niveau  |  Il doit permettre à la  
|  Attention, le rapport doit être  
global de sécurité, risques  |  direction de comprendre  
|  adapté à la personne qui le  
majeurs, recommandations  |  l’essentiel sans connaître le  
|  cible.  
|  prioritaires et impacts  |  technique.  
|  potentiels.

---

## La synthèse technique : pour les équipes
IT  

|  Contenu : step-by-step PoC, commandes exécutées, captures  
|  d’écran, fichiers d’artefacts, et suggestions de correctifs détaillées.  

|  Fournir patchs, commandes de configuration et liens vers KB/éditeurs.

---

## Notation du   Proposer une méthode
risque :  |  combinant CVSS, probabilité  
|  d’exploitation et impact métier  
méthode  |  pour prioriser.  
pratique  
|  Expliquer comment pondérer  
|  selon la présence de contrôles  
|  compensatoires et l’exposition  
|  (internet/public vs interne).

---

Recommandations de remédiation :  
pragmatisme et priorisation  

|  Formuler  
|  Pour chaque  
|  recommandations  
|  recommandation,  
actionnables : patch, mise  
|  indiquer effort estimé  
|  à jour, durcissement,  
|  (temps/personne) et  
|  segmentation, MFA,  
|  priorité.  
|  rotation de secrets.

---

## Annexes techniques utiles

|  INCLURE LOGS, CAPTURES WIRESHARK,  |  LES ANNEXES PERMETTENT AUX ÉQUIPES DE  
|  SORTIES NMAP, CONFIGURATIONS, SCRIPTS,  |  REPRODUCTION D’EXPLOITS ET DE  
|  RÉFÉRENCES CVE ET MODULES METASPLOIT.  |  VALIDATION DES CORRECTIONS.

---

## Sensibilisation et accompagnement des
équipes  

|  Les découvertes d’un pentest doivent mener à un plan de formation  
|  (dev, ops, helpdesk).  

|  Sensibiliser sur phishing, gestion de secrets, procédures d’accès et  
|  bonnes pratiques de développement sécurisé.

---

## Automatisation et outils de remédiation
continue  

Proposer l’intégration d’outils  
|  : scanners automatisés,  
|  pipelines de tests de  |  L’automatisation réduit la  
|  sécurité, gestionnaire de  |  fenêtre d’exposition.  
|  secrets, déploiement de  
|  correctifs centralisé.

---

## Mesures défensives recommandées —
réseau  

|  Segmenter réseau, appliquer ACLs, déployer bastions, utiliser VPNs et  
|  micro-segmentation pour limiter mouvement latéral.  

|  Activer logging centralisé et alerting en corrélation SIEM pour  
|  détection rapide.

---

## Mesures défensives recommandées   Maintenir patchs, appliquer principe de
— système & applicatif  |  moindre privilège, activer MFA partout,  
|  durcir configurations, limiter services  
|  inutiles, et contrôler accès  
|  administrateur via solutions PAM.

---

## Mesures défensives recommandées —
monitoring & détection  

Déployer IDS/IPS, centraliser logs, définir use   Mettre en place playbooks d’incident pour  
cases SIEM pour détection d’anomalies et  |  traitement rythmé des alertes.  
|  d’IOC.

---

## Gestion des incidents suite à découverte
critique  

Définir procédure d’urgence  
|  : contact d’escalade,  
|  Le pentest peut révéler un  
isolement, sauvegarde des  
|  incident réel, il faut donc  
preuves, communication  
|  être prêt.  
réglementaire si données  
|  personnelles exposées.

---

## Gestion d’un incident découvert pendant
un pentest  

|  Dans ce cas, l’auditeur doit suspendre  
|  immédiatement ses actions, alerter le  
|  contact désigné dans le mandat et  
Il est possible qu’un test d’intrusion  |  L’objectif n’est pas de résoudre l’incident  
|  fournir les éléments de preuve collectés.  
mette en évidence une compromission  |  à la place du client, mais de signaler la  
|  Une procédure d’escalade doit être  
réelle en cours ou une fuite de données  |  menace et de proposer un plan de  
|  définie à l’avance : qui prévenir, sous  
|  active.  |  réaction.  
|  quel délai, et comment sécuriser les  
|  preuves tout en limitant l’impact sur le  
|  système.

---

## Éthique
professionnelle   Le pentesteur a accès à des données sensibles, parfois  
et  |  critiques ou personnelles.  
comportement  
attendu d’un  |  Il doit respecter une éthique stricte : ne jamais exfiltrer  
auditeur  |  d’informations hors du périmètre autorisé, ne pas exploiter  
|  d’informations obtenues durant un test à des fins personnelles,  
|  et éviter tout jugement négatif dans les rapports.  

|  L’impartialité est essentielle : les résultats doivent refléter  
|  précisément les risques, sans exagération ni minimisation. La  
|  confiance du client se gagne avec une attitude professionnelle,  
|  rigoureuse et respectueuse.

---

## Aspects contractuels, assurances
et responsabilités légales  
Un pentest est encadré par un contrat détaillant les responsabilités de chaque partie.  
L’auditeur doit être couvert par une assurance “Responsabilité Civile Professionnelle  
(RCP)” incluant les tests d’intrusion.  
En cas de dommage involontaire (perte de données, arrêt de service), cette assurance  
protège l’auditeur et le client. Toute action non prévue dans le mandat (par exemple :  
test de phishing ou attaque DoS sans accord explicite) peut engager la responsabilité  
pénale de l’auditeur.  
Le cadre juridique doit donc être maîtrisé avant toute action.

---

## Études de cas : erreurs à éviter
dans un pentest  
Exemple 1 : un pentesteur lance un script de scan agressif en pleine journée, saturant  
un firewall et coupant un service de production — faute d’avoir respecté les horaires  
autorisés.  

Exemple 2 : un rapport contient des données clients non anonymisées, transmis par e-  
mail non chiffré — fuite potentielle de données personnelles.  

Exemple 3 : exploitation d’une faille non autorisée dans un périmètre exclu (ERP  
finance) — rupture de contrat.  

Chaque cas rappelle l’importance du mandat, de la planification et de la  
confidentialité.

---

Que doit contenir   Un bon rapport comprend :  
|  • Détails de chaque vulnérabilité (nom, CVE, score CVSS,  
exactement un  |  description, preuve, impact).  
rapport technique  |  • Étapes d’exploitation reproduisibles (commandes, scripts  
|  utilisés, captures).  
complet ?  |  • Risque métier associé (quels comptes, quelles données,  
|  quelles fonctions impactées).  
|  • Solution corrective précise (patch, configuration,  
|  segmentations réseau).  
|  • Annexes techniques : logs, scripts, hash de fichiers, versions  
|  des outils utilisés.

---

Préparer une  |  La restitution comprend généralement deux sessions :  

réunion de  |  1. Session technique : explication des failles, démonstrations des  
|  exploits, réponses aux questions des administrateurs et  
restitution (oral du  |  développeurs.  
|  2. Session exécutive : synthèse des risques majeurs, coût  
rapport)  |  approximatif des corrections, plan d’action priorisé et ROI  
|  sécurité.  
|  Le pentesteur doit être clair, factuel, et prêt à argumenter ses  
|  recommandations.

---

## Suivi après  |  Le travail du pentesteur ne s’arrête pas à la
|  remise du rapport. Souvent, le client demande  
|  :  
transmission : que  |  • un accompagnement pour la remédiation,  

se passe-t-il après  
|  • un re-test de validation après corrections,  
|  • des formations ou workshops pour l’équipe  
|  technique,  
?  |  • une assistance pour mise en conformité  
|  (ISO 27001, RGPD, PCI-DSS).  
|  Ces étapes donnent de la valeur à l’audit et  
|  renforcent la relation de confiance.

---

## Amélioration
|  Le rapport d’audit peut être utilisé par l’équipe  
continue du  |  de défense pour améliorer la détection et la  
SOC / Blue  |  réaction aux attaques. Exemple : si un exploit  
|  n’a généré aucune alerte SIEM, il faudra créer  
Team suite au   des règles de détection.  

pentest  
|  Le pentest nourrit ainsi le SOC avec des IoCs,  
|  règles de corrélation et scénarios de  
|  simulation (Purple Teaming).

---

Merci !
