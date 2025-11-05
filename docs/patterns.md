!!! note annotate "Les Design Pattern"

    - Un ensemble des solutions abstraits à des problèmes récurrents dans l'organisation pratique de classe d’objets.

        > - Les modèles de création
        >     - Les modèles de création sert pour déléguer la création d'objets à d'autre classe d'objets.
        >     - Les Design Patterns de Création sont un ensemble de design patterns qui permettent de créer
        >       des objets d'une manière qui soit flexible, modulaire et qui facilite leur réutilisation.<br>
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


#### Template
!!! note annotate "Template"

    - 

#### Observer
!!! note annotate "Observer"

    - 

#### Visitor
!!! note annotate "Visitor"

    - 

#### Facade
!!! note annotate "Facade"

    - 

#### Composite
!!! note annotate "Composite"

    - 

