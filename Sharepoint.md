https://gist.github.com/testanull/e1573437f91ec3726ab5041389c6f28d

# ÉTAPE 0
Preparer ad  dns

# ÉTAPE 1 – Installer les prérequis Windows

Ouvre PowerShell en Administrateur :

```powershell
Install-WindowsFeature Web-Server,Web-WebServer,Web-Common-Http,Web-Default-Doc,Web-Dir-Browsing,Web-Http-Errors,Web-Static-Content,Web-Http-Redirect,Web-Health,Web-Http-Logging,Web-Log-Libraries,Web-Request-Monitor,Web-Http-Tracing,Web-Performance,Web-Stat-Compression,Web-Security,Web-Filtering,Web-Basic-Auth,Web-Windows-Auth,Web-Digest-Auth,Web-Client-Auth,Web-App-Dev,Web-Net-Ext45,Web-Asp-Net45,Web-ISAPI-Ext,Web-ISAPI-Filter,Web-Mgmt-Tools,Web-Mgmt-Console,NET-Framework-45-Features,NET-Framework-45-Core,NET-Framework-45-ASPNET,NET-WCF-HTTP-Activation45,NET-WCF-TCP-Activation45,NET-WCF-Pipe-Activation45,NET-WCF-TCP-PortSharing45,Server-Media-Foundation,Windows-Identity-Foundation
```


Redémarre le serveur.

# ÉTAPE 2 – Installer SQL Server

SharePoint nécessite SQL Server (pas Express).

https://www.microsoft.com/en-us/download/details.aspx?id=101064

Versions supportées :

- SQL Server 2019
- SQL Server 2022

### Pendant l'installation SQL :

- Mode authentification mixte
- Ajouter le compte `SP_Farm` en admin SQL
- Activer :
    - Database Engine
    - Full-Text Search

Configurer :

- Collation : `Latin1_General_CI_AS_KS_WS`


# ÉTAPE 4 – Installer les prérequis SharePoint

Dans le dossier d’installation :

Lancer :

prerequisiteinstaller.exe

Cela installe :

- .NET Framework requis
- IIS components
- AppFabric (si nécessaire)
- SQL Native Client
- etc.

 Le serveur redémarrera plusieurs fois.

---

# ÉTAPE 5 – Installer SharePoint

Lancer :

setup.exe

Choisir :

- Complete Installation (Standalone = ❌ à éviter en prod)
- Entrer la clé produit
	- - Key:
    - Enterprise trial product key: M692G-8N2JP-GG8B2-2W2P7-YY7J6
    - Standard trial product key: F2DPD-HPNPV-WHKMK-G7C38-2G22J
- Accepter licence

Logs; C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\LOGS