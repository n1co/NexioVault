# Conception d’architectures modernes : SOA, Microservices et API Management	
![[Pasted image 20261028143255.png]]
---
# Objectifs pédagogiques
À l’issue de cette formation, vous serez capable de :
• Comprendre les mutations des systemès 	d’information
• Concevoir une architecture orientée services
• Développer des API REST robustes
• Mettre en œuvre des microservices scalables
* Piloter une stratégie d’API Management
---
# Mutation des systèmes d’information
---
# Pourquoi les architectures évoluent

>Les architectures évoluent sous la pression de contraintes métier et techniques.

Historiquement, les systèmes étaient centralisés, stables, mais peu flexibles.
Aujourd'hui, ils doivent être :
* distribués 
* adaptables 
* disponibles en permanence 

> Le changement n'est pas technologique uniquement : il est aussi business.

---
# De monolithe à distribué
> Un monolithe regroupe toute la logique dans une seule application.

Problèmes :
* déploiement lourd 
* couplage fort 
* évolution lente 
### Exemple : une modification du module paiement nécessite de redéployer toute l’application.

> D’où le passage vers des architectures distribuées.
---
# Cloud-Native: Changement de paradigme
```mermaid
flowchart TB
    A["Le cloud-native n'est pas un simple hébergement."]
    
    subgraph B["C'est une façon de concevoir :"]
        direction LR
        B1["applications<br/>découplées"]
        B2["tolérantes aux<br/>pannes"]
        B3["scalables<br/>automatiquement"]
    end

    C["Exemple : une application qui absorbe un pic<br/>de trafic sans intervention humaine."]

    A --> B
    B --> C

    style A fill:#3a7a35,stroke:#2d6a2b,color:#ffffff
    style B fill:#a3bb5a,stroke:#8aab3a,color:#ffffff
    style B1 fill:#ecd5c3,stroke:#ffffff,color:#000000
    style B2 fill:#dfe5c3,stroke:#ffffff,color:#000000
    style B3 fill:#cbd3c1,stroke:#ffffff,color:#000000
    style C fill:#e07a45,stroke:#d0652f,color:#ffffff
    ```
---
![[Untitled.mindmap]]

truc

![[SecureVault/Untitled.excalidraw]]

[[AWSSec1]](truc)

