## **1. Vérifier qu’OpenSSH est installé**

1. Ouvrir **PowerShell en administrateur** sur le serveur cible.
    
2. Vérifier que le serveur OpenSSH est installé :
    

`Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH.Server*'`

3. Si ce n’est pas installé :
    

`Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0`

4. Démarrer et configurer le service SSH pour qu’il démarre automatiquement :
    

`Start-Service sshd Set-Service -Name sshd -StartupType 'Automatic'`

5. Vérifier que le port 22 est ouvert dans le **pare-feu Windows** :
    

`New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22`


## **3. Configurer WAC pour utiliser SSH**

1. Ouvrir **Windows Admin Center**.
    
2. Aller dans **+ Ajouter un serveur** ou modifier un serveur existant.
    
3. Sélectionner **Connexion SSH** comme type de connexion (au lieu de Windows / WinRM).
    
4. Entrer l’**IP ou le nom du serveur**, l’utilisateur et soit :
    
    - Le mot de passe de l’utilisateur, ou
        
    - Une clé privée si vous utilisez l’authentification par clé SSH.
        
5. Tester la connexion. Si tout est correct, WAC utilisera SSH pour exécuter les commandes PowerShell à distance.