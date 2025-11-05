---
status: draft
---

## Kafka
!!! note annotate ""

    - Kafka est ^^une plateforme distribuée de données en continu^^, capable de publier, stocker, traiter 
      et souscrire à des flus d’enregistrements en temps réel.
    - Un système de messagerie distribué
    - Elle est conçue pour gérer des flux de données provenant de plusieurs sources et les fournir à plusieurs utilisateurs  
    - `Brokers` est le terme utilisé pour les serveurs, l’ensemble des brokers ayant comme but de construire un cluster.
    - Kafka a besoin d’un `cluster zookeeper` pour fonctionner, zookeeper pour maintenir la stabilité et l’intégralité du cluster Kafka
    - Kafka comprend
        - Réplication : topic les dupliquer sur plusieurs brokers (serveurs)
        - Partitionnement: topic soit segmenté et répartie sur plusieurs serveurs
    - Utilisé (data processing, centralisation de logs, métrics …)
    - pubsup: **pub**lish & **sub**scribe de messages
        - Structures modulaires (producteurs et consumers)


    - Kafka (Event-Driven Microservices using Spring Boot and Kafka)
    - https://www.redhat.com/fr/topics/integration/what-is-apache-kafka
    - https://www.javaguides.net/2022/07/event-driven-microservices-using-spring-boot-and-apache-kafka.html?spref=tw

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

