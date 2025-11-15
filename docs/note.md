---
status: draft
---
🧑‍💻
#### TODO List 1
!!! note annotate "TODO List 1"

    - [x] Liquibase
    - [x] Testing (notamment Junit)
    - [x] Propagation spring (question - 2 method transational in each other)
    - [x] Agilité (bonne pratique, scrum vs kanban , c quoi kanban?)
    - [x] API (Restful)
    - [x] Stateful | Stateless
    - [x] DDD (wording notions)
        - Le DDD se concentre sur le fait de donner au domaine métier plus d’importance d’une technologie en particulier.
    - [x] Spring MVC
    - [x] Spring Data
    - [x] Spring Actuator (metrics, type de métrique gauge)
        - Un Gauge mesure une valeur instantanée dans le temps, Gauge reflète l’état actuel d’une variable.
        - Counter qui ne fait que compter des événements cumulés
    - [x] Default method in interface (Java)
        - Une méthode avec une implémentation par défaut
            - Fournir un comportement par défaut que les classes peuvent surcharger si besoin.
    - ---
    - [x] Athentification vs Athorisation (oauth2)
    - [x] 🧑‍💻Tracabilité distribué (comment faire (technique)) - voir kafka s'il y a une technique en particulier
    - [x] Les types d'injection

#### TODO List 2
!!! note annotate "TODO List 2"

    - [ ] Spring Scheduling
    - [ ] CSRF
    - [ ] Cycle de vie Maven
    - [ ] MapStruct
    - [x] Lombok

#### TODO List 3
!!! note annotate "TODO List 3"

    - [ ] CI/CD & DevOps best practices
    - [ ] Automated testing.
    - [ ] Test Containers
    - [ ] sécurité OWASP
    - [X] NgRx
        - Elle permet de gérer l’état global de l’application
    - [ ] Bonne pratique stream Java
    - [ ] Spring Batch, Cucumber
    - [x] Design pattern CQRS
    - [ ] TDD : on arrete d'essayer de trouver l'algorithme final du premier coup
        - TDD évite de chercher la solution parfaite d’un coup: on construit l’algorithme étape par étape via les tests
        - TDD consiste à écrire d’abord un test, puis le code minimal pour le faire passer, et enfin refactorer le code.


#### Spring MVC | Data
!!! note annotate ""

    - **Spring MVC**
        - Basé sur le pattern MVC, qui ==gère les requêtes HTTP==
        - Gére la couche web et les requêtes HTTP
        - Dans Spring Boot, Spring MVC est auto-configuré via spring-boot-starter-web
    - **Spring Data**
        - Un module qui ==simplifie l’accès aux bases de données.==
        - Fournit des repositories abstraits pour interagir avec les bases de données,

    - **Les types d'injection**:
        - Spring supporte l’injection par constructeur, par setter et par champ.
            La plus recommandée est l’injection par constructeur pour l’immutabilité et la testabilité.


#### API | REST, RESTfull
!!! note annotate "API | REST, RESTfull"

    - [x] **API** est une interface de programmation, et un **contrat d’interaction** qui définit comment 
      un logiciel expose ses fonctionnalités à d’autres systèmes
    - ---
    - [x] **API** Dans le contexte des applications web, une API — souvent **une API REST**:
        - Une interface qui permet à un client (application, service, frontend…) de communiquer 
          avec un serveur via des requêtes **HTTP**.
        - Elle définit des endpoints et des méthodes HTTP pour manipuler des données :
            - GET : récupérer des données
            - POST : créer une nouvelle ressource
            - PUT : mettre à jour une ressource existante
            - DELETE : supprimer une ressource
    - ---
    - [x] **REST**
        - Est **un style architectural** pour créer des services web
        - **Un ensemble de règles** pour exposer des ressources via HTTP de manière uniforme, claire et évolutive.
        - Parmi ces règles ?
            - Les principales contraintes REST sont :
                - Client–serveur : séparation entre l’interface utilisateur et la logique serveur. 
                - Sans état (**stateless**) : chaque requête contient toutes les informations 
                    nécessaires (le serveur ne stocke pas l’état du client).
                     - Le serveur n’enregistre pas l’état du client d’une requête à l’autre.
                     - Chaque requête est indépendante.
                - URI bien définies
                - Méthodes HTTP correctes
    - [x] Un service est dit **RESTful** lorsqu’il respecte réellement les contraintes REST.
    - ---  
    - Elle constitue le cadre à travers lequel un développeur peut interagir avec une application.
    - Les APIs sont un ensemble de classes, méthodes, fonctions et constantes 
      qui sert d'interface par laquelle un logiciel peut offrir ses services à d'autres logiciels.
    - Elles servent concrètement à accéder aux données d'une application
      et à utiliser ses fonctionnalités.

#### Stateful
!!! note annotate "Stateful"

    - [x] Le serveur conserve l’état des interactions avec chaque client entre les requêtes. 
        Chaque requête dépend du contexte stocké côté serveur.

#### 
!!! note annotate ""
    - Que se passe-t-il lorsqu’une méthode transactionnelle Spring appelle une autre méthode transactionnelle dans la même classe ?

        - Lorsqu’une méthode transactionnelle (`methodA`) appelle une autre méthode transactionnelle (`methodB`) 
        dans la même classe, la transaction de `methodB` ne sera pas prise en compte 
        si l’on utilise les annotations Spring classiques.

#### Liquibase
!!! note annotate "Liquibase"

    - Est un ==outil de versioning et de gestion des changements de base de données==, 
      qui permet de déployer et ==suivre les modifications de schéma== de façon automatisée et fiable.

#### Scrum | Kanban
!!! note annotate "Scrum | Kanban"

    - **Scrum** **organise** le travail ==en sprints fixes avec rôles et réunions définis==
    - **Kanban** **gère** le flux de travail ==de façon continue et flexible==

!!! note annotate ""
!!! note annotate ""
!!! note annotate ""
!!! note annotate ""
!!! note annotate ""
!!! note annotate ""
!!! note annotate ""
