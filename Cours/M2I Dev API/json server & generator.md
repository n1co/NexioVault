Pour créer des exemples basiques d'API en Node.js en utilisant **JSON Server** et **JSON Generator**, nous allons passer par les étapes suivantes :

1. **Installer JSON Server** pour simuler une API REST.
2. **Configurer JSON Generator** pour générer des données aléatoires.

### Exemple 1 : API simple avec JSON Server

#### Étape 1 : Installation de JSON Server

Assurez-vous d'avoir Node.js installé sur votre machine. Ensuite, installez JSON Server :

npm install -g json-server

#### Étape 2 : Créer un fichier de données

Créez un fichier `db.json` avec le contenu suivant :

`{
  "users": [
    { "id": 1, "name": "John Doe", "email": "john@example.com" },
    { "id": 2, "name": "Jane Smith", "email": "jane@example.com" }
  ]
}
`
#### Étape 3 : Lancer JSON Server

Lancez le serveur en exécutant la commande suivante dans le terminal :

json-server --watch db.json

Par défaut, le serveur écoutera sur `http://localhost:3000`. Vous pouvez maintenant accéder aux utilisateurs en utilisant les endpoints suivants :

- **GET** `/users` - pour obtenir la liste des utilisateurs.
- **GET** `/users/1` - pour obtenir l'utilisateur avec l'ID 1.
- **POST** `/users` - pour ajouter un nouvel utilisateur.

### Exemple 2 : Générer des données avec JSON Generator

#### Étape 1 : Installation de JSON Generator

Pour utiliser JSON Generator, vous n'avez pas besoin de l'installer comme un module. Vous pouvez simplement accéder à [json-generator.com](https://json-generator.com/) pour créer des modèles de données.

#### Étape 2 : Créer un modèle

Vous pouvez créer un modèle de données en utilisant la syntaxe suivante. Par exemple, pour générer des utilisateurs :

`[
  '{{repeat(5)}}',
  {
    "id": '{{index}}',
    "name": '{{firstName}} {{surname}}',
    "email": '{{email}}'
  }
]
`
Ce modèle générera 5 utilisateurs avec des noms et des adresses e-mail aléatoires.

#### Étape 3 : Utiliser les données générées

1. Allez sur JSON Generator et collez le modèle.
2. Cliquez sur "Generate" pour générer des données.
3. Vous pouvez copier les données générées et les coller dans votre fichier `db.json` pour être utilisées avec JSON Server.

### Utilisation des API

Avec JSON Server en cours d'exécution, vous pouvez maintenant interagir avec l'API :

- **Pour obtenir tous les utilisateurs :**

curl http://localhost:3000/users

Pour ajouter un nouvel utilisateur :

curl -X POST http://localhost:3000/users -H 'Content-Type: application/json' -d '{"name": "Alice Cooper", "email": "alice@example.com"}'

