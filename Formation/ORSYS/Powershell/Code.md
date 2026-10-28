# Exemple de texte à tester

# Regex pour email
```
$email = "user.name@example-domain.com"
$regex = '^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$'

if ($email -cmatch $regex) {
    Write-Output "Adresse email valide"
} else {
    Write-Output "Adresse email invalide"
}
```

#### Vérification user valide

```powershell
$usernames = @(
    "john.doe",
    "jane.doe@entreprise.com",
    "john@entreprise.com",
    "john.doe@company.com",
    "john.doe@entreprise",
    "john.doe@entreprise.com"
)

$pattern = '^[a-zA-Z]+[.][a-zA-Z]+(@entreprise\.com)?$'

foreach ($username in $usernames) {
    if ($username -match $pattern) {
        Write-Output "$username est un nom d'utilisateur valide."
    } else {
        Write-Output "$username n'est pas un nom d'utilisateur valide."
    }
}



```


#### Guess the number

```powershell
# Générer un nombre aléatoire entre 1 et 100
$randomNumber = Get-Random -Minimum 1 -Maximum 101
$guess = 0
$attempts = 0

while ($guess -ne $randomNumber) {
    $guess = Read-Host "Devinez le nombre entre 1 et 100"
    $attempts++

    if (-not ($guess -match '^\d+$')) {
        Write-Output "Veuillez entrer un nombre valide."
    }
    elseif ($guess -lt $randomNumber) {
        Write-Output "Le nombre est plus grand."
    }
    elseif ($guess -gt $randomNumber) {
        Write-Output "Le nombre est plus petit."
    }
    else {
        Write-Output "Félicitations ! Vous avez deviné le nombre $randomNumber en $attempts tentatives."
    }
}
```

#### rss
```powershell
# URL du flux RSS
$url = "https://lemonde.fr/rss/une.xml"


# Téléchargement du flux RSS
[xml]$rss = Invoke-WebRequest -Uri $url

# Parcourir et afficher les éléments du flux RSS
foreach ($item in $rss.rss.channel.item) {
    # Extraire les informations
    $title = $item.title.'#cdata-section'  # Accéder au contenu de la balise CDATA
    $link = $item.link
    $description = $item.description.'#cdata-section'  # Accéder au contenu CDATA dans la description
    $pubDate = $item.pubDate

    # Afficher les informations de chaque élément
    Write-Output "Titre : $title"
    Write-Output "Lien : $link"
    Write-Output "Description : $description"
    Write-Output "Date de publication : $pubDate"
    Write-Output "-----------------------------------------"
}

```

# CIMSESSION
```powershell
# Créer une session CIM avec le serveur distant "Server01"
$session = New-CimSession -ComputerName "Server01"

# Récupérer la liste des interfaces réseau
$networkAdapters = Get-CimInstance -CimSession $session -ClassName Win32_NetworkAdapterConfiguration | 
                   Where-Object { $_.IPEnabled -eq $true }

# Afficher les informations des interfaces réseau et leurs adresses IP
foreach ($adapter in $networkAdapters) {
    Write-Host "Interface: $($adapter.Description)"
    Write-Host "MAC Address: $($adapter.MACAddress)"
    Write-Host "IP Addresses: $($adapter.IPAddress -join ', ')"  # Combine les IPs en une seule ligne
    Write-Host "-----------------------------------------"
}

# Fermer la session CIM après usage
Remove-CimSession -CimSession $session
```

# XAML

```powershell
Add-Type -AssemblyName PresentationFramework

# Charger le XAML
[xml]$xaml = @"
<Window xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        Title="Formulaire XAML" Height="200" Width="300">
    <Grid>
        <TextBox Name="MyTextBox" Width="150" HorizontalAlignment="Center" VerticalAlignment="Top" Margin="0,20,0,0"/>
        <Button Name="MyButton" Content="Afficher" Width="80" HorizontalAlignment="Center" VerticalAlignment="Center" />
    </Grid>
</Window>
"@

# Créer la fenêtre
$reader = (New-Object System.Xml.XmlNodeReader $xaml)
$window = [Windows.Markup.XamlReader]::Load($reader)

# Ajouter une action au bouton
$button = $window.FindName("MyButton")
$textbox = $window.FindName("MyTextBox")
$button.Add_Click({
    [System.Windows.MessageBox]::Show("Vous avez entré : $($textbox.Text)")
})

# Afficher la fenêtre
$window.ShowDialog()

```

# XAML2
```powershell
[xml]$xaml = @"
<Window xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        Title="Formulaire Complet" Height="250" Width="350">
    <Grid>
        <Label Content="Nom :" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="10,10,0,0"/>
        <TextBox Name="NameTextBox" Width="200" HorizontalAlignment="Left" Margin="60,10,0,0" VerticalAlignment="Top"/>
        
        <Label Content="Genre :" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="10,50,0,0"/>
        <ComboBox Name="GenderComboBox" Width="100" HorizontalAlignment="Left" Margin="60,50,0,0" VerticalAlignment="Top">
            <ComboBoxItem Content="Homme" />
            <ComboBoxItem Content="Femme" />
        </ComboBox>
        
        <Button Name="SubmitButton" Content="Soumettre" HorizontalAlignment="Center" VerticalAlignment="Bottom" Width="100" />
    </Grid>
</Window>
"@

$reader = (New-Object System.Xml.XmlNodeReader $xaml)
$window = [Windows.Markup.XamlReader]::Load($reader)

# Récupérer les contrôles
$nameTextBox = $window.FindName("NameTextBox")
$genderComboBox = $window.FindName("GenderComboBox")
$submitButton = $window.FindName("SubmitButton")

# Gestion de l'événement de clic
$submitButton.Add_Click({
    $name = $nameTextBox.Text
    $gender = $genderComboBox.SelectedItem.Content
    [System.Windows.MessageBox]::Show("Nom : $name, Genre : $gender")
})

# Afficher la fenêtre
$window.ShowDialog()
```

# PassGen

```powershell
	# Fonction pour générer un mot  de passe
function Generate-Password {
    param (
        [int]$length = 12  # Longueur du mot de passe par défaut
    )

    # Définir les caractères à utiliser
    $lowercase = 'abcdefghijklmnopqrstuvwxyz'
    $uppercase = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
    $digits = '0123456789'
    $specialChars = '!@#$%^&*()-_=+[]{};:,.<>?'
    

    $allChars = $lowercase + $uppercase + $digits + $specialChars
    
    $password = -join ((Get-Random -Count $length -InputObject $allChars.ToCharArray()) | Sort-Object)
    
    return $password
}

# Utilisation de la fonction pour générer un mot de passe
$password = Generate-Password -length 16  # Vous pouvez changer la longueur ici
Write-Output "Votre mot de passe généré est : $password"

```

# passgen propre

```powershell
function Generate-Password {  
param (  
[int]$Length = 12  
)  
  
$allChars = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!@#$%^&*()-_=+[]{};:,.<>?"  
  
$password = ""  
  
for ($i = 0; $i -lt $Length; $i++) {  
$password += $allChars[(Get-Random -Minimum 0 -Maximum $allChars.Length)]  
}  
  
return $password  
}  
  
# Exemple  
$password = Generate-Password -Length 16  
Write-Output "Votre mot de passe généré est : $password"
```

# Geoloc


```powershell
# Récupérer toutes les connexions réseau actives via netstat
$netstatOutput = netstat -n | Select-String -Pattern "TCP|UDP"

# Extraire les adresses IP distantes uniques (entrantes et sortantes)
$ips = @()
foreach ($line in $netstatOutput) {
    $columns = $line -split '\s+'
    
    if ($columns.Count -ge 3) {
        # Adresse IP distante (en général 3ème ou 4ème colonne selon le format)
        $remoteAddress = $columns[-2] -replace ':\d+$',''  # On enlève le port (:XXXX)
        
        # Vérifier si c'est une vraie adresse IP (éviter 0.0.0.0 et adresses locales)
        if ($remoteAddress -match '^\d{1,3}(\.\d{1,3}){3}$' -and $remoteAddress -notlike "127.0.0.*" -and $remoteAddress -notlike "0.0.0.0") {
            $ips += $remoteAddress
        }
    }
}

# Rendre les IPs uniques
$uniqueIps = $ips | Sort-Object -Unique

# Fonction pour géolocaliser une IP via l'API ipinfo.io
function Get-GeoLocation {
    param(
        [string]$ip
    )
    
    try {
        # Requête HTTP vers l'API ipinfo.io
        $response = Invoke-RestMethod -Uri "http://ipinfo.io/$ip/json"
        return [PSCustomObject]@{
            IP          = $ip
            City        = $response.city
            Region      = $response.region
            Country     = $response.country
            Latitude    = $response.loc.Split(',')[0]
            Longitude   = $response.loc.Split(',')[1]
            Organization = $response.org
        }
    } catch {
        Write-Warning "Impossible de géolocaliser l'IP $ip"
    }
}

# Parcourir chaque IP et récupérer les informations de géolocalisation
$geoData = @()
foreach ($ip in $uniqueIps) {
    $location = Get-GeoLocation -ip $ip
    if ($location) {
        $geoData += $location
    }
}

# Afficher les résultats
$geoData | Format-Table -AutoSize

# Optionnel : Exporter les données dans un fichier CSV
$geoData | Export-Csv -Path "C:\chemin\vers\fichier\geolocalisation_ips.csv" -NoTypeInformation

```

# Create local user

```powershell
# Importation du fichier CSV
$csvPath = "chemin\vers\votre\fichier.csv"
$users = Import-Csv -Path $csvPath

# Boucle pour chaque utilisateur dans le fichier CSV
foreach ($user in $users) {
    # Extraction des données depuis le fichier CSV
    $nom = $user.nom
    $prenom = $user.prenom
    $motdepasse = $user.motdepasse
    
    # Construction du nom d'utilisateur (p.nom)
    $username = "$($prenom.Substring(0,1)).$($nom)" -replace '\s', '' # Supprime les espaces éventuels
    
    # Conversion en minuscules pour uniformiser
    $username = $username.ToLower()
    
    # Construction de l'email fictif (optionnel si nécessaire)
    $email = "$username@credit-agricole.fr"
    
    # Debug : Affichage des informations générées
    Write-Host "Création de l'utilisateur : $prenom $nom"
    Write-Host "Nom d'utilisateur : $username"
    Write-Host "Mot de passe : $motdepasse"
    
    # Vérification si l'utilisateur existe déjà
    if (Get-LocalUser -Name $username -ErrorAction SilentlyContinue) {
        Write-Host "L'utilisateur $username existe déjà. Passage au suivant." -ForegroundColor Yellow
        continue
    }
    
    # Commande pour créer un utilisateur local
    try {
        New-LocalUser -Name $username `
                      -FullName "$prenom $nom" `
                      -Password (ConvertTo-SecureString $motdepasse -AsPlainText -Force) `
                      -PasswordNeverExpires $true `
                      -UserMayNotChangePassword $false `
                      -AccountNeverExpires $true
                      
        Write-Host "Utilisateur local $username créé avec succès." -ForegroundColor Green
    } catch {
        Write-Host "Erreur lors de la création de l'utilisateur $username : $_" -ForegroundColor Red
    }
}

Write-Host "Script terminé."

```

```csv
nom,prenom,motdepasse Dupont,Jean,Password123! Martin,Lisa,SecurePass!
```


# Inventaire en XSLX

```powershell
# Définir le chemin de sauvegarde du fichier Excel
$computerName = $env:COMPUTERNAME
$excelFile = "$(Get-Location)\${computerName}.xlsx"

# Créer une instance d'Excel
$Excel = New-Object -ComObject Excel.Application
$Excel.Visible = $false
$Excel.DisplayAlerts = $false

# Ajouter un nouveau classeur
$Workbook = $Excel.Workbooks.Add()

# Fonction pour ajouter une feuille et remplir les données
function Add-Worksheet {
    param (
        [string]$SheetName,
        [array]$Data
    )
    
    if ($Data.Count -eq 0) { return }
    
    $Sheet = $Workbook.Sheets.Add()
    $Sheet.Name = $SheetName
    
    # Ajouter les en-têtes
    $colIndex = 1
    foreach ($key in $Data[0].PSObject.Properties.Name) {
        $Sheet.Cells(1, $colIndex) = $key
        $colIndex++
    }
    
    # Ajouter les données
    $rowIndex = 2
    foreach ($item in $Data) {
        $colIndex = 1
        foreach ($key in $Data[0].PSObject.Properties.Name) {
            $Sheet.Cells($rowIndex, $colIndex) = $item.PSObject.Properties[$key].Value
            $colIndex++
        }
        $rowIndex++
    }
}

# Collecte des informations
$SystemInfo = Get-CimInstance Win32_ComputerSystem | Select-Object Name, Manufacturer, Model, TotalPhysicalMemory
$OSInfo = Get-CimInstance Win32_OperatingSystem | Select-Object Caption, Version, BuildNumber, OSArchitecture
$Processor = Get-CimInstance Win32_Processor | Select-Object Name, NumberOfCores, MaxClockSpeed
$RAM = Get-CimInstance Win32_PhysicalMemory | Select-Object Manufacturer, Capacity, Speed
$Disks = Get-CimInstance Win32_LogicalDisk | Select-Object DeviceID, VolumeName, FileSystem, Size, FreeSpace
$Network = Get-CimInstance Win32_NetworkAdapterConfiguration | Where-Object { $_.IPEnabled -eq $true } | Select-Object Description, MACAddress, IPAddress
$Software = Get-ItemProperty HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\* | Select-Object DisplayName, DisplayVersion, Publisher

Add-Worksheet -SheetName "Système" -Data @($SystemInfo)
Add-Worksheet -SheetName "OS" -Data @($OSInfo)
Add-Worksheet -SheetName "Processeur" -Data @($Processor)
Add-Worksheet -SheetName "Mémoire" -Data $RAM
Add-Worksheet -SheetName "Disques" -Data $Disks
Add-Worksheet -SheetName "Réseau" -Data $Network
Add-Worksheet -SheetName "Logiciels" -Data $Software

# Sauvegarde du fichier et fermeture d'Excel
$Workbook.SaveAs($excelFile)
$Excel.Quit()

# Libération de la mémoire
[System.Runtime.Interopservices.Marshal]::ReleaseComObject($Workbook) | Out-Null
[System.Runtime.Interopservices.Marshal]::ReleaseComObject($Excel) | Out-Null

Write-Output "Inventaire terminé. Fichier enregistré sous : $excelFile"

```


# generateur mdp oriente objet

```powershell
class PasswordGenerator {
    # Propriétés de la classe
    [string]$lowercase = 'qwertyuiopasdfghjklzxcvbnm'
    [string]$uppercase = 'QWERTYUIOPASDFGHJKLZXCVBNM'
    [string]$numbers = '1234567890'
    [string]$specialChars = '#$%^&*()_+!@[]{}|;:?><,./'
    [int]$length

    # Constructeur de la classe
    PasswordGenerator([int]$length = 16) {
        $this.length = $length
    }

    # Méthode pour générer un mot de passe aléatoire
    [string] GeneratePassword() {
        $allChars = ($this.lowercase + $this.uppercase + $this.numbers + $this.specialChars).ToCharArray()
        [string]$password = ''

        for ($i = 1; $i -le $this.length; $i++) {
            $password += Get-Random -InputObject $allChars
        }

        return $password
    }

    # Méthode pour générer un objet PowerShell avec le mot de passe
    [PSObject] GetPasswordObject() {
        $password = $this.GeneratePassword()
        return [PSCustomObject]@{
            Password = $password
        }
    }
}

# Exemple d'utilisation de la classe
$generator = [PasswordGenerator]::new(25) # Créer un générateur de mot de passe avec une longueur de 25
$passwordObject = $generator.GetPasswordObject()

# Afficher le mot de passe généré
$passwordObject
```



```
$Path = "C:\"

$MinSize = 100MB

$LargeFiles = Get-ChildItem -Path $Path -Recurse -File | Where-Object { $_.Length -gt $MinSize }

$FileList = $LargeFiles | Select-Object FullName, @{Name="SizeMB";Expression={[math]::Round($_.Length / 1MB, 2)}}

$FileList | Export-Csv -Path "files.csv" -NoTypeInformation -Encoding UTF8

Write-Host "Export terminé. $(($FileList).Count) fichiers enregistrés dans files.csv."
```


# find file resursive

```powershell
# Chemin du CSV
$CsvPath = "C:\files.csv"

# Vérifier si le CSV existe déjà et créer l'entête si nécessaire
if (-Not (Test-Path $CsvPath)) {
    "FullName,SizeMB" | Out-File -FilePath $CsvPath -Encoding UTF8
}

# Taille minimale
$MinSize = 100MB

# Fonction pour scanner les dossiers
function Scan-Folder {
    param([string]$Folder)

    try {
        # Parcours tous les fichiers du dossier
        Get-ChildItem -Path $Folder -File -ErrorAction Stop | ForEach-Object {
            if ($_.Length -gt $MinSize) {
                $SizeMB = [math]::Round($_.Length / 1MB, 2)
                "$($_.FullName),$SizeMB" | Out-File -FilePath $CsvPath -Append -Encoding UTF8
                Write-Host "Fichier trouvé : $($_.FullName) - $SizeMB MB"
            }
        }

        # Parcours récursif des sous-dossiers
        Get-ChildItem -Path $Folder -Directory -ErrorAction Stop | ForEach-Object {
            Scan-Folder $_.FullName
        }
    }
    catch {
        Write-Warning "Accès refusé ou erreur sur $Folder"
    }
}

# Lancer le scan sur le disque C:
Scan-Folder "C:\"

Write-Host "Scan terminé."

```