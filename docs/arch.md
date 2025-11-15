
### Architecture distribuée
!!! note annotate "Architecture distribuée"

    - Un système distribué est un ensemble de programmes informatiques sur plusieurs nœuds de calcul distincts pour atteindre un objectif commun et partagé.
    - Il s’appuie dur des noeuds distincts pour communiquer et se synchroniser sur un réseau commun
    - Les systèmes distribués contribuent souvent à améliorer **la fiabilité et les performances** du système.
       
        ---
        > Fiabilité 
    
        - La fiabilité est améliorée en supprimant les points de défaillance centraux.
        - Les nœuds d'un système distribué offrent une redondance de sorte que si l'un d'eux tombe en panne, 
           d'autres nœuds sont prêts à couvrir et à remplacer la panne.
        ---
        > Performances 
    
        - les performances sont améliorées, car les nœuds peuvent facilement être mis à ==l'échelle horizontalement et verticalement==. 
          Si un système subit une charge importante, des nœuds supplémentaires peuvent être ajoutés pour aider à absorber la charge.
        - La capacité d'un nœud individuel peut également être augmentée pour gérer une charge importante.
        
        ---
        > #### horizontal scaling
    
        - _La montée en charge horizontale_ consiste à ajouter plusieurs instances du même service pour gérer une charge plus importante.
        - La mise à l'échelle horizontale peut améliorer **la disponibilité, la fiabilité et la tolérance aux pannes** de nos microservices, 
          ainsi que le débit et la réactivité globale de notre système.
        - Il introduit également une certaine complexité et une certaine surcharge, telles que **la gestion de la configuration**, de **la synchronisation** 
          et de **la communication des instances de service**, ainsi que la gestion des problèmes potentiels tels que la latence du réseau, 
          la cohérence des données et **la découverte des services.**

        ---
        > #### scale-up

        - _La mise à l'échelle verticale_: c'est le processus d'augmenter la capacité d'une seule instance de service pour gérer une charge plus importante.
        - La mise à l'échelle verticale peut être plus simple et moins coûteuse que la mise à l'échelle horizontale, car elle ne nécessite pas d'ajouter de serveurs ou de conteneurs


#### Types
!!! info annotate "Types de systèmes distribués"

    Il existe de nombreux types de systèmes distribués. Les plus courants sont les suivants :

    1. ##### ^^Client-serveur^^
    
        - Une architecture client-serveur se décompose en deux responsabilités principales.
        - Le client est responsable de la présentation de l'interface utilisateur, qui se connecte ensuite au serveur via le réseau.
        - Le serveur est responsable de la gestion de la logique métier et de la gestion des états.
       
    2. ##### ^^À plusieurs niveaux^^
        - Une architecture à plusieurs niveaux <u>étend l'architecture client-serveur</u>. Dans une architecture à plusieurs niveaux, le serveur est décomposé en nœuds granulaires supplémentaires, qui découplent les responsabilités supplémentaires du serveur principal, comme le traitement et la gestion des données.

    3. ##### ^^SOA^^

        - L'architecture orientée services (SOA) est <u>un prédécesseur des microservices</u>.
        - La principale différence entre SOA et microservices est la portée du nœud

    4. ##### ^^Microservices^^

        - [x] L'architecture microservice ==décrit une manière de concevoir une application comme une suite de service
          hautement disponible==, **autonomes** at ==faibelement couplées==,
          ^^que l'on peut developper, versionner, déployer et scaler indépondement^^
        - [x] ^^Une approche de développement^^ qui consiste {++ à décomposer les applications en éléments les plus simples, 
          indépendants les uns des autres++}. Contrairement à une approche monolithique classique,
          selon laquelle tous les composants forment une entité indissociable.
        - [x] ^^Un microservice est une architecture^^ pour les applications {++qui sépare une application en plusieurs petits services Web autonomes++}.
        - [x] Le concept de base du microservice, c'est une application qui ne fait qu'une chose, mais qui la fait de manière optimale:
        - <h6>Les microservices désignent à la fois: Une architecture Une approche de développement</h6>
        - **Avantages**:
            - Par rapport aux applications monolithiques, les microservices sont beaucoup 
              plus faciles à créer, tester, déployer et mettre en jeu
                - Il est facilement **remplaçable** pour offrir une évolutivité à l’application.
                - Il est **déployé indépendamment**.
                - Son **développement est indépendant**.
            - Les microservices sont plus robustes et permettent une mise à l'échelle verticale et horizontale plus dynamique.
            - Robustes: solides, résistants, etc. : les microservices sont plus résistants aux pannes que les monolithes.
            - Une architecture de microservice complète est un réseau interconnecté de services isolés.

##### ^^Event-Driven Architecture^^

- Un modèle d'architecture ==où les systèmes **réagissent** à des événements en temps réel.==
    - [x] **réagissent** c-à-d publient, consomment ou acheminent des événements.
    - Un modèle d'architecture moderne créé à partir de petits services découplés qui **réagissent** à des événements en temps réel

- **`Un événement`** représente ^^un changement d'état ou une mise à jour^^. Par exemple : commande payée, ou utilisateur créé 
    - Un événement transmet (envoi) un état à un instant T (le numéro de transaction, le montant et le numéro de commande

1. ^^Les différents modèles pour implémenter une event driven architecture^^
    - L'architecture Event-Driven (orientée événements) peut utiliser le modèle de **`Pub/sub`** ou le modèle de **`Event streaming`**.
        1. **`Pub/sub`** : lorsqu'un événement est publié, le router va le communiquer 
            à tous les consumers qui sont abonnés à cet événement. 
            Si un nouveau consumer s'abonne à un événement, il n'a pas accès aux événements passés. 
        2. **`Event streaming`** : les événements sont enregistrés dans un journal dans l'ordre chronologique. 
            Un client peut lire n'importe quelle partie du flux à n'importe quel moment. 
            Cela signifie aussi qu'un client peut s'abonner à tout moment et avoir accès aux événements passés.
2. ^^Caractéristiques de l’EDA^^
    1. **Découplage** des composants :
        - Les services communiquent via des événements sans dépendances directes. 
        ^^ce qui leur permet d'être modifiés et déployés de manière indépendante.^^
    2. **Scalabilité** et résilience :
        - Les systèmes peuvent gérer une grande quantité d’événements simultanés.
    3. Traitement **asynchrone** :
        - Les services ne nécessitent pas de réponse immédiate, améliorant la fluidité.

##### SOA vs Microservices
!!! info annotate "SOA vs Microservices"

    - Similitudes:
        - Les architectures SOA et microservices, contrairement aux applications monolithiques, <u>fournissent des composants qui sont uniquement responsables d'une tâche particulière.</u>

    - Différences:
        - La première différence est que lors du développement de microservices, chaque équipe peut développer et déployer des applications indépendamment des autres services. En revanche, lors de l'utilisation de SOA, chaque équipe développant un service <u> doit connaître le mécanisme de communication commun à utiliser pour réaliser le SOA.</u>
        - La deuxième différence principale entre SOA et microservices est que dans une SOA, <u>le bus de services</u> , utilisé comme <i>couche de communication entre les services</i>, peut potentiellement devenir un point de défaillance unique.
        
        <u>En termes de stockage</u>

        - une architecture SOA utilise généralement une solution de <u>stockage de données partagée</u> traditionnelle comme un SGBDR.
        - Une architecture de microservices, en revanche, a une approche plus flexible qui est souvent déclinée sous le nom de <i>stockage natif de conteneur</i> .
          C'est-à-dire que vous <u>définissez votre stockage comme un conteneur lui-même, tout comme vos applications.</u>
        
    - Chaque approche a ses avantages et ses inconvénients : l'utilisation d'une solution de données partagées facilite la réutilisation des données entre les applications. D'un autre côté, pour les applications qui s'exécutent indépendamment les unes des autres, une solution de stockage indépendante (comme le stockage de conteneurs) peut être plus facile à démarrer et à maintenir.

!!! info annotate "Les microservices ont-ils un rapport avec les conteneurs Linux ?"

    - Lorsque les microservices sont stockés dans des conteneurs,
      il est plus simple de tirer parti du matériel et d'orchestrer les services,
      notamment les services de stockage, de réseau et de sécurité.
      `Les microservices et les conteneurs constituent la base du développement d'applications cloud-native`

### Le traçage distribué
!!! note annotate ""

    - Le traçage distribué est une méthode utilisée pour **profiler** ou **surveiller** le résultat d'une ^^requête exécutée sur un système distribué^^.
    - Surveiller un système distribué c-a-d surveiller le résultat d'une requête exécutée dans le système.
    - ^^La surveillance d'un système distribué^^ peut être difficile, car chaque nœud individuel possède son propre flux de journaux et de mesures.
    - Pour obtenir une vue précise d'un système distribué, ces mesures de nœuds distincts doivent être regroupées dans une vue globale.
        - Les requêtes adressées aux systèmes distribués n'accèdent généralement pas à l'ensemble des nœuds du système, mais à un ensemble partiel ou à un chemin à travers les nœuds.
        - Le traçage distribué met en lumière les chemins couramment utilisés dans un système distribué et permet aux équipes d'analyser et de surveiller ces chemins.
        - Le traçage distribué est installé sur chaque nœud du système et permet ensuite aux équipes **d'interroger** le système **pour obtenir des informations** sur **l'état du nœud et les performances des requêtes**.


#### Comment techniquement faire le traçage distribué dans Kafka ?
!!! note annotate "traçage distribué dans Kafka"

    - Ajouter des identifiants de trace dans les messages
    - Intégration avec un système de traçage 
        - Kafka ne fait pas de traçage distribué natif → on utilise des outils de tracing :
            - OpenTelemetry (standard open-source)
    - Dans Kafka, **le traçage distribué** se fait en ajoutant un **traceId** dans les headers des messages, 
        en instrumentant producteurs et consommateurs avec un outil comme OpenTelemetry ou Jaeger, 
        et en collectant tous les **spans** pour reconstruire le chemin complet des messages 
        dans le système distribué.
        - L’instrumentation des producteurs et consommateurs consiste à créer des spans 
                et à propager les traceIds dans les headers des messages, pour suivre 
                le chemin complet d’un message dans Kafka.

    ```shell
    Producteur --[traceId]--> Broker Kafka --[traceId]--> Consommateur --> Service downstream
    ```

### Cloud Native
!!! note annotate ""

    - Le Cloud Native décrit une approche de développement logiciel dans laquelle
      les applications sont dès le début conçues pour une utilisation sur le Cloud.
    - L'approche Cloud Native repose sur quatre piliers qui sont liés et interdépendants.
        1. Du côté technique, on trouve les **microservices** et les **technologies de conteneurs**
           qui constituent la base du développement d'applications cloud-native
        2. Du côté de la stratégie, on trouve les **processus de développement** et la **Continuous Delivery**
          sont bien établis dans une culture DevOps agile.
    - Donc les applications Cloud Native sont créées dans le cadre d'une collaboration
      étroite entre toutes les parties prenantes (les développeurs et les enterprises).
    - Dans le but d'une meilleure solution pour les utilisateurs finaux.
    - Par exemple, dans un cadre d'un échange constant, l'équipe de développeurs ajoute à un microservice
      certaines fonctionnalités livrées automatiquement par des processus de Continuous-Delivery

    **Mot clés:** PaaS, Openshift

### Servless
!!! note annotate ""
    
    - Le serverless est un paradigme de conception et de déploiement d'applications pilotées par les événements.
      dans lequel les ressources informatiques sont fournies sous forme de services par Cloud.
      cad le matériel et l'infrastructure sont tous gérés par le fournisseur.<br/>
    - AWS est l'un des acteurs majeurs du serverless.

    **Mot clés :** FaaS

### API
!!! info annotate "API (Application programming Interface)"

    - Est une interface de programmation. Elle constitue le cadre à travers lequel un développeur peut interagir avec une application.
    - Les APIs sont un ensemble de classes, méthodes, fonctions et constantes qui sert d'interface par laquelle un logiciel peut offrir ses services à d'autres logiciels.
    - Elles servent concrètement à accéder aux données d'une application
      et à utiliser ses fonctionnalités.


