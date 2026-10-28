
# modules utiles

**`os`** : interactions avec le système de fichiers

```python
import os
print(os.getcwd())
```

**`sys`** : accès aux arguments et à l’environnement

```python
import sys
print(sys.argv)
```


**`datetime`** : manipulation des dates et heures
```python
from datetime import datetime
print(datetime.now())
```

**`random`** : génération aléatoire

```python
import random
print(random.randint(1, 10))
```

**`json`** : traitement des données au format JSON

```python
import json
data = json.loads('{"nom": "Alice"}')
print(data["nom"])
```

