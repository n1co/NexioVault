## Slide 7 : Supprimer un PSDrive

```
Remove-PSDrive -Name Data
```

## Slide 8 : Création d’un PSDrive pour le registre

```
New-PSDrive -Name MyReg -PSProvider Registry -Root HKCU:\Software
```

## Slide 9 : Accéder au registre via un PSDrive

```
Set-Location MyReg:
Get-ChildItem
```

## Slide 10 : Accéder à des variables d’environnement via un PSDrive

```
New-PSDrive -Name EnvDrive -PSProvider Environment -Root ""
Set-Location EnvDrive:
Get-ChildItem
```