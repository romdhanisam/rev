##### Notes

!!! note annotate "TCK"
___

- Line tck  

- // Objet prefixé Dc sont (sign courant continu)
- // si nn (courant alternative ac qq chose)

___
- Network
- xsd, identifiable 
- Load (une charge)
___
- Extensions  (des objets, comme identifiable)
- Variant ?
- active power      : P0 
- reactive power    : Q0 -- unité 'MVar' (volt-ampère réactif)
- voir fct d'import 
- ampl (à voir)
- ...
- TODO: add single line diagrams 
- https://powsybl.readthedocs.io/projects/powsybl-core/en/stable/grid_features/network_modifications.html
- TODO: insert a picture
- https://powsybl.readthedocs.io/projects/powsybl-core/en/stable/grid_features/import_post_processor.html
- TODO
- https://powsybl.readthedocs.io/projects/powsybl-core/en/latest/grid_exchange_formats/iidm/import.html#
- TODO
- https://powsybl.readthedocs.io/projects/powsybl-core/en/stable/grid_exchange_formats/cgmes/import.html#synchronousmachine


___
LoadFlow post-processor (config)
___
1. Grid exchange formats ()
2. IIDM api , TCK :: Network and subnetwork model
3. Merging networks, Imports, Detaching ...


### Grid Model

- Network: 
- VoltageLevel 
    - Line : connect 2 VoltageLevel (in same substation) or throught transformers (not same substation).
    - (kind: node/breaker or bus/breaker)
    - // the vertices (sommets)
        - node/breaker : is a graph structure (where vertice Node & edge Switches)
        - Nodes (transmission lines, two-winding transformers, …)
        - bus/breaker:  (vertice Buses, Switche can be defined between buses)
    - bus/breaker view bus/branch view
    //Lines can have loading limits.
- Area : collection of VoltageLevel
- Generator / Load
- Branch
- shunt 
- Switch (kind: breakers, disconnectors)
- transformers

---

- api interface :: Container (Network, Substation, VoltageLevel)
- api interface :: Identifiable (Area, .. Switch, Branch ...)
- api interface :: Connectable ()
- api interface :: Injection (Generator, Load)

---

- Voir la partie Simulation (ou sur /powsybl-tutorials)
=> https://powsybl.readthedocs.io/projects/powsybl-core/en/latest/simulation/index.html

> pypowsybl-notebooks

- https://github.com/powsybl/pypowsybl-notebooks
---
- iidm-api : HVDCLine
    - https://powsybl.readthedocs.io/projects/powsybl-core/en/stable/grid_model/network_subnetwork.html#hvdc-line
- Breaker/Switch : https://powsybl.readthedocs.io/projects/powsybl-core/en/stable/grid_model/network_subnetwork.html#breaker-switch
---
- setpoint: valeur de consigne.
- DC Ground 
- Line :
- Tie Line:  ligne d'interconnexion (de liaison)
- Dangling Line: ligne ouverte à une extrémité
-
- A Line is a Branch  (Branch is not a Line)
- Branch:: An equipment with two terminals. 
- Boundary (frontière) :? DOC il y a Area (parle du AreaBoundary) mais de notion de Boundary
___
- Bus → jeu de barres
- Un jeu de barres est un point de connexion électrique commun où se raccordent :
des lignes, 
- des transformateurs, 
- des générateurs, 
- Il sert à distribuer l'énergie électrique à plusieurs équipements.
des charges.
- A bus is a set of equipments connected together through a closed switch.
___
- Busbar section 
- A busbar section is a non impedant element used in a node/breaker substation topology to connect equipment.
____
- Busbar section vs Busbar
______
        VoltageLevel vl1 = s1.newVoltageLevel()
                .setId("VL1")
                .setNominalV(380)
                .setTopologyKind(TopologyKind.BUS_BREAKER)
                .add();
        Bus b1 = vl1.getBusBreakerView().newBus()
                .setId("B1")
                .add();


## Questions 
___
- VoltageLevelImpl  implements VoltageLevelExt  :: pk VoltageLevelExt et pas  VoltageLevel ?
- VoltageLevelImpl doit implement VoltageLevel et pas VoltageLevelExt.
___
- VoltageLevelExt.BusBreakerViewExt    **Ext dans le module impl ?
___
- TopologyKind It will be NODE_BREAKER or BUS_BREAKER depending on the level of detail of the CGMES grid model.
- La diff entre Topology NODE_BREAKER et BUS_BREAKER ?
___
- conform load vs a non-conform load:  ((vu dans cgmes :: https://powsybl.readthedocs.io/projects/powsybl-core/en/stable/grid_exchange_formats/cgmes/import.html#energyconsumer))
___
- dans cgmes / imports Documentation
- EnergyConsumer - EnergySource :: les deux modéliser comme LOAD (charge)
___
- Branch , Bus, (BusExt ).... voir sld 
- VoltageLevel  [ BusBreakerView   [ Bus ]  ]
- VoltageLevel  [ NodeBreakerView   [ Bus ]  ]
- VoltageLevel  [ BusView   [ Bus ]  ]
---
public interface Terminal {
    /**
     * A node/breaker view of the terminal.
     */
    public static interface NodeBreakerView {
___
- L'impédance est la grandeur électrique qui représente l'opposition d'un circuit au passage du courant.
---
- OpenRAO :: Open Remedial Actions Optimizer  (Optimiseur d'actions correctives, des parades)
- https://powsybl.readthedocs.io/projects/openrao/en/stable/
---
- https://github.com/powsybl/pypowsybl-notebooks
---
- public interface AreaBoundaryAdder {
---
interface qui extend identifiable vs interface n extend pas ... (exemple Area ..)
 == meme pour interface **Adder qui extend IdentifiableAdder et autre non ...
---
TODO
voir importer(s) & exporter(s) in iidm-api (Converter ausi)
importer , converter :: la meme chose
---
Les extensions dans iidm/iidm-extensions sont ** extends Extension<T> (import com.powsybl.commons.extensions.Extension;)
Les extensions dans 
