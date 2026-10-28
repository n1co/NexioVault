# Socle général OSINT / méthodologie

https://bellingcat.gitbook.io/toolkit
https://osintframework.com/
https://start.me/p/L1rEYQ/osint4all
Google Advanced Search / opérateurs Google

# Analyse structurée du renseignement

- **Maltego** — indispensable pour montrer les graphes de relations.
- **Gephi** — analyse/réseaux complexes.
- **Obsidian** — prise de notes et structuration d'enquête.
- **Logseq** — alternative orientée knowledge graph.
- **Hunchly** — capture et documentation d'enquête web.
- **Zotero** — gestion des sources.
- **Datawrapper** — visualisation simple.
- **RAWGraphs** — dataviz.
- **Google Sheets / Excel** — tri, classification, pivot, scoring.
# Recherche de personnes / identités

- **Google / Bing**
- **WhatsMyName**
- **Sherlock**
- **Maigret**
- **Namechk**
- **Blackbird**
- **GHunt** — recherche liée aux comptes/services Google.
- **Have I Been Pwned** — exposition d'une adresse e-mail dans des compromissions.
- **DeHashed** — à présenter surtout comme service de recherche de données compromises.
- **IntelX / Intelligence X**
- **Truecaller** — dans les limites légales et éthiques.
- **Hunter** — recherche/validation d'adresses professionnelles.
- **Epieos** — intéressant pour les investigations autour des identifiants.

# Images et vidéos

### Recherche inversée

- **Google Lens**
- **TinEye**
- **Yandex Images**
- **Bing Visual Search**

### Vérification vidéo

- **InVID-WeVerify** — incontournable.
- Extraction de keyframes
- Recherche inversée des frames
- Analyse de thumbnails
- Analyse de contexte

InVID permet notamment d'extraire des images-clés d'une vidéo, d'effectuer des recherches inversées et d'examiner les informations/provenances disponibles.

### Métadonnées / forensic

- **ExifTool**
- **ExifReader**
- **Metadata2Go**
- **Forensically**
- **FotoForensics**
- **C2PA / Content Credentials**
- **JPEGsnoop** éventuellement

### Géolocalisation

- **Google Maps**
- **Google Earth Pro**
- **Google Street View**
- **OpenStreetMap**
- **Mapillary**
- **KartaView**
- **GeoHints**
- **SunCalc**
- **ShadowMap**
- **PeakVisor**
- **what3words**
- **Overpass Turbo**

Bellingcat recommande justement Google Maps/Earth/Street View, OpenStreetMap, GeoHints, SunCalc, Google Lens et InVID parmi les outils de géolocalisation et de vérification.

### Satellites

- **Google Earth**
- **Sentinel Hub**
- **Copernicus Browser**
- **NASA Worldview**
- **Google Earth Engine**
- **Planet** — pour montrer le principe du satellite commercial.


# Recherche web / historique des sites

- **Wayback Machine**
- **Archive.today**
- **Common Crawl**
- **Google Cache / caches alternatifs** selon disponibilité
- **urlscan.io**
- **PublicWWW**
- **SecurityTrails**
- **WHOIS / RDAP**
- **ICANN Lookup**
- **DomainTools**
- **Whoxy**
- **DNSdumpster**
- **crt.sh**
- **ViewDNS**

# Entreprises / finance / personnes morales

- **OpenCorporates**
- **Companies House**
- **ICIJ Offshore Leaks Database**
- **Open Ownership**
- **OCCRP Aleph**
- **EDGAR**
- **EU Sanctions Map**
- **OpenSanctions**
- **LittleSis**
- **North Data**
- **ImportYeti**
- **ImportGenius**
- **OpenSecrets** — surtout pour le contexte américain.

# Géolocalisation / événements / conflits

Je créerais un TP complet « Où et quand cette image/vidéo a-t-elle été prise ? »

Outils :

- Google Earth Pro
- Google Maps
- Street View
- OpenStreetMap
- Mapillary
- KartaView
- GeoHints
- SunCalc
- ShadowMap
- Sentinel Hub
- Copernicus Browser
- **Liveuamap**
- **ACLED**
- **NASA Worldview**
- **Planet**
- **Google Earth Engine**
- **Overpass Turbo**


# Aviation / maritime / transport

### Aviation

- **Flightradar24**
- **FlightAware**
- **ADS-B Exchange**
- **OpenSky Network**

### Maritime

- **MarineTraffic**
- **VesselFinder**
- **ShipFinder**
- **Equasis**

### Ferroviaire

- **Chronotrains**

# Threat intelligence / infrastructure

Pour faire le lien OSINT ↔ cyber :

- **VirusTotal**
- **Shodan**
- **Censys**
- **urlscan.io**
- **SecurityTrails**
- **crt.sh**
- **AbuseIPDB**
- **AlienVault OTX**
- **GreyNoise**
- **WHOIS / RDAP**
- **DNSDumpster**
- **ViewDNS**

# Désinformation / fact-checking

- **Google Fact Check Explorer**
- **InVID-WeVerify**
- **Google Lens**
- **TinEye**
- **Wayback Machine**
- **Hoaxy**
- **Google News**
- **Bing**
- **AFP Factuel**
- **Franceinfo – Vrai ou Faux**
- **Les Décodeurs**
- **EUvsDisinfo**
- **Full Fact**

# Crypto / blockchain

### Blockchain explorers

- **Etherscan**
- **Blockchair**
- **Blockchain.com Explorer**
- **Solscan**
- **BscScan**
- **Tronscan**

### Analyse

- **Arkham Intelligence**
- **Breadcrumbs**
- **Bubblemaps**
- **Chainabuse**

### Niveau avancé

- **Dune**
- APIs blockchain
- RPC publiques
- analyse de transactions avec Python.

# Python / collecte / scraping

https://github.com/cipher387/python-for-OSINT-21-days

### Environnement

- **Python**
- **VS Code**
- **Jupyter Notebook**
- **Google Colab**
- **GitHub**

### Bibliothèques

- `requests`
- `BeautifulSoup`
- `Scrapy`
- `Selenium`
- `Playwright`
- `pandas`
- `openpyxl`
- `lxml`
- `re`
- `json`
- `urllib`

### Outils CLI

- `curl`
- `wget`
- `jq`
- `grep`
- `ripgrep`

### Collecte OSINT

- **yt-dlp**
- **Instaloader**
- **Sherlock**
- **Maigret**
- **theHarvester**
- **SpiderFoot**

