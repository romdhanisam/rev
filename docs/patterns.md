[//]: # (!!! note annotate "Phasellus posuere in sem ut cursus &#40;1&#41;")

[//]: # ()
[//]: # (    Lorem ipsum dolor sit amet, &#40;2&#41; consectetur adipiscing elit. Nulla et)

[//]: # (    euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo)

[//]: # (    purus auctor massa, nec semper lorem quam in massa.)

[//]: # ()
[//]: # (1.  :information_source: I'm an annotation!)

1. Creational Patterns
    - [x] `Singleton` : Ensure a single global instance
    - [x] `Factory Method`: Creates Objects without specifying classes
    - [x] `Builder`: Construct complex objects step-by-step
   
2. Structural Patterns

    - [x] `Adapter`: Connects incompatible interfaces
        - Le Patron Adapter permet de ==faire connecter des composants
          incompatibles== sans changer leur code en utilisant un objet adaptateur (un convertisseur)
          qui transforme une interface en une autre.
        - Son rôle est d’adapter l’interface d’un objet pour qu’il puisse être 
          utilisé par d’autres objets sans modifier son code.
        - Example: [https://dev.to/syridit118/understanding-the-adapter-design-pattern-4nle](https://dev.to/syridit118/understanding-the-adapter-design-pattern-4nle)
     - [x] `Decorator`: ==Adds new functionality to an object==
        - Example [https://www.geeksforgeeks.org/system-design/decorator-pattern/](https://www.geeksforgeeks.org/system-design/decorator-pattern/)
    - [x] `Facade` : Simplifies complex subsystems
        - ==Fournit une interface simplifiée== pour un ensemble de classes ou un sous-système complexe.
        - Masque les détails du sous-système
        - _Key Features:_
            - Réduit le couplage: Minimizes client dependency on system internals
            - Encapsulation
      - Example [https://www.geeksforgeeks.org/system-design/facade-design-pattern-introduction/](https://www.geeksforgeeks.org/system-design/facade-design-pattern-introduction/)

3. Patterns comportementales

    - [x] `Strategy`: 
        - ==Définit une ensemble d’algorithmes==, de ==les encapsuler chacun dans une classe séparée==
          et de ==les rendre remplaçables==
          de sorte que le client peut choisir l’algorithme à utiliser au moment de l’exécution.
        - _Key Components of the Strategy Design Pattern_
            - _Strategy Interface_: Une interface ou classe abstracte
            - _Concrete Strategies_: les differentes implementations du Strategy Interface
    - [x] `Observer`:
        - ==Permet à un objet d’envoyer des notifications concernant son état à d’autres objets.==
        - _Key Components of the Observer Design Pattern_
            - Subject Interface
            - Observer Interface
            - ConcreteSubject: Implements the subject interface, A specific subject that holds actual data
            - ConcreteObserver: Implements the observer interface and subscribe to subject updates
    - [x] `Command`


!!! note annotate "Les Design Pattern"

    - Un ensemble des solutions abstraits à des problèmes récurrents dans l'organisation pratique de classe d’objets.

        > - Les modèles de création
        >     - Les modèles de création sert pour déléguer la création d'objets à d'autre classe d'objets.
        >     - Les Design Patterns de Création sont un ensemble de design patterns qui permettent de créer
        >       des objets d'une manière flexible, modulaire et qui facilite leur réutilisation.<br>
        >       Ils sont utilisés pour résoudre des problèmes de conception liés à la création d'objets.
        > - Les modèles de structures
        > - Les modèles comportementaux

#### Singleton
!!! note annotate "Singleton"

	- C’est un pattern de conception qui permet de s’assurer qu’une classe ne peut avoir qu’une seule instance,
      et fournit un accès global à cette instance
    - Il est souvent utilisé pour gérer des ressources partagées comme des connexions à une base de données, 
      des fichiers de configuration ou des logs.

    ![img.png](assets/images/singleton.png)

#### Factory Method
!!! note annotate "Factory Method"

    - ^^Définit une interface pour la création d’objets^^ dans une classe mère, 
       mais ce sont les sous-classes qui décident (qui choisit) quel objet instancier.
    - Ce modèle centralise la création d’objets tout en offrant une flexibilité pour produire différents types de produits.
      
        > Exemple: Retourne une instance concrète de Pattern.
        ```java
        Pattern.compile(String regex)
        ```

    ![img.png](assets/images/factory-method.png)

#### Abstract Factory
!!! note annotate "Abstract Factory"

    - ^^Fournit une interface pour créer des familles d’objets liés ou dépendants^^ sans préciser leur classe concrète.
        
        > Exemple: Fournit des objets de connexion à une base de données
        ```java
        javax.sql.DataSource via DataSourceFactory
        ```
    ![img.png](assets/images/abstract-factory.png)



#### Builder
!!! note annotate "Builder"

    - But : construire un objet complexe étape par étape. 
    - Permet de construire un objet complexe étape par étape sans avoir à passer un grand nombre de paramètres dans un constructeur.
    - Idée : sépare la construction d’un objet de sa représentation finale.  
    - Avantage : facilite la création d’objets avec beaucoup de paramètres optionnels.

    ![img.png](assets/images/builder.png)
    ```java
    StringBuilder
    ```

#### Prototype
!!! note annotate "Prototype"

    - But : créer de nouveaux objets en copiant un objet existant (prototype).  
    - Idée : utiliser la méthode clone() plutôt que new.  
    - Avantage : plus rapide et utile quand la création est coûteuse.

    ![img.png](assets/images/prototype.png)
    ```java
    obj.clone(), Date#clone(), ArrayList#clone()
    ```


[//]: # (#### Template)

[//]: # (!!! note annotate "Template")

[//]: # ()
[//]: # (    - )

[//]: # ()
[//]: # (#### Observer)

[//]: # (!!! note annotate "Observer")

[//]: # ()
[//]: # (    - )

[//]: # ()
[//]: # (#### Visitor)

[//]: # (!!! note annotate "Visitor")

[//]: # ()
[//]: # (    - )

[//]: # ()
[//]: # (#### Facade)

[//]: # (!!! note annotate "Facade")

[//]: # ()
[//]: # (    - )

[//]: # ()
[//]: # (#### Composite)

[//]: # (!!! note annotate "Composite")

[//]: # ()
[//]: # (    - )

