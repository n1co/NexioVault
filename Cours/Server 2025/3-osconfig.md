# Lister tous les paramètres disponibles pour le scénario DomainController
Get-OSConfigDesiredConfiguration -Scenario SecurityBaseline/WS2025/DomainController | Select-Object Name, Value

### Activer le chiffrement SMB pour un DC

Pour les contrôleurs de domaine, le chiffrement SMB est souvent appliqué via le paramètre **`SMBServer:EnableEncryption`** (ou un équivalent listé par la commande précédente) plutôt que `SMBServerEncryptData`.
Set-OSConfigDesiredConfiguration -Scenario SecurityBaseline/WS2025/DomainController -Name "SMBServer:EnableEncryption" -Value 1


### Bloquer NTLM sur un DC

Les paramètres NTLM pour DC sont :

`Set-OSConfigDesiredConfiguration -Scenario SecurityBaseline/WS2025/DomainController -Name "NetworkSecurity: RestrictNTLM: NTLMv1" -Value 1 Set-OSConfigDesiredConfiguration -Scenario SecurityBaseline/WS2025/DomainController -Name "NetworkSecurity: RestrictNTLM: OutgoingNTLM" -Value 2`

Vérifie avec `Get-OSConfigDesiredConfiguration` si ces noms sont exactement ceux exposés pour ton serveur.

### Pare-feu de base pour DC

Les mêmes paramètres Firewall existent mais pour le scénario DC :

Set-OSConfigDesiredConfiguration -Scenario SecurityBaseline/WS2025/DomainController -Name "WindowsFirewall:DomainProfile:Enabled" -Value 1
Set-OSConfigDesiredConfiguration -Scenario SecurityBaseline/WS2025/DomainController -Name "WindowsFirewall:PrivateProfile:Enabled" -Value 1
Set-OSConfigDesiredConfiguration -Scenario SecurityBaseline/WS2025/DomainController -Name "WindowsFirewall:PublicProfile:Enabled" -Value 1


Set-OSConfigDesiredConfiguration -Scenario SecurityBaseline/WS2025/DomainController -Name "Defender:EnableRealTimeMonitoring" -Value 1


Get-OSConfigDesiredConfiguration -Scenario SecurityBaseline/WS2025/DomainController | Select Name, Value