# ![](https://img.shields.io/badge/Spring-%23F5F6F7.svg?&logo=Spring&logoColor=green)

!!! note annotate ""

    - Spring est un framework de développement d'applications Java. 
    - Il s'agit d'une plateforme qui {++fournit des supports pour le développement d'applications Java++} robustes et à grande échelle. 
    - Il propose également plusieurs modules qui sont utilisées pour créer toutes sortes d’applications, tous ces modules sont construits sur leurs conteneurs de base. 
    - Il y a beaucoup de dépendances et Spring a donc eu le besoin de développer son propre système de gestion de dépendances. Spring IoC (Inversion of Control)
    - Un plateforme qui **facilite** le travail du développeur.

!!! note annotate ""

    - Spring, est basé sur une architecture en couches qui comprend différents modules. 
    - Chaque module offre des fonctionnalités différentes pour les applications et tous ces modules sont construits sur leurs conteneurs de base.

#### Spring IoC/DI
> Spring IoC (Inversion of Control):
!!! note annotate ""

    - Spring IoC est **un concept clé du Framework** et **une des principales fonctionnalités du Framework**.<br>
    Via le conteneur Spring IoC (cad via l’environnement (le cadre) d’exécution fourni par Spring) 
    il modifie fondamentalement la manière dont les objets sont créés et gérés donc le conteneur est responsable de la gestion des objets
    - Il utilise l'injection de dépendances pour réaliser l'inversion de contrôle
    > ET favorisant un couplage faible et une meilleure modularité.

#### IoC: l'inversion de contrôle 
!!! note annotate ""

    - L'inversion de contrôle est un {++principe de conception dans lequel le contrôle++} de la création des objets, 
    de la configuration et du cycle de vie des objets est **transféré** du code de l'application vers un conteneur ou un framework 
    - ((C’est le principe sur-lequel la gestion des objets et les dépendances entre les objets est 	gérés par un framework externe (un conteneur))
    > Ce conteneur gère les dépendances des objets ET favorisant ainsi un code plus maintenable et testable.  
    > 
    > Le détails dépend de l’abstraction et pas l’inverse : un  détail qui s’adapte à l’abstraction (contrat, interface)
     Les implémentations concrètes doivent suivre l’interface (le contrat) Ce n’est pas le Service (contrat) qui s’adapte à un détail, c’est le détail qui s’adapte à l’abstraction (contrat, interface)

#### DI: Dependency Injection
!!! note annotate ""

    - C’est une technique de création des objets dans laquelle les objets ne créent pas eux-mêmes leurs dépendances. 
    Au lieu de ça, l'objet déclare ses dépendances et c’est le 	rôle d’un objet externe ou à un framework de fournir les dépendances concrètes à l’objet.
    > L'injection de dépendances est une forme d’IoC.


### Spring Boot

!!! note annotate ""

	- **SringBoot** est un projet Spring (c-a-d basé sur le framework Spring) - opinionated. 
    - Il {++prend en charge une grande partie de la configuration standard++}: comme ==un serveur web intégrés tomcat== et ==des dépendances utiles simplifiés via des starter.==,
     qui permet de créer facilement des applications Java (autonomes).
    - Il est souvent utilisé dans l'architecture microservice en raison de la simplicité qu'il permet.


#### Comment SpringBoot simplifie  ?

Les avantages de Spring Boot <br>
Il simplifie le développement par l'auto-configuration: son

!!! note annotate ""

    **==Auto-Configuration==**
    !!! note annotate ""

        - Il y a beaucoup moins de configuration (concernant la gestion des servlets, le chargement du contexte Spring, la connexion à la base de données). 
        - L’utilisation de Spring Boot, et l’annotation **@SpringBootApplication** placée au niveau de la classe principale, déclenchent automatiquement de nombreuses opérations en background qui nous sont nécessaires.
        - On peut alors se concentrer sur le code métier au lieu de passer un temps fou à configurer le framework qu’il utilise.

            But 
            > L’auto-configuration permet de se concentrer sur le code métier, et simplifie énormément la mise en œuvre des composants Spring qui sont utilisés.
    
            Comment fonction la Configuration automatique dans Spring Boot ?
            > L’annotation **@SpringBootApplication** déclenche la configuration automatique de l’infrastructure Spring
    
            > Au démarrage de l’application, Spring Boot Scanne toutes les classes qui ont l’annotation @Configuration: les classes de configuration spécifiques à l’application et les classes suffixées par AutoConfiguration
            >
            > - Spring utilise aussi les JAR présents dans le classpath pour prendre des décisions
            > - Spring repose sur des activations conditionnelles
            > - Spring fournit des modules starters qui ont des classes d’auto-configuration  
        
    **==Le déploiement==**
    !!! note annotate ""

        - Les applications créées avec Spring Boot peuvent être exécutées avec une simple commande `java -jar`
        - Le projet contient un tomcat embarqué au sein même du JAR généré. 
        - Le projet web peut donc être déployé au sein de ce tomcat embarqué.

    **==La gestion des propriétés==**
    !!! note annotate ""

        - Spring Boot **permet de gérer les propriétés** au sein d’un programme en toute simplicité.
        - La gestion des propriétés rend l'application {++configurable++}.
        - Dans fichier `applications.properties` ou `applications.yml`. 
            - Les informations qui étaient saisies ont été prises en compte par certaines classes, sans que nous ayons besoin d’agir. 
        
        - Ce fichier est l’un des éléments clés pour la gestion des propriétés de notre programme.
            - La gestion des propriétés ne se limite pas à ce simple fichier, il est facilement possible de récupérer même des variables d’environnement système, et de les fournir à nos classes.


    **==Optimisation de la gestion des dépendances==**
    !!! note annotate ""

        - La gestion des dépendances est simplifiée grâce aux starters qui regroupent plusieurs dépendances et homogénéisent les versions. 


    **==Le monitoring et la gestion du programme==**
    !!! note annotate ""

        - `Spring Boot Actuator` correspond à une fonctionnalité de Spring Boot qui permet de monitorer et de manager notre programme pendant qu’il est en cours d’exécution.


{++ ++}
