# TP 5 — Gestion des autorisations

## Contexte

Les documents RH contiennent des données sensibles.

Le sous-site doit disposer d’une sécurité spécifique.

---

## Objectifs pédagogiques

- Comprendre l’héritage des permissions
- Rompre l’héritage
- Ajouter des groupes SharePoint

---

# Partie 1 — Réalisation

## Étape 1 — Accéder aux permissions

1. Ouvrir le sous-site RH
2. Cliquer sur **Paramètres du site**
3. Cliquer sur **Autorisations du site**

---

## Étape 2 — Rompre l’héritage

1. Cliquer sur **Arrêter l’héritage des autorisations**
2. Confirmer l’opération

---

## Étape 3 — Ajouter des groupes

Créer les groupes suivants :

|   |   |
|---|---|
|Groupe|Niveau|
|RH Membres|Contribution|
|RH Visiteurs|Lecture|

---

# Résultat attendu

Le sous-site possède maintenant ses propres permissions.

---

# Correction détaillée

## Vérification

Le message suivant doit apparaître :

« Ce site possède des autorisations uniques »

---

## Point pédagogique

### Pourquoi éviter trop de ruptures d’héritage ?

Une multiplication des droits uniques entraîne :

- Une administration complexe
- Des erreurs de sécurité
- Une maintenance difficile

---

## Bonne pratique

Toujours privilégier les groupes SharePoint plutôt que des droits utilisateur individuels.