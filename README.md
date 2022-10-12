# iSTA-model-for-robotic-enabled-facility-inspection
This repository contains graph representations of an ontology model for using robots to implement facility inspection.

The model broadly categorizes facility inspection knowledge into three interconnected spheres, i.e., built environments “Scene”, inspection “Tasks”, and robotic “Agents”. 

1. Scene

We adopt the IFC (Industry Foundation Classes) schema, the most recognized knowledge formalization in the built environment, as the scene ontology. An open-source IFC2RDF converter (https://github.com/pipauwel/IFCtoRDF) is used to translate the original IFC schema to a knowledge graph format. The figure below shows the backbone structure of the IFC schema that is closely related to the inspection tasks in this study (e.g., fire door and lighting inspection). Of the many entities in IFC schema, IfcProduct is of the most interest for robotized inspection (the red boxes in below figure). Under the branch of IfcProduct, the abstract concepts about space (e.g., a floor, or a room) are represented by IfcSpatialStructureElement. This entity is highly relevant, as it will be used to describe the scope of inspection work so that suitable robots can be assigned, and related elements can be retrieved. IfcBuildingElement describes all elements participating in a building system such as walls (IfcWall) and doors (IfcDoor), which will be the entities to inspect in this study. As for the lighting system, we will search the IfcLightFixture for related lighting equipment. 
![image](https://user-images.githubusercontent.com/30916607/195350459-c4fcf422-a12c-4df4-b1b3-896548c261cc.png)

2. Task

As demonstrated by the figure below, a facility inspection task can be conceptualized into three interconnected entities. At the top level is the fmTask class, which divides facility inspection tasks into general categories such as the inspection of the fire resisting system, or the inspection of the lighting system. A fmTask can be broken down into multiple fmActivity, e.g., assignment of suitable robotic agents, path planning to navigate to target positions, and taking photos of elements being inspected. Different fmActivity are chained by the “isFollowedBy” property to indicate the implementation sequence. During the execution of an activity, there may be actions the robots need to implement in an ad hoc manner. For example, in the process of navigating to the inspection target, the robot needs to activate collision avoidance module when encountering unexpected obstacles. Such actions are represented by the adhocAction entity. All the fmTask, fmActivity and adhocAction are related to properties that define their specific attributes.  
![image](https://user-images.githubusercontent.com/30916607/195351366-d97ebd58-9cac-40d9-ad5b-c410bafd5840.png)

3. Agent

As shown by the below figure, this study extends existing robotic ontologies to meet the need of facility inspection. The Agent ontology is built upon CORA, the core ontology broadly encompassing main notions across the robotics and automation arena (https://github.com/srfiorini/IEEE1872-owl).
![image](https://user-images.githubusercontent.com/30916607/195351513-d33e1a20-ce6b-4c37-91ae-8ff534d0500d.png)

4. Integration of the scene, task, and agent model

The aforementioned ontologies are integrated into a unified knowledge model for automated facility inspection. The integration is achieved by reusing well-defined entities from one another. The following figure shows the identified entities that are used across ontologies and their connections. It can be observed that the iSTA-Task has borrowed several concepts related to robot agents and building elements/spaces from iSTA-Agent and iSTA-Scene. In the meantime, iSTA-Agent also reused entities (fmListOfCoor and IfcSpatialStructureElement) defined in its counterparts to describe robot position. To make sense of the indexed entities across ontologies, namespaces (or prefixes) of the origin ontologies need to be cited, e.g., the “core-bare” for Robot entity and the “ifc” for IfcSpatialStructureElement entity.
![image](https://user-images.githubusercontent.com/30916607/195352258-69d52c91-d1f5-46ac-bff0-884605a9fcdc.png)

Some of the knowledge graphs here are public robot ontologies from the community. They are:
- CORA and RPART: https://github.com/srfiorini/IEEE1872-owl
- Rosetta: https://github.com/jacekmalec/Rosetta_ontology
- IFCRDF: https://github.com/pipauwel/IFCtoRDF
