# TP 1 — Création d’un sous-site SharePoint 2016

## Contexte

L’équipe RH souhaite disposer d’un espace dédié afin de centraliser ses documents internes.

Votre mission consiste à créer un sous-site collaboratif destiné au service RH.

---

## Objectifs pédagogiques

À l’issue du TP, vous serez capable de :

- Créer un sous-site SharePoint 2016
- Choisir un modèle adapté
- Configurer les paramètres de navigation
- Comprendre l’héritage des autorisations

---

# Partie 1 — Réalisation

## Étape 1 — Accéder au portail SharePoint

1. Ouvrir votre navigateur Internet
2. Accéder à l’URL SharePoint fournie par le formateur
3. Se connecter avec votre compte utilisateur

---

## Étape 2 — Créer le sous-site

1. Cliquer sur l’icône **Paramètres** en haut à droite
2. Cliquer sur **Contenu du site**
3. Sélectionner **Nouveau sous-site**

Compléter les informations suivantes :

|Champ|Valeur|
|---|---|
|Titre|Ressources Humaines|
|URL|rh|
|Description|Site collaboratif RH|
|Modèle|Site d’équipe|

---

## Étape 3 — Paramétrer la navigation

1. Conserver l’affichage dans la barre de lancement rapide
2. Choisir l’héritage de navigation du site parent
3. Cliquer sur **Créer**

---

# Résultat attendu

Vous devez désormais voir :

- Un nouveau sous-site nommé « Ressources Humaines »
- Une nouvelle entrée dans la navigation SharePoint
- Une URL contenant /rh

---

# Correction détaillée

## Ce qu’il fallait faire

Le modèle « Site d’équipe » est le modèle standard de collaboration dans SharePoint 2016.

Il fournit automatiquement :

- Une bibliothèque Documents
- Une liste Calendrier
- Une liste Annonces
- Une structure collaborative prête à l’emploi

---

## Point pédagogique

### Héritage des autorisations

Le sous-site hérite automatiquement des droits du site parent.

Cela signifie que :

- Les membres du site parent ont accès au sous-site
- La gestion des droits reste simplifiée
- Aucun groupe spécifique n’est encore nécessaire