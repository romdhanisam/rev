### Transaction
!!! note annotate ""

    Une transaction est {++une séquence d'accès (lectures ou mises à jour)++} à la base de données qui satisfait 4 propriétés : ACID
    > Les propriétés ACID (atomicité, cohérence, isolation et durabilité) c'est un ensemble de propriétés qui garantissent qu'une transaction est exécutée de façon fiable.

!!! note annotate ""

    1. **A**tomicité → tout ou rien (la transaction s’exécute entièrement ou est annulée). 
        - Toutes les opérations dans une transaction ==sont appliquées ou annulées ensemble==.
    2. **C**ohérence → 
        - Assure que ==la base reste dans un état correct même en cas d’erreur==.
        - Elle maintient l’intégrité des données (les règles sont respectées).
    3. **I**solation → ==pas d’interférence entre transactions==, les transactions simultanées
          ne se perturbent pas entre elles. 
        - Toute transaction doit s'exécuter comme si elle était la seule sur le système.
    4. **D**urabilité → une fois validée (commit), la transaction est définitivement enregistrée, même en cas de panne.

### Isolation
!!! note annotate ""

    - Le niveau d’isolation {++définit comment une transaction voit ou impacte les données modifiées par d’autres transactions concurrentes++}
    - L’isolation des transactions **détermine dans quelle mesure les modifications apportées à une transaction sont visibles dans d'autres transactions** et par d'autres utilisateurs du système.
        - Un niveau d'isolation **élevé** signifie que les modifications d'une transaction **ne sont pas visibles**
        - Un niveau d'isolation **faible** signifie que les modifications d'une transaction peuvent «se glisser» dans les sélections exécutées dans le cadre d'une autre transaction.

### Propagation
!!! note annotate ""

    - La propagation définit {++comment une méthode transactionnelle se comporte quand elle est appelée à l’intérieur d’une autre transaction++}.
    - C’est la capacité à maintenir l'intégrité des transactions lorsque plusieurs transactions sont exécutées simultanément 
    dans un contexte de transaction unique.


### Niveau d'isolation

!!! note annotate ""

    La norme SQL définit quatre niveaux d'isolation:

    - **READ_UNCOMMITTED**  →  Dirty read,  Non-repeatable read, Phantom read
    - **READ_COMMITTED** →  empêche dirty read, mais non-repeatable read possible.
    - **REPEATABLE_READ**  → empêche dirty read et non-repeatable read, mais phantom read possible.
    - **SERIALIZABLE** (le plus strict)
        - SERIALIZABLE: empêche les anomalies concurrentes (simule une exécution séquentielle).
        - SERIALIZABLE: **Simule une exécution séquentielle des transactions.**
    - Tous, sauf le niveau SERIALIZABLE, sont soumis à des anomalies de données

    ---
    - **Dirty read** → lorsqu’une transaction lit une donnée non validée par une autre transaction.
    - **Non-repeatable read** → Lorsqu’une transaction lit la même ligne mais obtient des résultats différents car une autre transaction a modifié/validé cette donnée entre-temps.
    - **Phantom read** → Lorsqu’une transaction lit un ensemble de données mais le résultat est différent car de nouvelles lignes apparaissent/disparaissent entre-temps.
    
    ---
    #### Qu’est-ce qu’un dirty read (lecture sale) ?
    - Un dirty read se produit lorsqu’une transaction lit une donnée qui a été modifiée par une autre transaction non encore validée (non commitée).
    - Si cette autre transaction fait un rollback, la première transaction aura utilisé une donnée invalide.
    
        > Exemple :
    
        > 1. T1 modifie le solde d’un compte (solde = 500 → 300), mais ne fait pas encore de commit.
    
        > 2. T2 lit le solde = 300.
    
        > 3. T1 fait rollback → le solde réel est toujours 500, mais T2 a pris une mauvaise décision en pensant que c’était 300.

    ---
    #### Non-repeatable read (lecture non reproductible)
    - Est un phénomène d’anomalie de concurrence qui se produit lorsqu’une transaction lit deux fois la même donnée, mais obtient des valeurs différentes entre les deux lectures — parce qu’une autre transaction l’a modifiée entre-temps.
    - Une transaction lit une donnée deux fois, mais obtient des résultats différents car une autre transaction a modifié/validé cette donnée entre-temps.

        > Exemple :

        > T1 lit le solde d’un compte = 500.

        > T2 modifie ce solde à 300 et fait **commit**.

        > T1 relit le même compte = 300.

        > Résultat : T1 a lu 500 puis 300 pour le même enregistrement, dans la même transaction.

### Hibernate-JPA

#### Hibernate
!!! note annotate "Hibernate"

    - Un framework ORM est conçu par Red Hat. 
    - Il a été initialement publié le 23 mai 2007.
    - Il prend en charge une JVM multiplateforme et est écrit en Java.
    ---
    - La principale caractéristique d'Hibernate est de ==mapper les classes Java aux tables de la base de données.==
    - L'avantage est clairement de masquer la logique relationnelle aux développeurs,
      d'interconnecter facilement des objets avec une base de données 'business' existante.
    - Quoi qu'il arrive il faut faire un pont entre le monde relationnel de la base de données et le monde objet de Java.
    - Fonctionnalités clés d'Hibernate :
        - Hibernate est une implémentation des directives JPA.
        - Il aide à ==mapper les types de données Java aux types de données SQL.==

#### JPA
!!! note annotate "JPA"

    - Il s'agit ^^d'une spécification Java^^ qui donne des fonctionnalités et des normes aux outils ORM. 
    - Un standard pour gérer la persistance dans Java
    - Il est utilisé pour examiner, contrôler et stocker les données entre les objets Java 
      et les bases de données relationnelles.

!!! note annotate "Différence entre JPA et Hibernate "

    La principale différence entre Hibernate et JPA est que Hibernate
    est un framework, tandis que JPA est une spécification d'API.<br/>
    Hibernate est une implémentation du JPA.
    
    | JPA           | Hibernate                                                                      |
    | ------------- |:-------------:                                                                 |
    | JPA est décrit dans le package **javax.persistence**.                                          | Hibernate est décrit dans le package **org.hibernate**. |
    | Il utilise (**JPQL**) pour exécuter des opérations de base de données.                         | Il utilise (**HQL**) pour exécuter des opérations de base de données.      |
    | il utilise l' interface **EntityManagerFactory** . Ainsi, cela donne un gestionnaire d'entité. | Pour créer des instances de Session, il utilise l' interface **SessionFactory** .  |
    | Pour créer, lire et supprimer des actions pour les instances de classes d'entités mappées, il utilise l' interface **EntityManager** | Pour créer, lire et supprimer des actions pour les instances de classes d'entités mappées, il utilise l' interface **Session** . _Il agit comme une interface d'exécution entre une application Java et Hibernate._     |

!!! note annotate "Quelle est la différence entre Session et EntityManager ?"

    - **EntityManager** est l’interface standard JPA.
    - **Session** est spécifique à Hibernate, avec plus de fonctionnalités.
    - Dans Spring, **EntityManager** est souvent encapsulé dans un **JpaRepository**. 

!!! note annotate "Cache d'entités vs Cache de requêtes"

    - Cache d’entités (1er ou second niveau) -> Stockage : Objets Hibernate (entités)
    - Cache de requêtes -> Stockage : Résultat d’une requête (liste d'objets)

!!! note annotate "Le cache d'entités JPA "

    - JPA mentionne la possibilité d’un cache, mais ne fournit pas d’implémentation concrète.

    ---

    1. **Cache de premier niveau (L1)** Le cache de premier niveau est rattaché à l'objet **EntityManager**, 
       il s'agit en fait du « persistence context » qui lui est associé.
    2. **Cache de deuxième niveau (L2)** En dessous de ce cache placé sous la direction des `EntityManagers`
       se trouve un autre cache dit de second niveau. ^^Ce cache est global à la JVM^^ 
       ou ^^plus exactement à l'**EntityManagerFactory**.
       Il peut aussi être configuré au niveau cluster, dans ce cas le cache sera répliqué sur chaque JVM.

    ---

    - Le cache de premier niveau (au niveau du persistence context / **EntityManager**) est obligatoire et toujours actif.
    - 1er niveau
        - Par `Session` ou `EntityManager`
            - Toujours actif, stocke les entités chargées pendant la transaction.
    - Le cache de second niveau (partagé entre sessions) est optionnel et dépend de l’implémentation de JPA utilisée.

    - 2e niveau
        - Partagé entre sessions `SessionFactory`
            - Permet de réutiliser les entités déjà lues depuis la base sans requête SQL.

    [https://www.docdoku.com/blog/2010/01/22/le-cache-dentites-jpa/](https://www.docdoku.com/blog/2010/01/22/le-cache-dentites-jpa/)

#### Performances

##### Hibernate

!!! note annotate "Comment optimiser les performances avec Hibernate ?"

    1. **Optimisation du cache**
        - Premier niveau (obligatoire, session) déjà utilisé par défaut par Hibernate.
            - Le cache de premier niveau est propre à la session et disparaît à sa fermeture. 
            - Hibernate garde les entités dans le cache de `session` (`transactionnel`).
            - [x] Le cache de premier niveau permet d'éviter les accès répétés à la même entité dans la même session.
        - Deuxième niveau (optionnel)
            - Active un cache partagé entre sessions
            - [x] Le cache de second niveau fournit une mémoire partagée pour les entités et collections ^^entre sessions^^,
                - Permet de réduire les lectures SQL 
                - Éviter des requêtes SQL répétitives et améliorant la performance globale.
    2. **FETCH JOIN** pour améliorer les performances d’Hibernate
        - Permet de charger les entités principales et leurs associations en une seule requête SQL, <br/>
          On évite ainsi le problème classique du N+1, où Hibernate exécute une requête par entité associée
        - Sans FETCH JOIN, Hibernate exécute une requête pour les entités principales, 
           puis une requête par entité associée. 
            - Avec FETCH JOIN, tout est chargé d’un coup. Moins de requêtes, donc meilleures performances.

    3. **Batch processing** ==Traiter en petits lots pour éviter la surcharge==
        - [x] Déf1: ^^Le batch processing^^, c’est le fait de traiter les opérations en lots — par exemple 50 insertions à la fois — 
           pour réduire le nombre d’aller-retours SQL et limiter la consommation mémoire.
        - Déf2: ^^Le batch processing^^ consiste à regrouper plusieurs opérations sur la base de données (insert, update, delete) 
          en un seul lot, au lieu d’exécuter une requête par entité.
        - Par exemple, avec Hibernate, on peut définir un `hibernate.jdbc.batch_size` et utiliser `flush() / clear()` 
          tous les X enregistrements pour éviter la surcharge mémoire.
        - J’ai déjà utilisé cette approche pour importer des milliers d’enregistrements sans saturer la JVM.
        - Objectif :
             - [x] Éviter l’OutOfMemoryError (ne pas tout charger en mémoire)
             - [x] Améliorer la performance et le débit global du traitement
             - [x] Réduire la charge sur la base de données et le réseau

    4. **Pagination**: ==Lire les données par pages==
        - La pagination consiste à récupérer les données d’une base par pages
        - Objectif :
            - [x] Limiter le nombre de lignes renvoyées par une requête SQL
    5. **Indexation**
        - Créer des index sur les colonnes fréquemment filtrées ou triées.
    6. **Projection**
        - Projection classique (liste d'objets Object[])
        - Projection vers un DTO (meilleure pratique)
        - Objectif :
            - [x] Seule la data nécessaire est chargée → économie mémoire
            - [x] Evite la surcharge du cache Hibernate
                - Les DTO ne vont pas dans le cache de premier ou second niveau, 
                  car ils ne sont pas des entités gérées par Hibernate.
                - => le cache reste léger, seule la mémoire nécessaire pour les DTO est utilisée.

##### Connection pooling

En plus d'optimiser le lazy loading, les fetch joins, et le cache, <br/>
utiliser un connection pool (HikariCP…) permet de ==réduire le coût de création des connexions==
et améliorer la performance globale de l’application

!!! note annotate "Connection pooling"

    - C'est une optimisation côté infrastructure et gestion des connexions à la base de données
    - Hibernate ne gère pas directement les connexions, 
      il s’appuie sur un `DataSource` ou `un pool de connexions` (HikariCP.. ).
    - Cela complète les optimisations Hibernate: même si tes requêtes sont optimisées,
      sans pool, chaque appel ouvre/ferme une connexion → perte de performance.

    _Principe :_

      - Établir une connexion à une base de données est une opération coûteuse (temps + ressources).
      - Au lieu de créer et fermer une connexion à chaque requête, on met en place ==un pool== {++(réservoir)++} 
        de connexions déjà ouvertes et prêtes à l’emploi.
      - Dans Spring Boot, l’outil **HikariCP** est une implémentation performante très utilisée.
    
    _But_ : Diminuer le temps de réponse et la charge serveur.

    _Fonctionnement :_

      - {++Lorsqu’une application a besoin d’accéder à la BDD, elle emprunte une connexion disponible dans le pool++}
      - Une fois la requête terminée, la connexion n’est pas détruite, mais rendue au pool pour être réutilisée.
      - Le pool peut gérer un nombre maximum de connexions pour éviter la surcharge.


### MySQL

#### JDBC - SQL - DBMS (SGBD)

!!! note annotate "Hibernate - JDBC - SQL - DBMS (SGBD)"

    - **SGBD** (Système de Gestion de Base de Données) ou **DBMS** (Database Management System)
        - Le SGBD est le ==logiciel qui stocke et gère les données==
          (gère physiquement les données) et exécute les requêtes SQL (un logiciel comme MySQL ou PostgreSQL).
        - Un ^^SGBD^^ doit avoir un modèle qui définit la manière dont les données sont organisées. 
    - **SQL**
        - Une ==API standard== pour les bases de données relationnelles.
        - Il s’agit d’un langage de programmation standardisé utilisé pour gérer les bases de données.
    - **JDBC** (Java Database Connectivity)
        - ==API Java== qui permet à une application Java de se connecter à un SGBD et d’exécuter des requêtes SQL.
            - Une API Java pour envoyer du SQL au SGBD.
        - Par rapport Hibernate 
            - C'est une API Java bas niveau pour interagir directement avec une base de données via des requêtes SQL.
            - Le développeur écrit le SQL et gère manuellement les connexions, transactions et mappages.
    - **Hibernate** (ORM)
        - ==Framework Java== qui automatise le mapping entre objets Java et tables SQL, 
           et utilise JDBC (API java) pour communiquer avec le SGBD (logiciel qui stocke et gère les données )

    !!! note annotate ""
    
        - **ORM** signifie **O**bject-**R**elational **M**apping (ou mappage objet-relationnel).
            - C’est ==une technique de programmation== qui permet de convertir les données 
              entre une base de données relationnelle et un langage de programmation orienté objet, comme Java.


#### Optimisation HikariCP avec MySQL
!!! note annotate "Performances… Optimisation HikariCP avec MySQL"

    - ^^Optimisation de la configuration de HikariCP^^
        - De nombreux paramètres de configuration de `HikariCP` peuvent impacter les performances globales du buffer, 
          notamment ceux liés à la gestion des connexions et au cache.
        - Augmenter le nombre maximum de connexions dans le pool de HikariCP permet de mieux gérer les demandes simultanées

    - ^^Optimisation de la base de données (MySQL)^^
        - Certaines configurations au niveau de la base de données peuvent aussi améliorer les performances 
          de HikariCP` en réduisant les zones de ralentissement au niveau de la gestion des connexions.
        - Augmenter la taille du pool de mémoire pour stocker plus de données en mémoire et réduire les accès disques, 
          ce qui peut accélérer les requêtes et la gestion des connexions.

    - ^^Utilisation des caches^^
        - Cache de requêtes : désactiver le cache de requêtes dans MySQL peut améliorer 
          les performances si vous avez des données en constante évolution, car les caches peuvent 
          devenir obsolètes rapidement.

    - ^^Optimisation du système^^
        - Mémoire et CPU:
            - Il est essentiel d'avoir suffisamment de mémoire et de ressources CPU pour 
              supporter un grand nombre de connexions simultanées.
            - Augmenter la capacité mémoire sur le serveur permet à HikariCP et 
              à la base de données de mieux gérer les connexions et les requêtes en cache.

#### Index SQL

!!! note annotate "Index SQL : Qu’est-ce que c’est ? À quoi ça sert ?"

    - ^^Un index SQL^^ permet de localiser rapidement les données recherchées dans une base de données relationnelle. 
      (localiser rapidement ce que l’on recherche).
    
    - Un index SQL est ==une structure de données== qui ^^accélère l’accès aux informations^^ dans une base de données relationnelle.
    - Sur le plan technique, ^^c’est une table supplémentaire^^ associée à la table principale dans la base de données. 
      Elle contient une ou plusieurs colonnes de la table principale, triées de manière spécifique.

!!! note annotate "Procédures stockées"

    - Les procédures stockées sont un ensemble d'instructions SQL compilées résidant dans la base de données


#### Questions

[https://www.mygreatlearning.com/blog/hibernate-interview-questions](https://www.mygreatlearning.com/blog/hibernate-interview-questions)

!!! note annotate ""

!!! note annotate "À quoi sert l’interface Transaction dans Hibernate"

    - ^^L’interface Transaction dans Hibernate^^ permet de gérer un ensemble d’opérations sur la base : 
      elle permet de démarrer, valider (commit) ou annuler (rollback) 
    - Hibernate fournit une interface `Transaction` qui encapsule la communication avec
      deux types de systèmes transactionnels : les transactions JDBC, et les transactions JTA (Java Transaction API)
        - Transactions JDBC
            - Transaction locale, liée à une connexion JDBC unique
            - Hibernate utilise la transaction JDBC sous-jacente pour commit/rollback..
        - Transactions JTA (Java Transaction API)
            - Transaction globale / distribuée,
            - Transactions JTA sont globales et peuvent coordonner plusieurs ressources 
              avec un commit distribué, garantissant la cohérence dans des environnements complexes.

!!! note annotate "Transaction - Hibernate VS Spring"

    - **Les transactions Hibernate** sont gérées manuellement via l’interface Transaction 
        pour contrôler commit et rollback.
        - Avec Hibernate, tu travailles avec `Session` et `Transaction`, et Hibernate 
          se charge de déléguer correctement le commit ou rollback au JDBC sous-jacent.
    - **Avec Spring**, `@Transactional` permet de gérer automatiquement les transactions, 
      avec en plus la propagation, l’isolation et le rollback sur exception, 
      et ce de façon indépendante de la technologie sous-jacente (JPA, Hibernate, JDBC…).

    - **Particularités**
        - **Propagation dans Hibernate**
            - Hibernate n’a pas de mécanisme de propagation intégré comme Spring.
            - La `propagation` se fait manuellement via la même Session et Transaction.
            - Dans Hibernate, la propagation des transactions doit être gérée manuellement : 
              plusieurs opérations peuvent partager la même transaction ou créer une transaction 
              indépendante via une nouvelle session.
        - **Isolation dans Hibernate**
            - Hibernate repose sur le SGBD pour gérer l’isolation.
            - Dépend du SGBD ou du niveau d’isolation de la connexion JDBC: Hibernate n’impose rien.
            - L’isolation des transactions dépend du SGBD ou de la configuration JDBC, 
              car Hibernate utilise les niveaux d’isolation fournis par la base de données.
    
                > TRANSACTION_READ_UNCOMMITTED

                > TRANSACTION_READ_COMMITTED ==(MySQL par défaut)==

                > TRANSACTION_REPEATABLE_READ

                > TRANSACTION_SERIALIZABLE
