---
status: draft
---

### ^^Event-Driven Architecture^^ EDA

!!! note annotate ""

      - [x] EDA est un modèle d'architecture ==qui est caractérisé par ses composants (ses systèmes) qui **réagissent** à des événements en temps réel.==
         - [ ] **réagissent** c-à-d publient, consomment ou acheminent des événements.
         - [ ] un modèle d'architecture ^^où les systèmes (les composants du système)^^ **réagissent** à des événements en temps réel.
         - [ ] Un modèle d'architecture moderne créé à partir de petits services découplés qui **réagissent** à des événements en temps réel
      ---
      - **Un événement** représente ^^un changement d'état ou une mise à jour^^. Par exemple : commande payée, ou utilisateur créé
      - Un événement envoi un état à un instant T (le numéro de transaction, le montant et le numéro de commande

### Notions

#### Définition
!!! note annotate "Définition Kafka"

    - ==Une plateforme de streaming distribué==
    - ==Une plateforme de streaming en temps réel==
    - ==Un système de messagerie distribué==
    - Kafka est une plateforme de streaming distribuée qui permet d'envoyer, stocker et traiter des messages en temps réel.
        - Avec Kafka, on peut :
            1. Publier facilement des messages dans des `topics` (push records). 
            2. Stocker une grande quantité de messages sans problème de capacité grâce à la `rétention` configurable. 
            3. Traiter les messages en temps réel dès leur arrivée, pour analyses ou transformations (stream processing).
    - Kafka permet de transférer des données entre systèmes et de créer des plateformes de streaming 
      en temps réel pour traiter et réagir aux événements immédiatement.
    - Avantages: 
        - Traitement des données en temps réel

!!! note annotate "Notes"

    1. [x] Kafka est principalement développé en Java et Scala.
    2. [x] Les consumers dans Kafka lisent les messages en ^^s'abonnant à un ou plusieurs^^ **`topics`**.
      ```mermaid
       %%{init: {'layout': 'elk', 'look': 'handDrawn', 'theme': 'neutral'}}%%
      graph LR
        A[Consumer] --> |s'abonne à un ou plusieurs| B{Topic};
      ```
    4. [x] Kafka garantit par défaut la livraison des messages au moins une fois
    5. [x] La disponibilité de Kafka est assurée par la **réplication** des **partitions** sur plusieurs **brokers**, ce qui permet 
      de continuer à servir les messages même en cas de panne d'un broker.
       <div style="display: flex; gap: 20px;">
       <div style="flex: 1;">
       ```mermaid
         %%{init: {'layout': 'elk', 'look': 'handDrawn', 'theme': 'neutral'}}%%
         flowchart LR
            A[partition 0 - réplication] --> |leader, géré par | B{Broker 1};
            A[partition 0 - réplication] --> |réplica 1, géré par | C{Broker 2};
            A[partition 0 - réplication] --> |réplica 2, géré par | D{Broker 3};
       ```
       </div>
       <div style="flex: 1;">
       ```mermaid
           %%{init: {'layout': 'elk', 'look': 'handDrawn', 'theme': 'neutral'}}%%
           flowchart LR
             AA[partition 1 - réplication] --> |leader, géré par | BB{Broker 1};
             AA[partition 1 - réplication] --> |réplica 1, géré par | CC{Broker 2};
             AA[partition 1 - réplication] --> |réplica 2, géré par | DD{Broker 3};
       ```
       </div>
       </div>
       ```shell
          kafka-topics.sh --create \
          --topic my-topic \
          --bootstrap-server localhost:9092 \
          --partitions 3 \
          --replication-factor 3
       ```
      > ^^Configuration principale^^ : **replication.factor** | min.insync.replicas
      > 
      > **replication-factor** = 3 → chaque partition a 1 leader + 2 copies.

!!! note annotate "broker"

    - **Un broker** est un serveur (worker) qui stocke les messages et gère les partitions (reçoit les messages des producers,
      les stocke dans les topics/partitions)
    - Un broker != ni un producer ni un consumer.

!!! note annotate "Topic"

    - C'est le concept central pour organiser les messages.
    - Topic c'est **`une catégorie de messages`** ou ==**`un flux nommé de messages`**== dans lequel Kafka stocke les données, 
      comme une table dans une base de données,
    - **Partitionné** : Un topic ==peut être divisé== en **partitions**, ce qui permet de **distribuer** les messages sur plusieurs
       brokers et de paralléliser la lecture.
    - **Persistant** : Les messages dans un topic sont stockés sur disque pendant un temps configurable, même après leur consommation.

!!! note annotate "Partition"

    - Une section d'un **`topic`** ==contenant un sous-ensemble de données==
    - Une partie d'un **`topic`** qui contient un sous-ensemble ordonné des messages pour permettre l'évolutivité et la parallélisation.
    - Unité de stockage ordonnée et immuable.
    ```markdown
    Topic : commandes
      Partition 0 → [msg1, msg2, msg3]
      Partition 1 → [msg4, msg5]
      Partition 2 → [msg6]
    ```
    ---
    - Une partition peut avoir différents rôles
        - Une partition peut être soit **leader** (partition principale) soit **réplica** (des copies)
        - Les réplicas (copies) peuvent être synchronisés (ISR) ou en retard 
        - Le leader (la partition principale) gère les lectures/écritures, et les réplicas (copies) assurent la haute disponibilité.
          ```mermaid
           %%{init: {'layout': 'elk', 'look': 'handDrawn', 'theme': 'neutral'}}%%
           flowchart LR
             A[Partition 0] --> |<span style="color:green">role: leader - partition principale , géré par </span>| B{Broker 1};
             A[Partition 0] --> |<span style="color:red">role: réplica - copie, géré par </span>| C{Broker 2};
             A[Partition 0] --> |<span style="color:red">role: réplica - copie, géré par </span>| D{Broker 3};
             C --> X[ISR In-Sync Replicas ou NO];
             D --> X;
             B --> Y[Gère les lectures, écritures];
             X --> W[Assure la haute disponibilité];

           classDef green fill:#9f6,stroke:#333,stroke-width:2px;
           class A green
          ```
!!! note annotate "offset"

    - **`Offset`** est la position d'un message dans une partition, utilisée par les consumer pour **suivre** leur progression
         - C'est le numéro du message dans une partition
    ```markdown
    Partition 0
    Offset: 0   1   2
    Msgs : msg1 msg2 msg3
    ```
    - Chaque message dans une partition a un numéro unique appelé offset.

      ```mermaid
      %%{init: {'layout': 'elk', 'look': 'handDrawn', 'theme': 'neutral'}}%%
      graph TB
          subgraph Partition0
              msg1[msg1] --> of00(( Offset 0))
              msg2[msg2] --> of01(( Offset 1))
              msg3[msg3] --> of02(( Offset 2))
          end
          subgraph Partition1
              msg4[msg4] --> of10(( Offset 0))
              msg5[msg5] --> of11(( Offset 1))
          end
      ```

| Concept      | Définition / Rôle                                  |                                 |
|-------------|----------------------------------------------------|------------------------------------------------|
| **Topic**    | Un flux nommé (flux logique) (comme une catégorie de messages)         | commandes, paiements, logs                     |
| **Partition**| Unité physique où les messages sont stockés dans l'ordre | Partition 0 → [msg1, msg2]                     |
| **Offset**   | Le numéro du message dans la partition      | Partition 0 : msg1 → offset 0, msg2 → offset 1 |

!!! note annotate "ZooKeeper"

    - Gére la coordination du cluster kafka: coordonne les brokers Kafka, gère l'état et Choisit le leader de chaque partition
    - Kafka peut-il fonctionner sans Zookeeper ?
        - Oui, Kafka peut fonctionner sans Zookeeper à partir de la version 2.8 en mode **`KRaft`**

!!! note annotate "consumer-group"

    - Un consumer-group est un ensemble de consumer qui se partagent la lecture des partitions d'un topic 
      pour paralléliser et équilibrer la consommation.
    - Un consumer-group assure la **répartition** des partitions entre plusieurs consumer
    - Assure un traitement parallèle
    - Permet une évolutivité horizontale.
    - Une partition peut être lue par plusieurs consumers appartenant à des groupes différents, mais dans un même groupe,
      elle n’est lue que par un seul consumer.

       <div style="display: flex; gap: 20px;">
       <div style="flex: 1;">
      ```mermaid
         %%{init: {'layout': 'elk', 'look': 'handDrawn', 'theme': 'neutral'}}%%
         graph TB
          C@{ shape: processes, label: "Consumer" } --> |s'abonne à un ou plusieurs| T@{ shape: processes, label: "Topic" }
          P@{ shape: processes, label: "Producer" } --> |publie des messages dans un ou plusieurs| T@{ shape: processes, label: "Topic" }
         style C fill:#9f6,stroke:#333,stroke-width:2px,stroke-dasharray: 5 5;
         style P fill:#bbf,stroke:#f66,stroke-width:2px,color:#fff,stroke-dasharray: 5 5
         style T fill:#ffd,stroke:#f66,stroke-dasharray: 5 5
      ```
       <div/>
       <div style="flex: 1;">
      ```mermaid
      %%{init: {'layout': 'elk', 'look': 'handDrawn', 'theme': 'neutral'}}%%
      graph TB
          subgraph partition[Partitions d'un Topic]
              p1[partition 0] --> sublist1(( msg1, msg2, msg3))
              p2[partition 1] --> sublist2(( msg4, msg5))
              p3[partition 2] --> sublist3(( msg6 ))
          end
         subgraph consumer-group1[Consumer Group 1]
              c11[consumer 1] --> p1
              c12[consumer 2] --> p2
              c13[consumer 3] --> p3
          end
         subgraph consumer-group2[Consumer Group 2]
              c21[consumer 1] --> p1
              c22[consumer 2] --> p2
              c22[consumer 2] --> p3
          end
         subgraph Brokers - Kafka cluster
             p1 --> |<span style="color:green">leader géré par </span>| B1{Broker 1};
             p1 --> |<span style="color:red">réplica1 géré par </span>| B2{Broker 2};
             p1 --> |<span style="color:red">réplica2, géré par </span>| B3{Broker 3};
          end

        classDef green fill:#9f6,stroke:#333,stroke-width:2px;
        class consumer-group1 green
        class consumer-group2 green
        style partition fill:#ffd,stroke:#f66
      ```
       <div/>
       <div/>

!!! note annotate "producer"

      - Un producteur (producer) est responsable de **publier** des messages dans un ou plusieurs topics Kafka
         - Il choisit le **topic** et éventuellement la **partition** pour chaque message. 
         - Il peut configurer la **clé** du message pour assurer que certains messages 
            vont toujours dans la même partition (utile pour l’ordre des messages).
            - la **clé** sert à regrouper les messages pour ^^préserver^^ l’ordre dans une partition. 

    !!! note annotate ""
      
          - [x] Clé → choix de la partition
          - [x] Offset → position du message dans la partition


!!! note annotate "schemas"

    - Un **`schemas`** définit la structure des messages: les champs, leur type (string, int, etc.), et les valeurs par défaut.
        - Pour assurer la compatibilité entre producers et consumers.

!!! note annotate "rétention"

    **Temps de `rétention`** s’applique au topic, définit la période pendant laquelle les messages restent disponibles (stockés)

!!! note annotate "replay"

    - **`replay`** fait référence à la relance ou à la relecture des messages déjà publiés dans un **`topic`**
    - Le **`replay`** consiste à relire des messages déjà publiés pour
        - Recalculer des résultats
        - Tester 
        - Rejouer un flux pour un nouveau consumer ou un nouveau service.

!!! note annotate "DLQ"

    - Un **`DLQ`** (Dead Letter Queue) est ^^une file spéciale^^ pour les messages qui n'ont pas pu être traités correctement.
    - Un **`DLQ`** dans Kafka est ^^un topic spécial^^ où sont envoyés les messages qui n'ont pas pu être traités correctement
    - Un **`DLQ`** est ^^un topic spécial^^ qui stocke les messages problématiques,
       pour éviter de bloquer le flux principal et permettre leur traitement ultérieur (pour investigation)


#### Sources

1. Until question number 30
    - [https://gist.github.com/bansalankit92/9414ef3614229cdca6053464fedf5038#q13-what-roles-do-replicas-and-the-isr-play](https://gist.github.com/bansalankit92/9414ef3614229cdca6053464fedf5038#q13-what-roles-do-replicas-and-the-isr-play)
2. [https://lnkd.in/d7u2D6mt](https://lnkd.in/d7u2D6mt)
3. [https://lnkd.in/dpGx-WiZ](https://lnkd.in/dpGx-WiZ)
4. [https://lnkd.in/dz6DXxb4](https://lnkd.in/dpGx-WiZ)
5. [https://lnkd.in/dUm64Qih](https://lnkd.in/dpGx-WiZ)
6. [https://lnkd.in/dQSV_7Es](https://lnkd.in/dpGx-WiZ)
7. [https://medium.com/@fromFullStack/top-25-kafka-interview-questions-867a5d8f31d8](https://medium.com/@fromFullStack/top-25-kafka-interview-questions-867a5d8f31d8)

!!! note annotate "Domain"

    - Kafka peut être utilisé dans plusieurs domaines : 
        1. `messagerie`
        2. `suivi des activités du Web en temps réel`, 
        3. surveillance des indicateurs opérationnels des applications distribuées,
        4. `agrégation des logs` d'un grand nombre de serveurs, 
        5. sourçage des événements consistant à consigner et à organiser les changements d'état dans une base de données, 
           et journaux de validation (commit logs) où sont consignées les opérations des systèmes distribués
              qui synchronisent les données et restaurent les données des systèmes défaillants.

!!! note annotate ""

    - Kafka est ^^une plateforme distribuée de données en continu^^, capable de publier, stocker, traiter 
      et souscrire à des flus d'enregistrements en temps réel.
    - Un système de messagerie distribué
    - Elle est conçue pour gérer des flux de données provenant de plusieurs sources et les fournir à plusieurs utilisateurs  
    - `Brokers` est le terme utilisé pour les serveurs, l'ensemble des brokers ayant comme but de construire un cluster.
    - Kafka a besoin d'un `cluster zookeeper` pour fonctionner, zookeeper pour maintenir la stabilité et l'intégralité du cluster Kafka
    - Kafka comprend
        - Réplication : topic les dupliquer sur plusieurs brokers (serveurs)
        - Partitionnement: topic soit segmenté et répartie sur plusieurs serveurs
    - Utilisé (data processing, centralisation de logs, métrics …)
    - pubsup: **pub**lish & **sub**scribe de messages
        - Structures modulaires (producteurs et consumers)


    - Kafka (Event-Driven Microservices using Spring Boot and Kafka)
    - https://www.redhat.com/fr/topics/integration/what-is-apache-kafka
    - https://www.javaguides.net/2022/07/event-driven-microservices-using-spring-boot-and-apache-kafka.html?spref=tw

#### Questions I

!!! note annotate "Quel protocole de communication Kafka utilise-t-il?"

    - **TCP**: Kafka communique via TCP avec un protocole binaire spécifique.
    - TCP assure une transmission fiable et ordonnée des données sur un réseau.

!!! note annotate "Comment les données sont-elles stockées dans Kafka"

    - Dans des **`Topics`** ou des files d'attente
    - Les données dans Kafka sont stockées dans des **`Topics`**, qui peuvent être **`partitionnés`**

!!! note annotate "Comment gérer l'évolution des schémas dans Kafka"

    - L'évolution des schémas désigne le processus de mise à jour des formats de données au fil du temps, 
      sans impacter les consumer existants.
    - Kafka gère ce problème grâce à ==**Confluent Schema Registry**==, qui ^^applique les règles de compatibilité^^.
        - Types de compatibilité :
            1. Rétrocompatibilité: Les nouveaux producer travaillent avec les anciens consumer. 
            2. Compatibilité ascendante : Les anciens producer travaillent avec de nouveaux consumer. 
            3. Compatibilité totale : Les deux directions sont prises en charge.

!!! note annotate "Comment les messages sont-ils ordonnés dans Kafka?"

    - Les messages dans Kafka sont ^^ordonnés par ordre d'arrivée^^ au sein de chaque partition, identifiés par un offset unique.
    - Dans Kafka, l'ordre est garanti uniquement au sein d'une partition,
        - Chaque partition agit comme une file d'attente (FIFO – First In, First Out) : le premier message publié est le premier lu.
        - Chaque partition d'un topic Kafka fonctionne comme une file d'attente ordonnée (FIFO), où les messages sont traités dans l'ordre d'arrivée.

!!! note annotate "Quel est le concept de “commit” dans Kafka"

    - Dans Kafka, **`un commit`** permet au consumer de marquer ^^la position jusqu'à^^ laquelle il a lu les messages dans une partition.
    - Cette position est appelée ^^`offset`^^.
    - `Le commit` est l'action par laquelle un consumer enregistre l'offset des messages lus, assurant une lecture durable et fiable.

!!! note annotate "La politique de rétention par défaut dans Kafka?"

    - Par défaut, Kafka conserve les messages pendant une durée définie, 
      même après leur consommation, selon une politique de rétention temporelle.
    - Cette politique permet aux consommateurs de relire les messages si nécessaire.

!!! note annotate "Comment peut-on effectuer une requête sur un topic Kafka spécifique?"

    - En utilisant un client Kafka et en s'abonnant au topic

!!! note annotate "Les performances et le débit de Kafka"

      La compression ^^réduit la taille des messages^^ et ^^la charge du réseau^^, ce qui permet de réduire la consommation d'espace disque

!!! note annotate "Kafka 4 main APIs"

    1. [x] Producer API
        - L'API Producer permet à une application `d'envoyer` des messages dans un ou plusieurs `topics` Kafka.
    2. [x] Consumer API 
        - L'API Consumer permet à une application de `s'abonner` à des topics et de ^^consommer leurs messages^^.
    3. [x] Streams API 
        - L'API Streams permet à une application de ^^lire des messages depuis des topics^^, 
         de` les transformer` et de `les écrire vers d'autres topics` en temps réel.
    4. [x] Connector API
        - L'API Connector permet de `connecter` Kafka à d'autres systèmes pour lire ou écrire des données automatiquement.

!!! note annotate "Expliquez le concept de Leader et de Follower dans Kafka."

    - Dans chaque partition d'un topic Kafka, un serveur joue le rôle de Leader.
        - Le Leader est responsable de toutes les lectures et écritures pour cette partition.
    - Les Followers (autres serveurs) copient les données du Leader pour assurer la haute disponibilité et la tolérance aux pannes.
    - Si le Leader tombe en panne, un Follower synchronisé peut prendre sa place et devenir le nouveau Leader.

!!! note annotate "Qu'est-ce qui assure l'équilibrage de charge (load balancing) des serveurs dans Kafka ?"

    - Dans chaque partition, le Leader gère toutes les lectures et écritures pour cette partition.
    - Les autres serveurs (réplicas) copient les données du Leader
    - Si le Leader tombe en panne, un des réplica devient Leader, reprenant la gestion des lectures et écritures.
    - [x] Ce mécanisme de `réplication` et de `bascule automatique` permet de répartir la charge
      et d'assurer la continuité du service, ce qui contribue à l'**équilibrage de charge** entre les serveurs.

!!! note annotate "Quel rôle jouent les Réplicas et l'ISR dans Kafka ?"

    - **`Replicas`**: Tous les serveurs qui copient les messages d'une partition 
    - **`ISR`** (In-Sync Replicas): Les réplicas qui sont synchronisés avec le leader et prêts à le remplacer si besoin
        - **`ISR`** garantit que les données sont répliquées et cohérentes

!!! note annotate "Les types de méthodes traditionnelles de transfert de messages"

    - Les méthodes traditionnelles sont : `file d'attente (Queueing)` (chaque message pour un consumer) 
        et **`Publish-Subscribe (Pub/Sub)`** (chaque message pour tous les consumer).
    ---
    Kafka combine les 3 modèles `Queue`, `Pub/Sub` et `Event Streaming`:

    - [x] **`Queue`** → consumer groups pour le load balancing
        - Dans Kafka, le modèle `Queue` est implémenté via les `consumer groups` : 
          chaque partition est lue par un seul consumer (assignée à un seul consumer dans un groupe), ce qui répartit la charge entre eux.
        - Les consumer à l'intérieur d'un groupe lisent chacun une partie → **répartition de la charge** (load balancing).
      
    - [x] **`Pub/Sub`** → diffusion à plusieurs groupes
        - Plusieurs consumer groups peuvent `s'abonner` au même `topic` c-à-d peuvent recevoir tous les messages d'un topic
        - Chaque groupe reçoit tous les messages publiés → broadcast à chaque groupe.

    - [x] **`Event Streaming`** → stockage persistant et traitement en temps réel
        - Les messages sont persistés dans un log (journal) ordonné avec des offsets. 
        - Possibilité de rejouer (replay) les messages ou de les transformer en temps réel.
    ---
    - [x] **Tolérance aux pannes** (Fault Tolerance) : les messages ne sont pas perdus même si un serveur tombe 
      en panne, `grâce à la réplication` et aux leaders/followers.
    - [x] **Haute performance** (High Throughput) : Kafka peut gérer des millions de messages par seconde.
    - [x] **Scalabilité** (Scalability) : il est facile d’ajouter des serveurs pour augmenter la capacité du cluster.

!!! note annotate "Event-Driven modèles"

    - [x] **`Event streaming`**:
        - C'est un modèle Event-Driven, où les événements sont publiés et stockés dans un log (journal) de manière chronologique, 
          un client peut lire n'importe quelle partie du flux à n'importe quel moment.

!!! note annotate "géoréplication"

    - La géoréplication consiste à copier les messages d'un cluster vers un autre cluster 
      dans une autre région pour la disponibilité, la récupération et la proximité des données.

#### Questions II
!!! note annotate "Réplication (Replication) dans Kafka, comment le configurer."

    - Principe
        - Chaque topic est découpé en partitions.
        - Chaque partition a 1 leader et 0 à N followers.
        - Les followers répliquent les données du leader.
        - Si le leader tombe, l’un des followers devient leader.
    ---
    - [x] Configuration principale : **replication.factor** | min.insync.replicas
    > replication-factor = 3 → chaque partition a 1 leader + 2 copies.
    ```shell
    kafka-topics.sh --create \
      --topic my-topic \
      --bootstrap-server localhost:9092 \
      --partitions 3 \
      --replication-factor 3
    ```



### Elasticsearch
!!! note annotate ""

    - Une solution open source distribué conçue pour la recherche et les moteurs de recherche

### noSql
!!! note annotate "noSql"

    - La possibilité de stocker des gros volumes mais avant tout de pouvoir disposer un système distribué.
    - Les principaux moteurs noSql
        - Casandra
        - MongoDB
        - Redis
    - «NoSQL signifie Not Only SQL»
        - Ce sont des bases de données non relationnelles, **conçues pour gérer** de gros volumes de données, 
          ==souvent non structurées==, avec une forte scalabilité et de bonnes performances.
        - Contrairement aux bases relationnelles, elles ne reposent pas forcément sur un schéma fixe et **peuvent prendre différentes formes** comme clé-valeur, document, colonne ou graphe.
        - Elles sont particulièrement adaptées aux besoins Big Data, temps réel et aux systèmes distribués

### Rabbitmq
!!! note annotate ""

    TODO

### MongoDB
!!! note annotate ""

    TODO

### Redis
!!! note annotate ""

    TODO

### Datadog
!!! note annotate ""

    TODO

