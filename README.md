# Modelling the enslaved as historical persons

Rick Mourits, Thunnis van Oort, Kay Pepping, Pascal Konings, Britt van Duijvenvoorde

1. [Introduction](#1-introduction)
2. [Specification](#2-specification)
3. [Evaluation of the PiCo model](#3-evaluation-of-the-pico-model)
4. [Integration of existing schemas](#4-integration-of-existing-schemas)
   - [4.1. PiCo-M](#41-pico-m)
   - [4.2. Enslaved.org](#42-enslavedorg)
   - [4.3. Exploring Slave Trade in Asia (ESTA)](#43-exploring-slave-trade-in-asia-esta)
   - [4.4. Person Name Vocabulary](#44-person-name-vocabulary)
   - [4.5. Schema.org](#45-schemaorg)
   - [4.6. SlaveVoyages](#46-slavevoyages)
   - [4.7. WikiData](#47-WikiData)
   - [4.8. Required specialised classes](#48-required-specialised-classes)
   - [4.9. Required specialised properties](#49-required-specialised-properties)
   - [4.10. Taxonomies and thesauri](#410-taxonomies-and-thesauri)
5. [Exentensions of the PiCo model](#5-exentensions-of-the-PiCo-model)
   - [5.1. Enslavement status](#51-enslavement-status)
   - [5.2. Relation enslaved - enslaver](#52-relation-enslaved---enslaver)
   - [5.3. Relation enslaved - legal representative](#53-relation-enslaved---legal-representative)
   - [5.4. Relation owner - legal representative](#54-relation-owner---legal-representative)
   - [5.5. Plantations (and other organisations)](#55-plantations-and-other-organisations)
   - [5.6. Slave voyages](#56-slave-voyages)
   - [5.7. Group observations](#57-group-observations)
   - [5.8. Manumission](#58-manumission)

<br>

## 1. Introduction

In this document, we reflect on how to implement historical person data on enslaved people as Linked Data. Our aim is to use the [PiCo model](https://www.personsincontext.org) to fit all historical person observations by using the guidelines for flexible and extended reuse the model.

In order to effectively communicate (historical) person data, the [Dutch Center for Family History (CBG)](https://cbg.nl) has developed the Persons in Context (PiCo) model [(Woltjer et al., 2024)](https://doi.org/10.51964/hlcs19312), on the basis of the ROAR model developed by Menno den Engelse and Leon van Wissen [(2021)](https://www.leonvanwissen.nl/project/roar/). The PiCo model states how information on common factors in historical person observations, such as age, dates, occupations, relations between family members, roles in source documents, etc. should be described.

The PiCo model reuses as many existing URIs as possible to describe historical person data, as it encourages communities to give the same name to the same entity. This prevents discussions on naming and describing resources that have already been authoritatively defined. Moreover, this makes data more findable as people can search on one common term, rather than having to waste time on resolving a potentially endless list of variations. And, perhaps most importantly, it enforces stringent definitions of properties and resources that can be used for efficient knowledge interference.

<br>

## 2. Specifications
- Persons are modelled as standardised in the Persons in Context model (PiCo-M)
- Where possible, extensions to the model are based on existing vocabularies
- Extensions to the model follow the logic of concentric description: where possible global (Schema.org), otherwise domain-specific (Enslaved.org), or specialised (Person Name Vocabulary)
- New extensions can be introduced with consensus between the HDSC, Globalised, and ESTA
- The model should be easily transposable to the Enslaved.org data model

<br>

## 3. Evaluation of the PiCo model
During three meetings in Q1 2025, we identified the following issues in implementing PiCo-M for historical person data on slave history:

|  | Issue | Description	  |
|--|-------|----------------|
| 1. | [PiCo-M](#41-pico-m) | A basic descriptive model is necessary to describe observations and reconstructions of enslaved persons |
| 2. | Age categories<sup>[1](#41-pico-m),[2](#42-enslavedorg)</sup> | It is not uncommon that person observations of enslaved persons only contain an age category (child vs adult) instead of an exact age  |
| 3. | [Enumerations](#41-pico-m) | Certain sources contain (only) information about groups of enslaved persons as part of an enumeration |
| 4. | [Name changes](#41-pico-m) | Emancipation and manumission records refer to one event, but these records contain two observations for the same (enslaved and free) person |
| 5. | [Observation or reconstruction](#41-pico-m) | The distinction between person observations and person reconstructions is not always clear with old data, as the preserved datasets are an undocumented mix of original and enriched data |
| 6. | [Person names](#44-person-name-vocabulary) | Person names can contain African names, Christian names, and person descriptions |
| 7. | [Person status](#42-enslavedorg) | There is no property to describe whether someone is enslaved or free |
| 8. | [Reasons for observation](#42-enslavedorg) | Enslavement, emancipation, manumission, and trade are necessary to model the start and/or end of observations |
| 9. | Relations<sup>[1](#42-enslavedorg),[2](#49-required-specialised-properties)</sup> | There are currently no properties to describe relationships between <br> - slaveholder and enslaved, <br> - freed persons and ["straatvoogden"](https://www.nationaalarchief.nl/onderzoeken/zoekhulpen/suriname-vrijgelaten-slaven-manumissies-1832-1863), or <br> - slave owners and their legal representative. The latter group includes women who are legally represented by their husband, also known as nomine uxoris |
| 10. | Slaveholders<sup>[1](#45-schemaorg),[2](#47-wikidata)</sup> | Slaveholders are not always persons, but can also be organisations (mainly plantations, but also other) |
| 11. | Slave voyages<sup>[1](#45-schemaorg),[2](#43-exploring-slave-trade-in-asia-esta),[3](#46-slavevoyages),[4](#48-required-specialised-classes)</sup>  | Ships are required to model slave voyages |
| 12. | Social categories<sup>[1](#42-enslavedorg),[2](#49-required-specialised-properties)</sup> | Scholars have collected extensive lists of data related to slavery, such as plantations in Suriname or an overview of all religions. These need to be shared durably |
| 13. | Taxonomies and Thesauri<sup>[1](#47-wikidata),[2](#410-taxonomies-and-thesauri)</sup> | Person observations often contain social categories related to race, class, or religion |
| 14. | [Toponyms](#44-person-name-vocabulary) | Person names of enslaved often contain a toponym with which they have an association. The exact meaning is ambiguous, but the association with the place is, for example, required to reconstruct persons |
| 15. | [Type of enslavement](#42-enslavedorg) | There is no property to describe the type of enslavement |

<br>

## 4. Integration of existing schemas

For each of these issues, we checked whether solutions were available in the Persons in Context model, Enslaved.org, Person Name Vocabulary, Schema.org, and SlaveVoyages.net. For each of these solutions we evaluated the viability for reuse in and presented our outcomes in Q1 and Q2 2025.

### 4.1. PiCo-M

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 1. | PiCo-M | The logic of the Persons in Context model is easily applicable to data on enslaved persons | **yes** |
| 2. | Age categories | hasAge is used to mention ages. However, the user expects an exact age <br> _**We suggest not to use hasAge to refer to age categories**_ | **no** |
| 3. | Enumerations | Each individual in the enumeration can be modelled as an enslaved with the PiCo or extended characteristics | **yes** |
| 4. | Name changes | An emancipation or manumission record should be seen as two observations: one of an enslaved person until emancipation/manumission, and another of a free person from emancipation/manumission. These two observations can be joint with a personReconstruction. | **yes** |
| 5. | Observation or reconstruction | Person observations are meant to model a record and stay close to the source. Person reconstructions combines information and allows for interpretation. <br> _**In case the relation to the source is lost, and records probably contain interpretation by the data provider, we suggest to use person reconstructions**_ | **yes** |


### 4.2. Enslaved.org

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 2. | Age categories | [_hasAgeCategory_](https://lod.enslaved.org/wiki/Property:P4) is used to model age groups. This property has four categories: [_Infant Age Group_](https://lod.enslaved.org/wiki/Q426), [_Child Age Group_](https://lod.enslaved.org/wiki/Q427), [_Adult Age Group_](https://lod.enslaved.org/wiki/Q425), and [_Older Person Age Group_](https://lod.enslaved.org/wiki/Q429) |  **yes** | 
| 7. | Person status | [_hasPersonStatus_](https://lod.enslaved.org/wiki/Property:P33) is used to model person status. This property has seven categories: [_Enslaved Person_](https://lod.enslaved.org/wiki/Q109), [_Free Person_](https://lod.enslaved.org/wiki/Q117), [_Freed Person_](https://lod.enslaved.org/wiki/Q386), [_Indentured Person or Pawn_](https://lod.enslaved.org/wiki/Q166), [_Enslaver or Owner_](https://lod.enslaved.org/wiki/Q112), [_Liberated African_](https://lod.enslaved.org/wiki/Q159275), [_Liminal Status Person_](https://lod.enslaved.org/wiki/Q192). This category is too specific to be broadly used, and too broad to be used specifically. <br> _**We suggest to use the property and three concepts: [_Enslaved Person_](https://lod.enslaved.org/wiki/Q109), [_Free Person_](https://lod.enslaved.org/wiki/Q117), [_Liminal Status Person_](https://lod.enslaved.org/wiki/Q192)**_ | **yes** |
| 8. | Reasons for observations | [_hasEventType_](https://lod.enslaved.org/wiki/Property:P30) contains 27 events: [_Advertisement_](https://lod.enslaved.org/wiki/Q907443), [_Appraisal_](https://lod.enslaved.org/wiki/Q647904), [_Baptism or Naming Ceremony_](https://lod.enslaved.org/wiki/Q149), [_Birth_](https://lod.enslaved.org/wiki/Q147), _Burial or Interment_, [_Death_](https://lod.enslaved.org/wiki/Q148), [_Disappearance_](https://lod.enslaved.org/wiki/Q154), [_Disembarkation_](https://lod.enslaved.org/wiki/Q10088), _Education_, [_Emancipation or Manumission_](https://lod.enslaved.org/wiki/Q281), [_Embarkation_](https://lod.enslaved.org/wiki/Q10087), [_Employment, Apprenticeship, or Indenture_](https://lod.enslaved.org/wiki/Q156), [_Enslavement_](https://lod.enslaved.org/wiki/Q151), [_Legal Proceeding_](https://lod.enslaved.org/wiki/Q155), [_Marriage_](https://lod.enslaved.org/wiki/Q150), [_Membership_](https://lod.enslaved.org/wiki/Q473), [_Mention_](https://lod.enslaved.org/wiki/Q856060), [_Military Service_](https://lod.enslaved.org/wiki/Q164), [_Mortgage_](https://lod.enslaved.org/wiki/Q298746), [_Narrative_](https://lod.enslaved.org/wiki/Q157), [_Resistance or Rebellion_](https://lod.enslaved.org/wiki/Q357), [_Registration_](https://lod.enslaved.org/wiki/Q250), [_Relocation_](https://lod.enslaved.org/wiki/Q161), [_Residence_](https://lod.enslaved.org/wiki/Q159), [_Sale or Transfer_](https://lod.enslaved.org/wiki/Q153), [_Trade_](https://lod.enslaved.org/wiki/Q1147583), [_Voyage_](https://lod.enslaved.org/wiki/Q146). These events can be used to indicate to indicate why observation started and ended | **yes** |
| 9. | Relations | Relations are modelled as a concept with its own entities. This approach is incongruent with the PiCo model that uses properties to directly relate two people. | **no** |
| 12. | Social Categories | [_hasRaceorColor_](https://lod.enslaved.org/wiki/Property:P32) is used to model racial characteristics. This variable causes discussions as social categories can also be based on religion, caste, class, etc. | **no** |
| 15. | Type of enslavement | [_hasPersonStatus_](https://lod.enslaved.org/wiki/Property:P33) can be used to model the type of enslavement. However, the seven categories: [_Enslaved Person_](https://lod.enslaved.org/wiki/Q109), [_Free Person_](https://lod.enslaved.org/wiki/Q117), [_Freed Person_](https://lod.enslaved.org/wiki/Q386), [_Indentured Person or Pawn_](https://lod.enslaved.org/wiki/Q166), [_Enslaver or Owner_](https://lod.enslaved.org/wiki/Q112), [_Liberated African_](https://lod.enslaved.org/wiki/Q159275), [_Liminal Status Person_](https://lod.enslaved.org/wiki/Q192) are too specific to be broadly used, and too broad to be used specifically | **yes** |


### 4.3. Exploring Slave Trade in Asia (ESTA)

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 11. | Slave voyages | Modelling ships is the bread and butter of SlaveVoyages.net and ESTA. We should aim for interoperability with their frameworks. This can easily be managed with [_sdo:TransferAction_](https://schema.org/TransferAction) | **MainVoyage** <br> **SubVoyage** |


### 4.4. Person Name Vocabulary

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 6. | Person names | Person names can contain African names, Christian names, and person descriptions. These can be modelled with [_nameSpecification_](https://www.lodewijkpetram.nl/vocab/pnv/doc/#nameSpecification) | **yes** |
| 14. | Toponyms | For ontologies, we need an easy way to extract place information from names. We will use examples to ask pnv for an extension of the model. (Update 2025/04/17: PNV is willing to extend if we provide them with a proposal for this property.) | **willing to extend** |


### 4.5. Schema.org

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 10. | Slaveholders | [_Organization_](https://schema.org/Organization) is a type in Schema.org with relevant properties like [_owns_](https://schema.org/owns), [_employee_](https://schema.org/employee), [_founder_](https://schema.org/founder), [_funder_](https://schema.org/funder), [_member_](https://schema.org/member). These properties can be made reflexive with [_affiliation_](https://schema.org/affiliation) | **yes** |
| 11. | Slave voyages | Modelling ships is the bread and butter of SlaveVoyages.net and ESTA. We should aim for interoperability with their frameworks. This can easily be managed with [_sdo:TransferAction_](https://schema.org/TransferAction) 


### 4.6. SlaveVoyages

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 11. | Slave voyages | Modelling ships is the bread and butter of SlaveVoyages.net and ESTA. We should aim for interoperability with their frameworks. This can easily be managed with [_sdo:TransferAction_](https://schema.org/TransferAction) | **in contact** |


### 4.7. WikiData
|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 10. | Slaveholders | WikiData can be used to specify the type of organization, and give a definiton of that organization. For example a [_plantation_](https://www.wikidata.org/entity/Q188913) | **yes** |
| 13. | Taxonomies and Thesauri | Thesauri should only be used if they are part of a curated collection, as this ascertain the long-term availability and stability of collections. This makes WikiData unsuited for hosting thesauri | **no** |


### 4.8. Required specialised classes
|  | Issue | Description	  | class | 
|--|-------|----------------|-------|
| 11. | Slave voyages | Modelling ships is the bread and butter of SlaveVoyages.net and ESTA. We should aim for interoperability with their frameworks. This can easily be managed with [_sdo:TransferAction_](https://schema.org/TransferAction) | **MainVoyage** <br> **SubVoyage** |


### 4.9. Required specialised properties
|  | Issue | Description	  | property | 
|--|-------|----------------|----------|
| 9. | Relations |  | **isEnslavedBy** <br> **isEnslaverOf** <br> **isLegallyRepresentedBy** <br> **legallyRepresents** |
| 11. | Slave voyages |  | **slaveVoyage** |
| 12. | Social categories |  | **hasSocialIdentity** |


### 4.10. Taxonomies and thesauri
|  | Issue | Description	  | property | 
|--|-------|----------------|----------|
| 13. | Taxonomies and Thesauri | Person observations often contain social categories related to race, class, or religion |

<br>

## 5. Exentensions of the PiCo model
Based on the [Evaluation of the PiCo model](#evaluation-of-the-pico-model), we made the following extensions to the PiCo model. These extensions were discussed in Q2 2025 and presented at the DH Benelux in June.


### 5.1. Enslavement status
Both enslaved and free persons can be modelled as picom:PersonObservations. We use the Enslaved.org property for hasPersonStatus [ed:P33](https://lod.enslaved.org/wiki/Property:P33) to note which persons are Enslaved [ed:Q109](https://lod.enslaved.org/wiki/Q109). 

| Object | Property | Object |
|----|----|----|
| hdsc:enslaved1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; |
| | [ed:P33](https://lod.enslaved.org/wiki/Property:P33) | [ed:Q109](https://lod.enslaved.org/wiki/Q109) . |


### 5.2. Relation enslaved - enslaver
We use the properties isEnslavedBy and isEnslaverOf to model the relationship between enslaver and enslaved. In its simplest form, this would result in the following triples.

| Object | Property | Object |
|----|----|----|
| hdsc:Enslaved1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; |
| | [ed:P33](https://lod.enslaved.org/wiki/Property:P33) | [ed:Q109](https://lod.enslaved.org/wiki/Q109) ; |
| | XXX:isEnslavedBy | hdsc:Owner1 . |
| hdsc:Enslaved2 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; |
| | [ed:P33](https://lod.enslaved.org/wiki/Property:P33) | [ed:Q109](https://lod.enslaved.org/wiki/Q109) ; |
| | XXX:isEnslavedBy | hdsc:Owner1 . |
| hdsc:Owner1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; |
| | XXX:isEnslaverOf | hdsc:Enslaved1, hdsc:Enslaved2 . |

However, we advise to also add the beginning and end date of the observed enslaved relations with a blank node using [sdo:startDate](https://schema.org/startDate) and [sdo:endDate](https://schema.org/endDate), as slavery relations can change over time. 

| Subject | Property | Object | Property Blank Node | Object Blank Node |
|----|----|----|----|----|
| hdsc:Enslaved1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; | | |
| | [ed:P33](https://lod.enslaved.org/wiki/Property:P33) | [ed:Q109](https://lod.enslaved.org/wiki/Q109) ; | | |
| | XXX:isEnslavedBy | [ | [rdf:value](http://www.w3.org/1999/02/22-rdf-syntax-ns#value) | hdsc:Owner1 ; |
| | | | [sdo:startDate](https://schema.org/startDate) | "1837-08-15"^^xsd:date ; |
| | | | [sdo:endDate](https://schema.org/endDate) | "1838"^^xsd:gYear ; |
| | | ] . | | |
| hdsc:Enslaved2 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; | | |
| | [ed:P33](https://lod.enslaved.org/wiki/Property:P33) | [ed:Q109](https://lod.enslaved.org/wiki/Q109) ; | | |
| | XXX:isEnslavedBy | [ | [rdf:value](http://www.w3.org/1999/02/22-rdf-syntax-ns#value) | hdsc:Owner1 ; |
| | | | [sdo:startDate](https://schema.org/startDate) | "1837-08-16"^^xsd:date ; |
| | | | [sdo:endDate](https://schema.org/endDate) | "1838"^^xsd:gYear ; |
| | | ] . | | |
| hdsc:Owner1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; | | |
| | XXX:isEnslaverOf | [ | [rdf:value](http://www.w3.org/1999/02/22-rdf-syntax-ns#value) | hdsc:Enslaved1 ; |
| | | | [sdo:startDate](https://schema.org/startDate) | "1837-08-15"^^xsd:date ; |
| | | | [sdo:endDate](https://schema.org/endDate) | "1838"^^xsd:gYear ; |
| | | ] ; | | |
| | XXX:isEnslaverOf | [ | [rdf:value](http://www.w3.org/1999/02/22-rdf-syntax-ns#value) | hdsc:Enslaved2 ; |
| | | | [sdo:startDate](https://schema.org/startDate) | "1837-08-16"^^xsd:date ; |
| | | | [sdo:endDate](https://schema.org/endDate) | "1838"^^xsd:gYear ; |
| | | ] . | | |

We also describe the start and end date of person observations using [sdo:startDate](https://schema.org/startDate) and [sdo:endDate](https://schema.org/endDate). These receive the Enslaved.org property for [hasEventType](https://lod.enslaved.org/wiki/Property:P30) and any of the associated concepts as a blank node: [_Advertisement_](https://lod.enslaved.org/wiki/Q907443), [_Appraisal_](https://lod.enslaved.org/wiki/Q647904), [_Baptism or Naming Ceremony_](https://lod.enslaved.org/wiki/Q149), [_Birth_](https://lod.enslaved.org/wiki/Q147), _Burial or Interment_, [_Death_](https://lod.enslaved.org/wiki/Q148), [_Disappearance_](https://lod.enslaved.org/wiki/Q154), [_Disembarkation_](https://lod.enslaved.org/wiki/Q10088), _Education_, [_Emancipation or Manumission_](https://lod.enslaved.org/wiki/Q281), [_Embarkation_](https://lod.enslaved.org/wiki/Q10087), [_Employment, Apprenticeship, or Indenture_](https://lod.enslaved.org/wiki/Q156), [_Enslavement_](https://lod.enslaved.org/wiki/Q151), [_Legal Proceeding_](https://lod.enslaved.org/wiki/Q155), [_Marriage_](https://lod.enslaved.org/wiki/Q150), [_Membership_](https://lod.enslaved.org/wiki/Q473), [_Mention_](https://lod.enslaved.org/wiki/Q856060), [_Military Service_](https://lod.enslaved.org/wiki/Q164), [_Mortgage_](https://lod.enslaved.org/wiki/Q298746), [_Narrative_](https://lod.enslaved.org/wiki/Q157), [_Resistance or Rebellion_](https://lod.enslaved.org/wiki/Q357), [_Registration_](https://lod.enslaved.org/wiki/Q250), [_Relocation_](https://lod.enslaved.org/wiki/Q161), [_Residence_](https://lod.enslaved.org/wiki/Q159), [_Sale or Transfer_](https://lod.enslaved.org/wiki/Q153), [_Trade_](https://lod.enslaved.org/wiki/Q1147583), [_Voyage_](https://lod.enslaved.org/wiki/Q146).

| Subject | Property | Object | Property Blank Node | Object Blank Node |
|----|----|----|----|----|
| hdsc:enslaved1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; | | |
| | [ed:P33](https://lod.enslaved.org/wiki/Property:P33) | [ed:Q109](https://lod.enslaved.org/wiki/Q109) ; | | |
| | XXX:isEnslavedBy | [ | [rdf:value](http://www.w3.org/1999/02/22-rdf-syntax-ns#value) | hdsc:owner1 ; |
| | | | [sdo:startDate](https://schema.org/startDate) | "1837-08-15"^^xsd:date ; |
| | | | [sdo:endDate](https://schema.org/endDate) | "1838"^^xsd:gYear ; |
| | | ] ; | | |
| | [sdo:startDate](https://schema.org/startDate) | [ | [rdf:value](http://www.w3.org/1999/02/22-rdf-syntax-ns#value) | "1837-08-15"^^xsd:date ; |
| | | | [ed:P30](https://lod.enslaved.org/wiki/Property:P30) | [ed:Q153](https://lod.enslaved.org/wiki/Q153) |
| | | ] ; | | |
| | [sdo:endDate](https://schema.org/endDate) | [ | [rdf:value](http://www.w3.org/1999/02/22-rdf-syntax-ns#value) | "1838"^^xsd:gYear ; |
| | | | [ed:P30](https://lod.enslaved.org/wiki/Property:P30) | [ed:Q250](https://lod.enslaved.org/wiki/Q153) |
| | | ] . | | |

  
### 5.3. Relation enslaved - legal representative
Enslaved and manumitted persons can receive a <i>straatvoogd</i> who represents them in the years after slavery. This can by modelled with the properties legallyRepresents and legallyRepresentedBy.

| Object | Property | Object |
|----|----|----|
| hdsc:Freedperson1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; |
| | [ed:P33](https://lod.enslaved.org/wiki/Property:P33) | [ed:Q386](https://lod.enslaved.org/wiki/Q386) ; |
| | XXX:legallyRepresentedBy | hdsc:Intermediary1 . |
| hdsc:Intermediary1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; |
| | XXX:legallyRepresents | hdsc:Freedperson1 . |

We advise to also add the beginning and end date of the observed enslaved relations with a blank node using sdo:startDate and sdo:endDate, as legal representation can change over time.

| Object | Property | Object | Property Blank Node | Object Blank Node |
|----|----|----|----|----|
| hdsc:Freedperson1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; | | |
| | [ed:P33](https://lod.enslaved.org/wiki/Property:P33) | [ed:Q386](https://lod.enslaved.org/wiki/Q386) ; | | |
| | XXX:legallyRepresentedBy | [ | [rdf:value](http://www.w3.org/1999/02/22-rdf-syntax-ns#value) | hdsc:Intermediary1 ; |
| | | | [sdo:startDate](https://schema.org/startDate) | "1848"^^xsd:gYear ; |
| | | | [sdo:endDate](https://schema.org/endDate) | "1851"^^xsd:gYear ; |
| | | ] . | | |
| hdsc:Intermediary1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; | | |
| | XXX:legallyRepresents | [ | [rdf:value](http://www.w3.org/1999/02/22-rdf-syntax-ns#value) | hdsc:Freedperson1 ; |
| | | | [sdo:startDate](https://schema.org/startDate) | "1848"^^xsd:gYear ; |
| | | | [sdo:endDate](https://schema.org/endDate) | "1851"^^xsd:gYear ; |
| | | ] . | | |


### 5.4. Relation owner - legal representative
Owners are sometimes represented by an intermediary or by their spouse. This is modelled with the properties legallyRepresents and legallyRepresentedBy.

| Object | Property | Object |
|----|----|----|
| hdsc:Owner1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; |
| | [sdo:gender](https://schema.org/gender) | [sdo:Female](https://schema.org/Female) |
| | [sdo:spouse](https://schema.org/spouse) | hdsc:Intermediary1 ; |
| | XXX:legallyRepresentedBy | hdsc:Intermediary1 . |
| hdsc:Intermediary1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; |
| | [sdo:gender](https://schema.org/gender) | [sdo:Male](https://schema.org/Male) |
| | [sdo:spouse](https://schema.org/spouse) | hdsc:Owner1 ; |
| | XXX:legallyRepresents | hdsc:Owner1 . |

We advise to also add the beginning and end date of the observed enslaved relations with a blank node using sdo:startDate and sdo:endDate, as legal representation can change over time.

| Object | Property | Object | Property Blank Node | Object Blank Node |
|----|----|----|----|----|
| hdsc:Owner1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; | | |
| | [sdo:gender](https://schema.org/gender) | [sdo:Female](https://schema.org/Female) | | |
| | [ed:P33](https://lod.enslaved.org/wiki/Property:P33) | [ed:Q386](https://lod.enslaved.org/wiki/Q386) ; | | |
| | [sdo:spouse](https://schema.org/spouse) | [ | [rdf:value](http://www.w3.org/1999/02/22-rdf-syntax-ns#value) | hdsc:Intermediary1 ; |
| | | | [sdo:startDate](https://schema.org/startDate) | "1848"^^xsd:gYear ; |
| | | | [sdo:endDate](https://schema.org/endDate) | "1851"^^xsd:gYear ; |
| | | ] ; | | |
| | XXX:legallyRepresentedBy | [ | [rdf:value](http://www.w3.org/1999/02/22-rdf-syntax-ns#value) | hdsc:Intermediary1 ; |
| | | | [sdo:startDate](https://schema.org/startDate) | "1848"^^xsd:gYear ; |
| | | | [sdo:endDate](https://schema.org/endDate) | "1851"^^xsd:gYear ; |
| | | ] . | | |
| hdsc:Intermediary1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; | | |
| | [sdo:gender](https://schema.org/gender) | [sdo:Male](https://schema.org/Male) | | |
| | [sdo:spouse](https://schema.org/spouse) | [ | [rdf:value](http://www.w3.org/1999/02/22-rdf-syntax-ns#value) | hdsc:Owner1 ; |
| | | | [sdo:startDate](https://schema.org/startDate) | "1848"^^xsd:gYear ; |
| | | | [sdo:endDate](https://schema.org/endDate) | "1851"^^xsd:gYear ; |
| | | ] ; | | |
| | XXX:legallyRepresents | [ | [rdf:value](http://www.w3.org/1999/02/22-rdf-syntax-ns#value) | hdsc:Owner1 ; |
| | | | [sdo:startDate](https://schema.org/startDate) | "1848"^^xsd:gYear ; |
| | | | [sdo:endDate](https://schema.org/endDate) | "1851"^^xsd:gYear ; |
| | | ] . | | |



### 5.5. Plantations (and other organisations)

| Object | Property | Object |
|----|----|----|
| hdsc:Organization1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [sdo:Organization](https://schema.org/Organization) |
| | [sdo:additionalType](https://schema.org/additionalType) | [wdt:Q188913](https://wikidata.org/entity/Q188913) ; |
| | [sdo:name](https://schema.org/name) | "Voorbeeld" ; |
| | [sdo:affiliation](https://schema.org/affiliation) | hdsc:Person1 ; |
| | [sdo:affiliation](https://schema.org/affiliation) | hdsc:Person2 ; |
| | [sdo:affiliation](https://schema.org/affiliation) | hdsc:Person3 ; |
| | XXX:isEnslaverOf | hdsc:Person4 . |
| hdsc:Person1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; |
| | [sdo:affiliation](https://schema.org/affiliation) | hdsc:Organization1 ; |
| | [sdo:owns](https://schema.org/owns) | hdsc:Organization1 . |
| hdsc:Person2 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; |
| | [sdo:affiliation](https://schema.org/affiliation) | hdsc:Organization1 ; |
| | [sdo:funder](https://schema.org/funder) | hdsc:Organization1 . |
| hdsc:Person3 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; |
| | [sdo:affiliation](https://schema.org/affiliation) | hdsc:Organization1 ; |
| | [sdo:employee](https://schema.org/employee) | hdsc:Organization1 . |
| hdsc:Person4 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; |
| | [ed:P33](https://lod.enslaved.org/wiki/Property:P33) | [ed:Q109](https://lod.enslaved.org/wiki/Q109) ; |
| | hdsc:isEnslavedBy | hdsc:Organization1 . |


### 5.6. Slave voyages
| Object | Property | Object |
|----|----|----|
| esta:Voyage1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | XXX:MainVoyage, [sdo:TransferAction](https://schema.org/TransferAction) . |
| esta:Voyage1a | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | XXX:SubVoyage, [sdo:TransferAction](https://schema.org/TransferAction) ; |
| | [sdo:memberOf](sdo:memberOf) | esta:Voyage1 ; |
| | [sdo:startDate](sdo:startDate) | "1824-06-10"^^xsd:date ; |
| | [sdo:startLocation](sdo:startLocation) | "Manilla" ; |
| | [sdo:endDate](sdo:endDate) | "1824-07-11"^^xsd:date ; |
| | [sdo:toLocation](sdo:toLocation) | "Antananarivo" . |




### 5.7. Manumission


### 5.8. Group observations


