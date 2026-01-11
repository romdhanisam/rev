
!!! note annotate ""

    - Interrupteur 
    - Disjoncteur 
    - Sectionneur 
    - Commutateur


!!! note annotate ""

    Switch un équipement réseau qui relie plusieurs appareils (PC, automates, serveurs…)

!!! note annotate ""

    Pertes dans le réseau (par lignes, transformateur ...)
    //
    Contingency = panne ou événement imprévu

!!! note annotate ""

    Sensi :: Sensitivity analysis (analyse de sensibilité)
    :: Étude de l'impact d'une petite variation d'un paramètre sur une grandeur du réseau.

!!! note annotate ""

                 l
                 l
                 l
                 l
                 .  Disjoncteur
                 l
                 l
                 l
    =============.============

              Sectionneur

!!! note annotate ""
    
     1. [https://powsybl.readthedocs.io/projects/powsybl-core/en/latest/grid_model/network_subnetwork.html
     ](https://powsybl.readthedocs.io/projects/powsybl-core/en/latest/grid_model/network_subnetwork.html
     )    
     2. [https://powsybl.readthedocs.io/projects/powsybl-core/en/latest/grid_model/extensions.html#active-power-control
     ](https://powsybl.readthedocs.io/projects/powsybl-core/en/latest/grid_model/network_subnetwork.html
     )
!!! note annotate ""
    
    - Un générateur fournit deux types de puissance au réseau :
    - Active power (P) qui fait réellment le travail 
        - Fait tourner le moteur, 
        - Produire de la chaleur.
        - Lié à la fréquence du réseau
    - Reactive power (Q) MVAr :: volt-ampère réactif
        - Créer des champs magnétiques
        - Maintenir la tension
        - Lié au niveau de tension
    - P (active) → énergie consommée
    - Q (réactive) → énergie échangée (va-et-vient)

!!! note annotate ""

    Des fonctionnalitées comme:
    1. merge des network (la fusion)
    2. import 

!!! note annotate ""

   boundary elements  (éléments de frontière)

   - Bus : un noeud 
       - À un bus peuvent être connectés :
       - Générateurs
       - LOAD :: Charges (loads)
       - Lignes
       - Transformateurs
       - Disjoncteurs
   ---
   with one terminal, such as loads, generators



