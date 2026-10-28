grep	
### **TP 1 : Utilisation de différentes cmdlets, du pipe et du pipelinevariable**

#### **Objectif :**
Découvrir les cmdlets de base, l'utilisation du pipe (`|`), et la gestion du pipeline variable (`$PSItem` ou `$_`).

#### **Exercice 1 : Découverte des cmdlets**
1. **Lister tous les processus en cours d'exécution :**
   ```powershell
   Get-Process
   ```

2. **Filtrer les processus pour afficher uniquement ceux dont le nom contient "chrome" :**
   ```powershell
   Get-Process | Where-Object { $_.ProcessName -like "*chrome*" }
   ```

3. **Afficher les services démarrés sur la machine :**
   ```powershell
   Get-Service | Where-Object { $_.Status -eq 'Running' }
   ```

#### **Exercice 2 : Utilisation du pipe**
1. **Lister les fichiers d'un répertoire et afficher uniquement les fichiers dont la taille est supérieure à 1 Mo :**
   ```powershell
   Get-ChildItem -Path "C:\Path\To\Directory" | Where-Object { $_.Length -gt 1MB }
   ```

2. **Afficher le nom et la taille des fichiers en formatant la sortie :**
   ```powershell
   Get-ChildItem -Path "C:\Path\To\Directory" | Where-Object { $_.Length -gt 1MB } | Select-Object Name, Length
   ```

### **TP 2 : Utilisation des variables, opérateurs et expressions régulières**

#### **Objectif :**
Maîtriser la gestion des variables, l'utilisation d'opérateurs et l'intégration d'expressions régulières dans PowerShell.

#### **Exercice 1 : Utilisation des variables et opérateurs**
1. **Créer une variable pour stocker un nombre et calculer son carré :**
   ```powershell
   $number = 5
   $square = $number * $number
   Write-Output "Le carré de $number est $square"
   ```

2. **Comparer deux variables et afficher un message si elles sont égales :**
   ```powershell
   $a = 10
   $b = 10
   if ($a -eq $b) {
       Write-Output "Les valeurs sont égales."
   } else {
       Write-Output "Les valeurs sont différentes."
   }
   ```

#### **Exercice 2 : Utilisation des expressions régulières**
1. **Vérifier si une chaîne de caractères est une adresse e-mail valide :**
   ```powershell
   $email = "example@example.com"
   if ($email -match "^[\w\.-]+@[\w\.-]+\.\w{2,4}$") {
       Write-Output "L'adresse e-mail est valide."
   } else {
       Write-Output "L'adresse e-mail est invalide."
   }
   ```

2. **Extraire les numéros de téléphone d'une chaîne de caractères :**
   ```powershell
   $text = "Contactez-nous au 01-23-45-67-89 ou au 06-12-34-56-78."
   $phones = $text -match "\b\d{2}-\d{2}-\d{2}-\d{2}-\d{2}\b"
   Write-Output $phones
   ```

### **TP 3 : Mise en œuvre des structures de contrôle et utilisation des fonctions**

#### **Objectif :**
Apprendre à structurer les scripts avec des structures de contrôle (`if`, `for`, `while`) et à utiliser des fonctions avec des paramètres.

#### **Exercice 1 : Utilisation des structures de contrôle**
1. **Créer un script qui affiche les nombres de 1 à 10 en utilisant une boucle `for` :**
   ```powershell
   for ($i = 1; $i -le 10; $i++) {
       Write-Output $i
   }
   ```

2. **Utiliser une boucle `while` pour demander à l'utilisateur de saisir un nombre supérieur à 10 :**
   ```powershell
   $number = 0
   while ($number -le 10) {
       $number = Read-Host "Veuillez saisir un nombre supérieur à 10"
   }
   Write-Output "Merci ! Vous avez saisi $number"
   ```

#### **Exercice 2 : Utilisation et paramétrage de fonctions**
1. **Créer une fonction qui calcule le facteur d'un nombre :**
   ```powershell
   function Get-Factorial {
       param([int]$number)
       $result = 1
       for ($i = 1; $i -le $number; $i++) {
           $result *= $i
       }
       return $result
   }

   $factorial = Get-Factorial -number 5
   Write-Output "Le facteur de 5 est $factorial"
   ```

2. **Créer une fonction pour afficher un message de bienvenue personnalisé :**
   ```powershell
   function Show-WelcomeMessage {
       param([string]$name)
       Write-Output "Bienvenue, $name !"
   }

   Show-WelcomeMessage -name "Alice"
   ```

### **TP 4 : Récupération d'un flux RSS sur Internet et création d'une page Web**

#### **Objectif :**
Récupérer des informations en ligne via un flux RSS et créer une page Web simple en utilisant PowerShell.

#### **Exercice 1 : Récupération d'un flux RSS**
1. **Télécharger et afficher les titres des articles d'un flux RSS :**
   ```powershell
   $rss = [xml](Invoke-WebRequest -Uri "https://example.com/rss.xml").Content
   $rss.channel.item | ForEach-Object { Write-Output $_.title }
   ```

#### **Exercice 2 : Création d'une page Web simple**
1. **Créer une page HTML affichant les titres des articles :**
   ```powershell
   $html = @"
   <html>
   <head>
       <title>Flux RSS</title>
   </head>
   <body>
       <h1>Titres des articles</h1>
       <ul>
"@

   $rss.channel.item | ForEach-Object {
       $html += "<li>$($_.title)</li>"
   }

   $html += @"
       </ul>
   </body>
   </html>
"@

   $html | Out-File "rss_feed.html"
   ```

2. **Ajouter une feuille de style CSS pour améliorer l'apparence de la page :**
   ```powershell
   $css = @"
   body {
       font-family: Arial, sans-serif;
   }
   ul {
       list-style-type: none;
   }
   li {
       margin: 5px 0;
   }
"@
   $html = @"
   <html>
   <head>
       <title>Flux RSS</title>
       <style>
           $css
       </style>
   </head>
   <body>
       <h1>Titres des articles</h1>
       <ul>
"@

   $rss.channel.item | ForEach-Object {
       $html += "<li>$($_.title)</li>"
   }

   $html += @"
       </ul>
   </body>
   </html>
"@

   $html | Out-File "rss_feed_styled.html"
   ```

### **TP 5 : Gestion des adresses IP à distance et intégration d'ordinateurs dans un domaine**

#### **Objectif :**
Automatiser la gestion des adresses IP et l'intégration d'ordinateurs dans un domaine à distance.

#### **Exercice 1 : Modification des adresses IP à distance**
1. **Modifier l'adresse IP d'une machine distante :**
   ```powershell
   $newIp = "192.168.1.100"
   $newSubnet = "255.255.255.0"
   $newGateway = "192.168.1.1"

   Invoke-Command -ComputerName "RemotePC" -ScriptBlock {
       New-NetIPAddress -InterfaceAlias "Ethernet" -IPAddress $using:newIp -PrefixLength 24 -DefaultGateway $using:newGateway
   }
   ```

#### **Exercice 2 : Intégration d'un ordinateur dans un domaine**
1. **Intégrer un ordinateur distant dans un domaine :**
   ```powershell
   $domain = "mydomain.com"
   $username = "AdminUser"
   $password = "SecurePassword"
   $credential = New-Object System.Management.Automation.PSCredential($username, (ConvertTo-SecureString $password -AsPlainText -Force))

   Add-Computer -DomainName $domain -Credential $credential -ComputerName "RemotePC" -Restart
   ```

### **TP 6 : Décompression de fichiers ZIP à distance et gestion des partages**

#### **Objectif :**
Automatiser la gestion des fichiers ZIP et des partages réseau sur des machines distantes.

#### **Exercice 1 : Décompression de fichiers ZIP à distance**
1. **Décompresser un

 fichier ZIP sur une machine distante :**
   ```powershell
   Invoke-Command -ComputerName "RemotePC" -ScriptBlock {
       Expand-Archive -Path "C:\Path\To\File.zip" -DestinationPath "C:\Destination\Folder"
   }
   ```

#### **Exercice 2 : Retrouver les partages d'un poste**
1. **Lister tous les partages d'un poste distant :**
   ```powershell
   Invoke-Command -ComputerName "RemotePC" -ScriptBlock {
       Get-SmbShare
   }
   ```

### **TP 7 : Création d'un formulaire en XAML et gestion d'authentification sécurisée**

#### **Objectif :**
Apprendre à créer des interfaces utilisateur en XAML et à sécuriser les scripts d'authentification.

#### **Exercice 1 : Création d'un formulaire en XAML**
1. **Créer un formulaire simple pour capturer des informations :**
   ```powershell
   [void][System.Reflection.Assembly]::LoadWithPartialName("presentationframework")

   $xaml = @"
   <Window xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" Title="Formulaire" Height="200" Width="300">
       <Grid>
           <Label Content="Nom :" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="10,10,0,0"/>
           <TextBox Name="txtName" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="60,10,0,0" Width="200"/>
           <Button Content="OK" HorizontalAlignment="Left" VerticalAlignment="Bottom" Margin="10,0,0,10" Width="75" Click="OK_Click"/>
       </Grid>
   </Window>
"@

   $reader = (New-Object System.Xml.XmlNodeReader $xaml)
   $form = [Windows.Markup.XamlReader]::Load($reader)

   $form.ShowDialog()
   ```

#### **Exercice 2 : Script d'authentification sécurisé**
1. **Créer un script qui demande des informations d'identification sécurisées :**
   ```powershell
   $credential = Get-Credential
   ```

2. **Utiliser ces informations pour se connecter à un serveur distant :**
   ```powershell
   Invoke-Command -ComputerName "RemoteServer" -Credential $credential -ScriptBlock {
       Get-Service
   }
   ```

### **TP 8 : Gestion d'Active Directory**

#### **Objectif :**
Automatiser la gestion d'Active Directory via PowerShell.

#### **Exercice 1 : Création d'un utilisateur dans l'Active Directory**
1. **Créer un nouvel utilisateur dans Active Directory :**
   ```powershell
   Import-Module ActiveDirectory; New-ADUser -GivenName "John" -Surname "Doe" -Name "John Doe" -UserPrincipalName "jdoe@dc.local" -SamAccountName "jdoe" -Path "CN=Users,DC=demo,DC=local" -AccountPassword (ConvertTo-SecureString "P@ssw0rd!" -AsPlainText -Force) -Enabled $true
   ```

```powershell
# Importer le module Active Directory
Import-Module ActiveDirectory

# Variables
$FirstName = "John"
$LastName = "Doe"
$DisplayName = "$FirstName $LastName"
$UserPrincipalName = "jdoe@dc.local"
$SamAccountName = "jdoe"
$OU = "OU=Users,DC=dc,DC=local"  # Remplacez par le chemin OU correct dans votre domaine
$Password = "P@ssw0rd!"  # Assurez-vous que le mot de passe respecte la politique de votre domaine

# Créer l'utilisateur
New-ADUser `
    -GivenName $FirstName `
    -Surname $LastName `
    -Name $DisplayName `
    -UserPrincipalName $UserPrincipalName `
    -SamAccountName $SamAccountName `
    -Path $OU `
    -AccountPassword (ConvertTo-SecureString $Password -AsPlainText -Force) `
    -Enabled $true

```



# propre CSV
```powershell
# Importer le module Active Directory
Import-Module ActiveDirectory

# Chemin vers le fichier CSV
$CsvFilePath = "C:\Users\Public\users.csv"

# Importer les données du fichier CSV
$Users = Import-Csv -Path $CsvFilePath

# Parcourir chaque ligne du fichier CSV pour créer des utilisateurs
foreach ($User in $Users) {
    # Extraire les informations de l'utilisateur
    $FirstName = $User.FirstName
    $LastName = $User.LastName
    $DisplayName = "$FirstName $LastName"
    $UserPrincipalName = $User.UserPrincipalName
    $SamAccountName = $User.SamAccountName
    $Password = $User.Password  # Le mot de passe peut être défini dans le CSV

    # Chemin par défaut pour le conteneur des utilisateurs
    $Path = "CN=Users,DC=dc,DC=local"

    # Créer l'utilisateur dans Active Directory
    try {
        New-ADUser `
            -GivenName $FirstName `
            -Surname $LastName `
            -Name $DisplayName `
            -UserPrincipalName $UserPrincipalName `
            -SamAccountName $SamAccountName `
            -Path $Path `
            -AccountPassword (ConvertTo-SecureString $Password -AsPlainText -Force) `
            -Enabled $true

        Write-Host "Utilisateur $DisplayName créé avec succès." -ForegroundColor Green
    } catch {
        Write-Host "Erreur lors de la création de l'utilisateur $DisplayName : $_" -ForegroundColor Red
    }
}

```

csv:

FirstName,LastName,UserPrincipalName,SamAccountName,Password
John,Doe,jdoe@demo.local,jdoe,P@ssw0rd!
Jane,Smith,jsmith@demo.local,jsmith,P@ssw0rd!
Paul,Adams,padams@demo.local,padams,P@ssw0rd!
Emily,Clark,eclark@demo.local,eclark,P@ssw0rd!

#### **Exercice 2 : Requête d'objets dans Active Directory**
1. **Rechercher des utilisateurs spécifiques dans Active Directory :**
   ```powershell
   Get-ADUser -Filter {Surname -eq "Doe"} -Property SamAccountName, EmailAddress
   Get-ADUser -Filter * -SearchBase "CN=Users,DC=demo,DC=local" -Properties SamAccountName,Enabled,DistinguishedName
   ```

### **TP 9 : Création d'un classeur Excel et récupération des données serveurs**

#### **Objectif :**
Apprendre à interagir avec Excel via PowerShell et à collecter des informations système.

#### **Exercice 1 : Création d'un classeur Excel**
1. **Créer un classeur Excel et y ajouter des données :**
   ```powershell
   $excel = New-Object -ComObject Excel.Application
   $workbook = $excel.Workbooks.Add()
   $worksheet = $workbook.Worksheets.Item(1)

   $worksheet.Cells.Item(1, 1) = "Nom du serveur"
   $worksheet.Cells.Item(1, 2) = "Espace disque"
   $worksheet.Cells.Item(1, 3) = "Adresse IP"

   $workbook.SaveAs("C:\Path\To\Save\ServerData.xlsx")
   $excel.Quit()
   ```

#### **Exercice 2 : Récupération des données serveur**
1. **Récupérer l'espace disque, l'adresse IP, et les processus en cours sur un serveur distant et les enregistrer dans Excel :**
   ```powershell
   $serverName = "RemoteServer"
   $ip = (Test-Connection -ComputerName $serverName -Count 1).IPv4Address.ToString()
   $diskSpace = (Get-PSDrive -PSProvider FileSystem).Where({$_.Used -gt 0}) | Select-Object Name, @{Name="Free(GB)";Expression={[math]::round($_.Free/1GB,2)}}
   $processes = Get-Process | Select-Object ProcessName
   ```

### **TP 10 : Génération d'un mot de passe sécurisé et contrôle d'intégrité d'un fichier**

#### **Objectif :**
Créer des outils pour générer des mots de passe sécurisés et vérifier l'intégrité des fichiers.

#### **Exercice 1 : Générateur de mot de passe sécurisé**
1. **Créer un script pour générer un mot de passe aléatoire :**
   ```powershell
   function Generate-Password {
       param([int]$length = 12)
       $chars = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*()"
       -join (Get-Random -InputObject ($chars.ToCharArray()) -Count $length)
   }

   $password = Generate-Password -length 16
   Write-Output "Mot de passe généré : $password"
   ```

#### **Exercice 2 : Contrôle d'intégrité d'un fichier**
1. **Calculer le hash d'un fichier pour vérifier son intégrité :**
   ```powershell
   $file = "C:\Path\To\File.zip"
   $hash = Get-FileHash -Path $file -Algorithm SHA256
   Write-Output "SHA256 Hash : $($hash.Hash)"
   ```


# Match numero de tel

```powershell
$text = "Contactez nous au 06-30-07-12-13 ou sinon au 01-67-66-32-11"

$regex = "\b\d{2}-\d{2}-\d{2}-\d{2}-\d{2}\b"

$matches = [regex]::Matches($text, $regex)


$phoneNumbers = $matches | ForEach-Object { "test: $($_.Value) a l'index: $($_.Index)" }

Write-Output $phoneNumbers

```