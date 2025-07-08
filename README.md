# Modelling the enslaved as historical persons

Rick Mourits, Thunnis van Oort, Kay Pepping, Pascal Konings, Britt van Duijvenvoorde

- [Introduction](#introduction)
- [Specification](#specification)
- [Evaluation of the PiCo model](#evaluation-of-the-pico-model)
  - [PiCo-M](#pico-m)
  - [Enslaved.org](#enslave.org)
  - [Exploring Slave Trade in Asia (ESTA)](#exploring-slave-trade-in-asia-esta)
  - [Person Name Vocabulary](#person-name-vocabulary)
  - [Schema.org](#schema.org)
  - [SlaveVoyages.net](#slavevoyages.net)
  - [WikiData](#WikiData)
  - [Required specialised classes](#required-specialised-classes)
  - [Required specialised properties](#required-specialised-properties)
- [Exentensions of the PiCo model](#exentensions-of-the-PiCo-model)
- [Taxonomies and thesauri](#taxonomies-and-thesauri)
  - [Enslavement status](#enslavement-status)
  - [Relation enslaved - enslaver](#relation-enslaved---enslaver)
  - [Relation enslaved - legal representative](#relation-enslaved---legal-representative)
  - [Relation owner - legal representative](#relation-owner---legal-representative)
  - [Plantations (and other organisations)](#plantations-and-other-organisations)
  - [Slave voyages](#slave-voyages)
  - [Group observations](#group-observations)
  - [Manumission](#manumission)


## Introduction

In this document, we reflect on how to implement historical person data on enslaved people as Linked Data. Our aim is to use the [PiCo model](https://www.personsincontext.org) to fit all historical person observations  and to provide flexibility and guidelines for extending the model.

The PiCo model states how information on common factors in historical person observations, such as age, dates of birth, marriage, and death, occupations, relations between family members, roles in source documents, etc. should be described. In order to effectively communicate (historical) person data, the Dutch Center for Family History (CBG) has developed the Persons in Context (PiCo) model (Woltjer et al., 2024), on the basis of the ROAR model developed by Menno den Engelse and Leon van Wissen (2021). 

The PiCo model reuses as many existing URIs as possible to describe historical person data, as it encourages communities to give the same name to the same entity. This prevents discussions on naming and describing resources that have already been authoritatively defined, such as birth dates or names. Moreover, this makes data more findable as people can search on one common term, rather than having to waste time on resolving a potentially endless list of variations in modelling the same concept. And, perhaps even more importantly, it also enforces stringent definitions of properties and resources that can be used for efficient knowledge interfering

## Specifications
- Persons are modelled as standardised in the Persons in Context model (PiCo-M)
- Where possible, extensions to the model are based on existing vocabularies
- Extensions to the model follow the logic of concentric description: where possible global (Schema.org), otherwise domain-specific (Enslaved.org), or specialised (Person Name Vocabulary)
- New extensions can be introduced with consensus between the HDSC, Globalised, and ESTA
- The model should be easily transposable to the Enslaved.org data model

## Evaluation of the PiCo model
During three meetings in Q1 2025, we identified the following issues in implementing PiCo-M for historical person data on slave history:


|  | Issue | Description	  |
|--|-------|----------------|
| 1. | [PiCo-M](#pico-m) | The logic of the Persons in Context model is easily applicable to data on enslaved persons |
| 2. | Age categories<sup>[1](#pico-m),[2](#enslaved.org)</sup> | Person observations sometimes only state an age category (child vs adult) rather than the exact age  |
| 3. | [Enumerations](#pico-m) | How to model enslaved who are listed as part of an enumeration (for example age category, color, sex) |
| 4. | [Name changes](#pico-m) | Emancipation and manumission records refer to one person, but contain multiple names (enslaved and free name) |
| 5. | [Observation or reconstruction](#pico-m) | The distinction between person observations and person reconstructions, but not always clear with old data (no link to the historical source, information added by researchers) |
| 6. | [Person names](#person-name-vocabulary) | Person names can contain African names, Christian names, and person descriptions |
| 7. | [Person status](#enslaved.org) | There is no property to describe whether someone is enslaved |
| 8. | [Reasons for observation](#enslaved.org) | Enslavement, emancipation, manumission, and trade are necessary to model the start and/or end of observations |
| 9. | Relations<sup>[1](#enslaved.org),[2](#required-specialised-properties)</sup> | Properties to describe relationships for enslavement (slaveholder and enslaved) or legal representation (owner and legal representative, e.g. nomine uxoris) |
| 10. | Slaveholders<sup>[1](#schema.org),[2](#wikidata)</sup> | Slaveholders are not always persons, but can also be organisations (mainly plantations, but also other) |
| 11. | Slave voyages<sup>[1](#schema.org),[2](#exploring-slave-trade-in-asia-esta),[3](#slavevoyage.net),[4](#required-specialised-classes)</sup>  | Ships are required to model slave voyages |
| 12. | Social categories<sup>[1](#enslaved.org),[2](#required-specialised-properties)</sup> | Scholars have collected extensive lists of data related to slavery, such as plantations in Suriname or an overview of all religions. These need to be shared durably |
| 13. | Taxonomies and Thesauri<sup>[1](#wikidata),[2](#taxonomies-and-thesauri)</sup> | Person observations often contain social categories related to race, class, or religion |
| 14. | [Toponyms](#person-name-vocabulary) | Person names of enslaved often contain a toponym with which they have an association. The exact meaning is ambiguous, but the association with the place is, for example, required to reconstruct persons |
| 15. | [Type of enslavement](#enslaved.org) | There is no property to describe the type of enslavement |

## Integration of existing schemas

For each of these issues, we checked whether solutions were available in the Persons in Context model, Enslaved.org, Person Name Vocabulary, Schema.org, and SlaveVoyages.net. For each of these solutions we evaluated the viability for reuse in and presented our outcomes in Q1 and Q2 2025.

### PiCo-M

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 1. | PiCo-M | The logic of the Persons in Context model is easily applicable to data on enslaved persons | **yes** |
| 2. | Age categories | hasAge is used to mention ages. However, the user expects an exact age <br> _**We suggest not to use hasAge to refer to age categories**_ | **no** |
| 3. | Enumerations | Each individual in the enumeration can be modelled as an enslaved with the PiCo or extended characteristics | **yes** |
| 4. | Name changes | An emancipation or manumission record should be seen as two observations: one of an enslaved person until emancipation/manumission, and another of a free person from emancipation/manumission. These two observations can be joint with a personReconstruction. | **yes** |
| 5. | Observation or reconstruction | Person observations are meant to model a record and stay close to the source. Person reconstructions combines information and allows for interpretation. <br> _**In case the relation to the source is lost, and records probably contain interpretation by the data provider, we suggest to use person reconstructions**_ | **yes** |


### Enslaved.org

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 2. | Age categories | [_hasAgeCategory_](https://lod.enslaved.org/wiki/Property:P4) is used to model age groups. This property has four categories: [_Infant Age Group_](https://lod.enslaved.org/wiki/Q426), [_Child Age Group_](https://lod.enslaved.org/wiki/Q427), [_Adult Age Group_](https://lod.enslaved.org/wiki/Q425), and [_Older Person Age Group_](https://lod.enslaved.org/wiki/Q429) |  **yes** | 
| 7. | Person status | [_hasPersonStatus_](https://lod.enslaved.org/wiki/Property:P33) is used to model person status. This property has seven categories: [_Enslaved Person_](https://lod.enslaved.org/wiki/Q109), [_Free Person_](https://lod.enslaved.org/wiki/Q117), [_Freed Person_](https://lod.enslaved.org/wiki/Q386), [_Indentured Person or Pawn_](https://lod.enslaved.org/wiki/Q166), [_Enslaver or Owner_](https://lod.enslaved.org/wiki/Q112), [_Liberated African_](https://lod.enslaved.org/wiki/Q159275), [_Liminal Status Person_](https://lod.enslaved.org/wiki/Q192). This category is too specific to be broadly used, and too broad to be used specifically. <br> _**We suggest to use the property and three concepts: [_Enslaved Person_](https://lod.enslaved.org/wiki/Q109), [_Free Person_](https://lod.enslaved.org/wiki/Q117), [_Liminal Status Person_](https://lod.enslaved.org/wiki/Q192)**_ | **yes** |
| 8. | Reasons for observations | [_hasEventType_](https://lod.enslaved.org/wiki/Property:P30) contains 27 events: [_Advertisement_](https://lod.enslaved.org/wiki/Q907443), [_Appraisal_](https://lod.enslaved.org/wiki/Q647904), [_Baptism or Naming Ceremony_](https://lod.enslaved.org/wiki/Q149), [_Birth_](https://lod.enslaved.org/wiki/Q147), _Burial or Interment_, [_Death_](https://lod.enslaved.org/wiki/Q148), [_Disappearance_](https://lod.enslaved.org/wiki/Q154), [_Disembarkation_](https://lod.enslaved.org/wiki/Q10088), _Education_, [_Emancipation or Manumission_](https://lod.enslaved.org/wiki/Q281), [_Embarkation_](https://lod.enslaved.org/wiki/Q10087), [_Employment, Apprenticeship, or Indenture_](https://lod.enslaved.org/wiki/Q156), [_Enslavement_](https://lod.enslaved.org/wiki/Q151), [_Legal Proceeding_](https://lod.enslaved.org/wiki/Q155), [_Marriage_](https://lod.enslaved.org/wiki/Q150), [_Membership_](https://lod.enslaved.org/wiki/Q473), [_Mention_](https://lod.enslaved.org/wiki/Q856060), [_Military Service_](https://lod.enslaved.org/wiki/Q164), [_Mortgage_](https://lod.enslaved.org/wiki/Q298746), [_Narrative_](https://lod.enslaved.org/wiki/Q157), [_Resistance or Rebellion_](https://lod.enslaved.org/wiki/Q357), [_Registration_](https://lod.enslaved.org/wiki/Q250), [_Relocation_](https://lod.enslaved.org/wiki/Q161), [_Residence_](https://lod.enslaved.org/wiki/Q159), [_Sale or Transfer_](https://lod.enslaved.org/wiki/Q153), [_Trade_](https://lod.enslaved.org/wiki/Q1147583), [_Voyage_](https://lod.enslaved.org/wiki/Q146). These events can be used to indicate to indicate why observation started and ended | **yes** |
| 9. | Relations | Relations are modelled as a concept with its own entities. This approach is incongruent with the PiCo model that uses properties to directly relate two people. | **no** |
| 12. | Social Categories | [_hasRaceorColor_](https://lod.enslaved.org/wiki/Property:P32) is used to model racial characteristics. This variable causes discussions as social categories can also be based on religion, caste, class, etc. | **no** |
| 15. | Type of enslavement | [_hasPersonStatus_](https://lod.enslaved.org/wiki/Property:P33) can be used to model the type of enslavement. However, the seven categories: [_Enslaved Person_](https://lod.enslaved.org/wiki/Q109), [_Free Person_](https://lod.enslaved.org/wiki/Q117), [_Freed Person_](https://lod.enslaved.org/wiki/Q386), [_Indentured Person or Pawn_](https://lod.enslaved.org/wiki/Q166), [_Enslaver or Owner_](https://lod.enslaved.org/wiki/Q112), [_Liberated African_](https://lod.enslaved.org/wiki/Q159275), [_Liminal Status Person_](https://lod.enslaved.org/wiki/Q192) are too specific to be broadly used, and too broad to be used specifically | **yes** |


### Exploring Slave Trade in Asia (ESTA)

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 11. | Slave voyages | Modelling ships is the bread and butter of SlaveVoyages.net and ESTA. We should aim for interoperability with their frameworks. This can easily be managed with [_sdo:TransferAction_](https://schema.org/TransferAction) | **MainVoyage** <br> **SubVoyage** |


### Person Name Vocabulary

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 6. | Person names | Person names can contain African names, Christian names, and person descriptions. These can be modelled with [_nameSpecification_](https://www.lodewijkpetram.nl/vocab/pnv/doc/#nameSpecification) | **yes** |
| 14. | Toponyms | For ontologies, we need an easy way to extract place information from names. We will use examples to ask pnv for an extension of the model. (Update 2025/04/17: PNV is willing to extend if we provide them with a proposal for this property.) | **willing to extend** |


### Schema.org

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 10. | Slaveholders | [_Organization_](https://schema.org/Organization) is a type in Schema.org with relevant properties like [_owns_](https://schema.org/owns), [_employee_](https://schema.org/employee), [_founder_](https://schema.org/founder), [_funder_](https://schema.org/funder), [_member_](https://schema.org/member). These properties can be made reflexive with [_affiliation_](https://schema.org/affiliation) | **yes** |
| 11. | Slave voyages | Modelling ships is the bread and butter of SlaveVoyages.net and ESTA. We should aim for interoperability with their frameworks. This can easily be managed with [_sdo:TransferAction_](https://schema.org/TransferAction) 


### SlaveVoyages.net

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 11. | Slave voyages | Modelling ships is the bread and butter of SlaveVoyages.net and ESTA. We should aim for interoperability with their frameworks. This can easily be managed with [_sdo:TransferAction_](https://schema.org/TransferAction) | **in contact** |


### WikiData
|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 10. | Slaveholders | WikiData can be used to specify the type of organization, and give a definiton of that organization. For example a [_plantation_](https://www.wikidata.org/entity/Q188913) | **yes** |
| 13. | Taxonomies and Thesauri | Thesauri should only be used if they are part of a curated collection, as this ascertain the long-term availability and stability of collections. This makes WikiData unsuited for hosting thesauri | **no** |


### Required specialised classes
|  | Issue | Description	  | class | 
|--|-------|----------------|-------|
| 11. | Slave voyages | Modelling ships is the bread and butter of SlaveVoyages.net and ESTA. We should aim for interoperability with their frameworks. This can easily be managed with [_sdo:TransferAction_](https://schema.org/TransferAction) | **MainVoyage** <br> **SubVoyage** |


### Required specialised properties
|  | Issue | Description	  | property | 
|--|-------|----------------|----------|
| 9. | Relations |  | **isEnslavedBy** <br> **isEnslaverOf** <br> **isLegallyRepresentedBy** <br> **legallyRepresents** |
| 12. | Social categories |  | **hasSocialIdentity** |


### Taxonomies and thesauri
|  | Issue | Description	  | property | 
|--|-------|----------------|----------|
| 13. | Taxonomies and Thesauri | Person observations often contain social categories related to race, class, or religion |


## Exentensions of the PiCo model
Based on the [Evaluation of the PiCo model](#evaluation-of-the-pico-model), we made the following extensions to the PiCo model. These extensions were discussed in Q2 2025 and presented at the DH Benelux in June.


### Enslavement status
Both enslaved and free persons can be modelled as picom:PersonObservations. We use the Enslaved.org property for hasPersonStatus [ed:P33](https://lod.enslaved.org/wiki/Property:P33) to note which persons are Enslaved [ed:Q109](https://lod.enslaved.org/wiki/Q109). 

| Object | Property | Object |
|----|----|----|
| hdsc:enslaved1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; |
| | [ed:P33](https://lod.enslaved.org/wiki/Property:P33) | [ed:Q109](https://lod.enslaved.org/wiki/Q109) . |


### Relation enslaved - enslaver
We use the properties isEnslavedBy and isEnslaverOf to model the relationship between enslaver and enslaved. In its simplest form, this would result in the following triples.

| Object | Property | Object |
|----|----|----|
| hdsc:enslaved1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; |
| | [ed:P33](https://lod.enslaved.org/wiki/Property:P33) | [ed:Q109](https://lod.enslaved.org/wiki/Q109) ; |
| | XXX:isEnslavedBy | hdsc:owner1 . |
| hdsc:enslaved2 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; |
| | [ed:P33](https://lod.enslaved.org/wiki/Property:P33) | [ed:Q109](https://lod.enslaved.org/wiki/Q109) ; |
| | XXX:isEnslavedBy | hdsc:owner1 . |
| hdsc:owner1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; |
| | XXX:isEnslaverOf | hdsc:enslaved1, hdsc:enslaved2 . |

However, we advise to also add the beginning and end date of the observed enslaved relations with a blank node using [sdo:startDate](https://schema.org/startDate) and [sdo:endDate](https://schema.org/endDate), as slavery relations can change over time. 

| Subject | Property | Object | Property Blank Node | Object Blank Node |
|----|----|----|----|----|
| hdsc:enslaved1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; | | |
| | [ed:P33](https://lod.enslaved.org/wiki/Property:P33) | [ed:Q109](https://lod.enslaved.org/wiki/Q109) ; | | |
| | XXX:isEnslavedBy | [ | [rdf:value](http://www.w3.org/1999/02/22-rdf-syntax-ns#value) | hdsc:owner1 ; |
| | | | [sdo:startDate](https://schema.org/startDate) | "1837-08-15"^^xsd:date ; |
| | | | [sdo:endDate](https://schema.org/endDate) | "1838"^^xsd:gYear ; |
| | | ] . | | |
| hdsc:enslaved2 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; | | |
| | [ed:P33](https://lod.enslaved.org/wiki/Property:P33) | [ed:Q109](https://lod.enslaved.org/wiki/Q109) ; | | |
| | XXX:isEnslavedBy | [ | [rdf:value](http://www.w3.org/1999/02/22-rdf-syntax-ns#value) | hdsc:owner1 ; |
| | | | [sdo:startDate](https://schema.org/startDate) | "1837-08-16"^^xsd:date ; |
| | | | [sdo:endDate](https://schema.org/endDate) | "1838"^^xsd:gYear ; |
| | | ] . | | |
| hdsc:owner1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; | | |
| | XXX:isEnslaverOf | [ | [rdf:value](http://www.w3.org/1999/02/22-rdf-syntax-ns#value) | hdsc:enslaved1 ; |
| | | | [sdo:startDate](https://schema.org/startDate) | "1837-08-15"^^xsd:date ; |
| | | | [sdo:endDate](https://schema.org/endDate) | "1838"^^xsd:gYear ; |
| | | ] ; | | |
| | XXX:isEnslaverOf | [ | [rdf:value](http://www.w3.org/1999/02/22-rdf-syntax-ns#value) | hdsc:enslaved2 ; |
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

  
### Relation enslaved - legal representative


### Relation owner - legal representative
Owners are sometimes represented by an intermediary or by their spouse. This is modelled with the properties legallyRepresents and legallyRepresentedBy.

| Object | Property | Object |
|----|----|----|
| hdsc:owner1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; |
| | [sdo:spouse](https://schema.org/spouse) | hdsc:intermediary1 ; |
| | [XXX:legallyRepresentedBy] | hdsc:intermediary1 . |
| hdsc:intermediary1 | [a](https://www.w3.org/1999/02/22-rdf-syntax-ns#type) | [picom:PersonObservation](https://personsincontext.org/model/#PersonObservation) ; |
| | [sdo:spouse](https://schema.org/spouse) | hdsc:owner1 ; |
| | [XXX:legallyRepresents] | hdsc:owner1 . |


### Plantations (and other organisations)


### Slave voyages


### Group observations


### Manumission

