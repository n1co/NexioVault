## Slide 10 : Modifier une valeur dans le registre avec un PSProvider

```
Set-ItemProperty -Path "HKCU:\Software\MyApp" -Name "Setting1" -Value "NewValue"
```

## Slide 11 : Créer une variable d’environnement

```
Set-Item Env:MyVariable "TestValue"
```

## Slide 12 : Supprimer une variable d’environnement

```
Remove-Item Env:MyVariable
```

## Slide 13 : Tester l’existence d’un élément dans un PSProvider

```
Test-Path Env:Path
```

## Slide 14 : Sauvegarder les paramètres du registre

```
Export-Clixml -Path "C:\backup_registry.xml" -InputObject (Get-Item HKCU:\Software\MyApp)
```

## Slide 15 : Restaurer des paramètres du registre

```
Import-Clixml -Path "C:\backup_registry.xml" | Set-Item
```