

#### DSL
!!! note annotate "DSL"

    - DSL: Domain-Specific Language
    - **DSL** est un mini-langage orienté (spécifique, dédié) à un domaine
        - Il permet de décrire des opérations ou des règles spécifiques au domaine de manière fluide et structurée
        - Des exemples de DSL très utilisés (Hibernate Criteria, Mockito, Spring Security ...)
            - DSL pour la manipulation de données (Stream API en Java)
            - DSL pour les tests (JUnit ou Mockito en Java)
            - DSL pour la configuration (YAML ou Dockerfile)
            - DSL pour les règles métier (Exemple : Spring Security DSL)
            - DSL pour interroger des bases de données. (SQL)
    - **Le Builder** Pattern sert à construire un objet complexe étape par étape,
        - Le builder retourne un objet final.
    - **Un DSL** peut retourner une requête, une configuration, une chaîne…
        - Ce n'est pas forcément un objet final.
        - **Interfaces imbriquées**: définissent `les étapes` du DSL (Where → OrderBy → Query)
        - **Method chaining**: Permet de naviguer `entre ces étapes` (en appelant des méthodes)

!!! note annotate "Method chaining"

    - Chaque méthode retourne `this` ou un autre objet pour enchaîner les appels
    - (enchaînement de méthodes) qui te permet de passer d'une étape à la suivante.

#### Design Pattern

!!! note annotate "Creational"

    1. Creational Patterns
        - [x] `Singleton` : Permet de s'assurer qu'une classe ne peut avoir qu'une seule instance, et fournit un accès global à cette instance

        - [x] `Factory Method`: 
            - ^^Définit une interface pour la création d'objets^^ dans une classe mère
            - Fournir une interface de création d'objets et déléguer aux sous-classes le choix de la classe concrète instanciée

        - [x] `Builder`: Construire un objet complexe étape par étape,
        - Idée : Sépare la construction d'un objet de sa représentation finale.  
        - Avantage : Facilite la création d'objets avec beaucoup de paramètres optionnels.

!!! note annotate "Structural"

    1. Structural Patterns

        - [x] `Adapter`: Connects incompatible interfaces
            - Le Patron Adapter permet de ==faire connecter des composants
            incompatibles== sans changer leur code en utilisant un objet adaptateur (un convertisseur)
            qui transforme une interface en une autre.
            - Son rôle est d'adapter l'interface d'un objet pour qu'il puisse être
            utilisé par d'autres objets sans modifier son code.
            - Example: [https://dev.to/syridit118/understanding-the-adapter-design-pattern-4nle](https://dev.to/syridit118/understanding-the-adapter-design-pattern-4nle)

        - [x] `Decorator`: ==Ajout des fonctionnalités à un objet sans modifier sa classe, il l'enveloppe dans un autre objet.==
            - En lui ajoute une couche (classe decorator) autour qui étend son comportement
            - Ajout des fonctionnalités autour d’un objet
            - Example [https://www.geeksforgeeks.org/system-design/decorator-pattern/](https://www.geeksforgeeks.org/system-design/decorator-pattern/)

        - [x] `Facade` : Simplifies complex subsystems
            - ==Fournit une interface simplifiée== pour un ensemble de classes ou un sous-système complexe.
            - Masque les détails du sous-système
            - _Key Features:_
                - Réduit le couplage: Minimizes client dependency on system internals
                - Encapsulation
            - Example [https://www.geeksforgeeks.org/system-design/facade-design-pattern-introduction/](https://www.geeksforgeeks.org/system-design/facade-design-pattern-introduction/)

!!! note annotate "Comportementales"

    1. Patterns comportementales

        - [x] `Template Method`:
            - Permet de mettre le squelette d'un algorithme dans la classe mère, mais laisse les sous-classes 
            redéfinir certaines étapes de l'algorithme sans changer sa structure. 
            - [x] Définir dans une classe de base le squelette d'un algorithme et laisser certaines étapes aux sous-classes
            - [ ] Le patron `Template Method` propose de découper un algorithme en une série d'étapes, 
            de transformer ces étapes en méthodes et de ==mettre l'ensemble des appels à ces méthodes dans une seule méthode socle,`Template Method`==
            - [ ] Déf 2: Permet de définir le squelette d'un algorithme (c'est-à-dire l'ordre exact des étapes) dans la classe de base, 
            et laisse les sous-classes redéfinir les étapes sans modifier la structure globale de l'algorithme.

        - [x] `Strategy`:
            - ==Définit un ensemble d'algorithmes==, de ==les encapsuler chacun dans une classe séparée== et de ==les rendre remplaçables==
               de sorte que le client peut choisir l'algorithme à utiliser au moment de l'exécution.
            - _Key Components of the Strategy Design Pattern_
            - _Strategy Interface_: Une interface ou classe abstracte
            - _Concrete Strategies_: Les differentes implementations du Strategy Interface

        - [x] `Observer`:
             - ==Permet à un objet d'envoyer des notifications concernant son état à d'autres objets.==
             - _Key Components of the Observer Design Pattern_
                 - Subject Interface
                 - Observer Interface
                 - ConcreteSubject: Implements the subject interface, A specific subject that holds actual data
                 - ConcreteObserver: Implements the observer interface and subscribe to subject updates

        - [x] `Command`

        - [x] `Visitor`: 
             - Ajout ==des opérations sur une structure d’objets== : un objet visiteur parcourt et traite chaque élément
             - ==Ajout des opérations sur différents types d’objets sans modifier ces objets.==
             - Permet d'ajouter de **nouvelles opérations** à une hiérarchie de classes ==sans modifier l'existant==
             - [ ] VS `Decorator :: structural`:
                 - ==Ajout des fonctionnalités à un objet sans modifier sa classe, il l'enveloppe dans un autre objet.==

        - [x] `Chaîne de responsabilité `: 
             - Permet de faire circuler des demandes (opérations) dans une chaîne de handlers. 
              Lorsqu’un handler reçoit une demande (opération), il décide de la traiter ou de l’envoyer au handler suivant de la chaîne.
             ---
             - Le projet implémente le patron Adapter pour encapsuler les objets JAXB générés à partir du schéma IEC 61850 
                et les présenter via une API.
             - L’idée: Chaque élément SCL (racine, sous-station, ...) est enveloppé dans un adpater qui sait dans quel parent 
                il se trouve, valide la relation parent-enfant et expose des méthodes métier (lecture/écriture)

!!! note annotate "CQRS"

    - CQRS (Command Query Responsibility Segregation) est un pattern d’architecture où l’on sépare nettement les opérations d’écriture 
    («commandes») des opérations de lecture («requêtes»).<br/>
    Plutôt qu’un même modèle/service pour tout faire, on a :
        - Côté commandes : des objets/handlers qui valident la logique métier et modifient l’état (ex. créer une entité, appliquer un changement).
        Ils ne retournent généralement pas de données complexes, seulement un statut. 
        - Côté requêtes : des modèles optimisés pour la lecture, souvent matérialisés via des projections ou vues spécialisées.
        Ils ne modifient rien ; ils répondent aux besoins d’affichage ou de reporting.
    ---
    - Quand l’utiliser ?
        - Scalabilité différente lecture/écriture : si l’application reçoit énormément de lectures par rapport 
          aux écritures (ou inversement), on peut optimiser chaque côté séparément.
        - Modèles de données complexes : parfois, le modèle nécessaire pour traiter 
          les commandes est très différent de celui requis pour interroger l’information.
        - Architecture événementielle : CQRS se combine bien avec Event Sourcing ou des bus d’événements
    - À éviter quand…
        - L’application est simple, avec peu de différences entre lecture et écriture.
