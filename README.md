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
| 2. | Age categories | Person observations sometimes only state an age category (child vs adult) rather than the exact age  |
| 3. | Name change | Emancipation and manumission records refer to one person, but contain multiple names (enslaved and free name) |
| 4. | Observation or reconstruction | The distinction between person observations and person reconstructions, but not always clear with old data (no link to the historical source, information added by researchers) |
| 5. | Person names | Person names contain more information than can currently be modelled in Schema.org or Person Name Vocabulary (African names, Christian names, person descriptions) |
| 6. | Person status | There is no property to describe whether someone is enslaved |
| 7. | Reasons for observation | Enslavement, emancipation, manumission, and trade are necessary to model the start and/or end of observations |
| 8. | Relations | Properties to describe relationships for enslavement (slaveholder and enslaved) or legal representation (owner and legal representative, e.g. nomine uxoris) |
| 9. | Slaveholders | Slaveholders are not always persons, but can also be organisations (mainly plantations, but also other) |
| 10. | Ships | Ships are required to model slave voyages |
| 11. | Social categories | Person observations often contain social categories related to race, class, or religion |
| 12. | Toponyms | Person names of enslaved often contain a toponym with which they have an association. The exact meaning is ambiguous, but the association with the place is, for example, required to reconstruct persons |
| 13. | Type of enslavement | There is no property to describe the type of enslavement |

## Integration of existing schemas

### PiCo-M

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 1. | PiCo-M | The logic of the Persons in Context model is easily applicable to data on enslaved persons | **yes** |
| 2. | Age categories | hasAge is used to mention ages. However, the user expects an exact age <br> _**We suggest not to use hasAge to refer to age categories**_ | **no** |
| 3. | Name change | An emancipation or manumission record should be seen as two observations: one of an enslaved person until emancipation/manumission, and another of a free person from emancipation/manumission. These two observations can be joint with a personReconstruction. | **yes** |
| 4. | Observation or reconstruction | Person observations are meant to model a record and stay close to the source. Person reconstructions combines information and allows for interpretation. <br> _**In case the relation to the source is lost, and records probably contain interpretation by the data provider, we suggest to use person reconstructions**_ | **yes** |


### Enslaved.org

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 2. | Age categories | [_hasAgeCategory_](https://lod.enslaved.org/wiki/Property:P4) is used to model age groups. This property has four categories: [_Infant Age Group_](https://lod.enslaved.org/wiki/Q426), [_Child Age Group_](https://lod.enslaved.org/wiki/Q427), [_Adult Age Group_](https://lod.enslaved.org/wiki/Q425), and [_Older Person Age Group_](https://lod.enslaved.org/wiki/Q429) |  **yes** | 
| 6. | Person status | [_hasPersonStatus_](https://lod.enslaved.org/wiki/Property:P33) is used to model person status. This property has seven categories: [_Enslaved Person_](https://lod.enslaved.org/wiki/Q109), [_Free Person_](https://lod.enslaved.org/wiki/Q117), [_Freed Person_](https://lod.enslaved.org/wiki/Q386), [_Indentured Person or Pawn_](https://lod.enslaved.org/wiki/Q166), [_Enslaver or Owner_](https://lod.enslaved.org/wiki/Q112), [_Liberated African_](https://lod.enslaved.org/wiki/Q159275), [_Liminal Status Person_](https://lod.enslaved.org/wiki/Q192). This category is too specific to be broadly used, and too broad to be used specifically. <br> _**We suggest to use the property and three concepts: [_Enslaved Person_](https://lod.enslaved.org/wiki/Q109), [_Free Person_](https://lod.enslaved.org/wiki/Q117), [_Liminal Status Person_](https://lod.enslaved.org/wiki/Q192)**_ | **yes** |
| 7. | Reasons for observations | [_Event Type_](https://lod.enslaved.org/wiki/Property:P30)_ contains 27 events: [_Advertisement_](https://lod.enslaved.org/wiki/Q907443), [_Appraisal_](https://lod.enslaved.org/wiki/Q647904), [_Baptism or Naming Ceremony_](https://lod.enslaved.org/wiki/Q149), [_Birth_](https://lod.enslaved.org/wiki/Q147), _Burial or Interment_, [_Death_](https://lod.enslaved.org/wiki/Q148), [_Disappearance_](https://lod.enslaved.org/wiki/Q154), [_Disembarkation_](https://lod.enslaved.org/wiki/Q10088), _Education_, [_Emancipation or Manumission_](https://lod.enslaved.org/wiki/Q281), [_Embarkation_](https://lod.enslaved.org/wiki/Q10087), [_Employment, Apprenticeship, or Indenture_](https://lod.enslaved.org/wiki/Q156), [_Enslavement_](https://lod.enslaved.org/wiki/Q151), [_Legal Proceeding_](https://lod.enslaved.org/wiki/Q155), [_Marriage_](https://lod.enslaved.org/wiki/Q150), [_Membership_](https://lod.enslaved.org/wiki/Q473), [_Mention_](https://lod.enslaved.org/wiki/Q856060), [_Military Service_](https://lod.enslaved.org/wiki/Q164), [_Mortgage_](https://lod.enslaved.org/wiki/Q298746), [_Narrative_](https://lod.enslaved.org/wiki/Q157), [_Resistance or Rebellion_](https://lod.enslaved.org/wiki/Q357), [_Registration_](https://lod.enslaved.org/wiki/Q250), [_Relocation_](https://lod.enslaved.org/wiki/Q161), [_Residence_](https://lod.enslaved.org/wiki/Q159), [_Sale or Transfer_](https://lod.enslaved.org/wiki/Q153), [_Trade_](https://lod.enslaved.org/wiki/Q1147583), [_Voyage_](https://lod.enslaved.org/wiki/Q146). These events can be used to indicate to indicate why observation started and ended | **yes** |
| 8. | Relations | Relations are modelled as a concept with its own entities. This approach is incongruent with the PiCo model that uses properties to directly relate two people. | **no** |
| 11. | Social Categories | [_hasRaceorColor_](https://lod.enslaved.org/wiki/Property:P32) is used to model racial characteristics. This variable causes discussions as social categories can also be based on religion, caste, class, etc. | **no** |
| 13. | Type of enslavement | _hasPersonStatus_](https://lod.enslaved.org/wiki/Property:P33) can be used to model the type of enslavement. However, the seven categories: [_Enslaved Person_](https://lod.enslaved.org/wiki/Q109), [_Free Person_](https://lod.enslaved.org/wiki/Q117), [_Freed Person_](https://lod.enslaved.org/wiki/Q386), [_Indentured Person or Pawn_](https://lod.enslaved.org/wiki/Q166), [_Enslaver or Owner_](https://lod.enslaved.org/wiki/Q112), [_Liberated African_](https://lod.enslaved.org/wiki/Q159275), [_Liminal Status Person_](https://lod.enslaved.org/wiki/Q192) are too specific to be broadly used, and too broad to be used specifically | **yes** |


### Person Name Vocabulary

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 5. | Person names | Person names contain more information than can currently be modelled in Schema.org or Person Name Vocabulary (African names, Christian names, person descriptions) | **Reach out** |


### Schema.org

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 9. | Slaveholders | [Organization](https://schema.org/Organization) is a concept in Schema.org | **TBD** |


### SlaveVoyages.net

|  | Issue | Description	  | Reuse |
|--|-------|----------------|-------|
| 10. | Ships | Modelling ships is the bread and butter of SlaveVoyages.net. We should aim for interoperability with their framework  | **Reach out** |


### Required specialised properties
|  | Issue | Description	  | property | 
|--|-------|----------------|----------|
| 8. | Relations |  | **isEnslavedBy** <br> **isEnslaverOf** <br> **isLegallyRepresentedBy** <br> **legallyRepresents** |
| 11. | Social categories |  | **hasSocialIdentity** |
| 12. | Toponyms | **TBD** |
| 13. | Type of enslavement | **TBD** |
