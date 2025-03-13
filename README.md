# Modelling the enslaved as historical persons

Rick Mourits, Thunnis van Oort, Kay Pepping, Pascal Konings, Britt van Duijvenvoorde

## Introduction

In this document, we reflect on how to implement historical person data on enslaved people as Linked Data. Our aim is to use the [PiCo model](https://www.personsincontext.org) to fit all historical person observations  and to provide flexibility and guidelines for extending the model.

The PiCo model states how information on common factors in historical person observations, such as age, dates of birth, marriage, and death, occupations, relations between family members, roles in source documents, etc. should be described. In order to effectively communicate (historical) person data, the Dutch Center for Family History (CBG) has developed the Persons in Context (PiCo) model (Woltjer et al., 2024), on the basis of the ROAR model developed by Menno den Engelse and Leon van Wissen (2021). 

The PiCo model reuses as many existing URIs as possible to describe historical person data, as it encourages communities to give the same name to the same entity. This prevents discussions on naming and describing resources that have already been authoritatively defined, such as birth dates or names. Moreover, this makes data more findable as people can search on one common term, rather than having to waste time on resolving a potentially endless list of variations in modelling the same concept. And, perhaps even more importantly, it also enforces stringent definitions of properties and resources that can be used for efficient knowledge interfering

## Specifications
- Persons are modelled as standardised in the Persons in Context model (PiCo-M)
- Where possible, extensions to the model are based on existing vocabularies
- Extensions to the model follow the logic of concentric description: where possible global (Schema.org), otherwise domain-specific (Enslaved.org), or specialised (Person Name Vocabulary)
- New extensions can be introduced with consensus between the HDSC, Globalised, and ESTA

## Evaluation of the PiCo model
During three meetings in Q1 2025, we came to the following conclusions


|  | Issue | Description	  |
|--|-------|----------------|
| 1. | PiCo-M | The logic of the Persons in Context model is easily applicable to data on enslaved persons |
| 2. | Age categories | Person observations sometimes only state an age category (child vs adult) rather than the exact age |
| 3. | Observation or reconstruction | The distinction between person observations and person reconstructions, but not always clear with old data (no link to the historical source, information added by researchers) |
| 4. | Person names | Person names contain more information than can currently be modelled in Schema.org or Person Name Vocabulary (African names, Christian names, person descriptions) |
| 5. | Person status | There is no property to describe whether someone is enslaved |
| 6. | Reasons for observation | Enslavement, emancipation, manumission, and trade are necessary to model the start and/or end of observations |
| 7. | Relations | Properties to describe relationships for enslavement (slaveholder and enslaved) or legal representation (owner and legal representative, e.g. nomine uxoris) |
| 8. | Slaveholders | Slaveholders are not always persons, but can also be organisations (mainly plantations, but also other) |
| 9. | Ships | Ships are required to model slave voyages |
| 10. | Social categories | Person observations often contain social categories related to race, class, or religion |
| 11. | Type of enslavement | There is no property to describe the type of enslavement |

## Integration of existing schemas

### PiCo-M

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 1. | PiCo-M | The logic of the Persons in Context model is easily applicable to data on enslaved persons | **yes** |
| 2. | Age categories | hasAge is used to mention ages. However, the user expects an exact age <br> We advise not to use hasAge to refer to age categories | **no** |
| 3. | Observation or reconstruction | Person observations are meant to model a record and stay close to the source. Person reconstructions combines information and allows for interpretation. <br> _**In case the relation to the source is lost, and records probably contain interpretation by the data provider, we advise to use person reconstructions**_ | **yes** |


### Enslaved.org

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 2. | Age categories | [_hasAgeCategory_](https://lod.enslaved.org/wiki/Property:P4) is used to model age groups. This property has four categories: [_Infant Age Group_](https://lod.enslaved.org/wiki/Q426), [_Child Age Group_](https://lod.enslaved.org/wiki/Q427), [_Adult Age Group_](https://lod.enslaved.org/wiki/Q425), and [_Older Person Age Group_](https://lod.enslaved.org/wiki/Q429) |  **yes** | 
| 5. | Person status | [_hasPersonStatus_](https://lod.enslaved.org/wiki/Property:P33) is used to model person status. This property has seven categories: [_Enslaved Person_](https://lod.enslaved.org/wiki/Q109), [_Free Person_](https://lod.enslaved.org/wiki/Q117), [_Freed Person_](https://lod.enslaved.org/wiki/Q386), [_Indentured Person or Pawn_](https://lod.enslaved.org/wiki/Q166), [_Enslaver or Owner_](https://lod.enslaved.org/wiki/Q112), [_Liberated African_](https://lod.enslaved.org/wiki/Q159275), [_Liminal Status Person_](https://lod.enslaved.org/wiki/Q192). This category is too specific to be broadly used, and too broad to be used specifically. <br> _**We suggest to use the property and three concepts: [_Enslaved Person_](https://lod.enslaved.org/wiki/Q109), [_Free Person_](https://lod.enslaved.org/wiki/Q117), [_Liminal Status Person_](https://lod.enslaved.org/wiki/Q192)**_ | **yes** |
| 6. | Reasons for observations | | **yes** |
| 7. | Relations | Relations are modelled as a concept with its own entities. This approach is incongruent with the PiCo model that uses properties to directly relate two people. | **no** |
| 10. | Social Categories | [_hasRaceorColor_](https://lod.enslaved.org/wiki/Property:P32) is used to model racial characteristics. This variable causes discussions as social categories can also be based on religion, caste, class, etc. | **no** |
| 11. | Type of enslavement | _hasPersonStatus_](https://lod.enslaved.org/wiki/Property:P33) can be used to model the type of enslavement. However, the seven categories: [_Enslaved Person_](https://lod.enslaved.org/wiki/Q109), [_Free Person_](https://lod.enslaved.org/wiki/Q117), [_Freed Person_](https://lod.enslaved.org/wiki/Q386), [_Indentured Person or Pawn_](https://lod.enslaved.org/wiki/Q166), [_Enslaver or Owner_](https://lod.enslaved.org/wiki/Q112), [_Liberated African_](https://lod.enslaved.org/wiki/Q159275), [_Liminal Status Person_](https://lod.enslaved.org/wiki/Q192) are too specific to be broadly used, and too broad to be used specifically | **yes** |


### Person Name Vocabulary

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 4. | Person names | Person names contain more information than can currently be modelled in Schema.org or Person Name Vocabulary (African names, Christian names, person descriptions) | **Reach out** |


### Schema.org

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 8. | Slaveholders | [Organization](https://schema.org/Organization) is a concept in Schema.org | **TBD** |


### SlaveVoyages.net

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 9. | Ships | Modelling ships is the bread and butter of SlaveVoyages.net.  | **Reach out** |


### Required specialised properties
|  | Issue | Description	  | property | 
|--|-------|----------------|----------|
| 10. | Social categories |  | **hasSocialDescription** |
| 11. | Type of enslavement | **TBD** |
