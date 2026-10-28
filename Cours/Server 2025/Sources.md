Nouveautes: https://www.it-connect.fr/chapitres/windows-server-2025-les-nouveautes/

Editions server 2025: https://www.it-connect.fr/chapitres/windows-server-2025-les-editions-et-les-modeles-de-licence/

2022 to 2025 https://petri.com/in-place-upgrade-to-windows-server-2025/


# pages 32k

## ⚠️ Points à noter / Limitations

- Une fois la fonctionnalité 32 K activée, **on ne peut pas revenir au format 8K** (mode simulation 8K ou format natif). [Microsoft Learn+1](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/32k-pages-optional-feature?utm_source=chatgpt.com)
    
- Les sauvegardes AD faites **avant** l’activation de 32K (en 8K) ne seront plus utilisables pour restauration dans une forêt en mode 32K. [Microsoft Learn+1](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/32k-pages-optional-feature?utm_source=chatgpt.com)
    
- Un contrôleur de domaine mis à niveau (“in-place upgrade”) depuis une version antérieure continue avec une base à pages de taille 8K, et ne deviendra pas automatiquement capable de 32K. [Robert Smit MVP Blog+1](https://robertsmit.wordpress.com/2024/11/20/upgrading-to-windows-server-2025-a-step-by-step-guide-ws2025-winserv-azurearc/?utm_source=chatgpt.com)

SETUP -> onglet powershell https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/enable-32k-pages-optional-feature?tabs=PowerShell

## Ce qu’on appelle le locateur de DC (DC Locator)

Le _DC Locator_ (ou localisateur de contrôleurs de domaine) est le mécanisme qui permet à un client Windows de trouver un contrôleur de domaine (DC) lorsqu’il a besoin de services AD (authentification, etc.). Historiquement, ce localisateur utilisait plusieurs méthodes, dont :

- la découverte basée sur DNS (SRV, etc.)
    
- la découverte basée sur NetBIOS / WINS
    
- la diffusion (broadcast / mailslots) dans certains cas, en mode « legacy »



enable ssh https://www.it-connect.fr/chapitres/windows-server-2025-utiliser-et-configurer-acces-ssh/#II_Activer_le_serveur_SSH

admin center: https://learn.microsoft.com/fr-fr/windows-server/manage/windows-admin-center/deploy/install?tabs=desktop-experience


# vu par eux

rien de precis
faire le tour
securite \

JEAN-JAQUES HONORE

msiexec /i "C:\WACDEPLOY\WindowsAdminCenter.msi" /qn /L*v log.txt SME_PORT=6516 SSL_CERTIFICATE_OPTION=generate