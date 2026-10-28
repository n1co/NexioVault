

---

## Énoncé

### Contexte :
Vous allez créer un conteneur Docker qui exécute une application web simple en Python avec Flask.  
Cette application affichera `Hello Docker!` dans le navigateur.

### Structure du projet :

docker-flask-app/ 
├── app.py
└── Dockerfile


### Étapes :

1. Installer Docker (si ce n’est pas déjà fait)
2. Créer le fichier `app.py` :

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
    return "Hello Docker!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)


```

- **Créer un fichier `Dockerfile`** :
    
    - Utilisez une image Python officielle
        
    - Copiez les fichiers nécessaires
        
    - Installez Flask
        
    - Démarrez l'application
        
- **Construire l'image Docker**
    
- **Exécuter le conteneur** avec un mappage du port `5000`
    
- **Tester dans le navigateur** ou via `curl localhost:5000`
