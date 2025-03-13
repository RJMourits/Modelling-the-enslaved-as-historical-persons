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


| Issue    | Description	  | 
|----------|----------------|
| 1. | The logic of the Persons in Context model is easily applicable to data on enslaved persons |
| 2. | The distinction between person observations and person reconstructions, but not always clear with old data (no link to the historical source, information added by researchers) |
| 3. | There is no property to describe whether someone is enslaved |
| 4. | Properties to describe relationships for enslavement (slaveholder and enslaved) or legal representation (owner and legal representative, e.g. nomine uxoris) |
| 5. | Enslaved are not always persons, but can also be organisations (mainly plantations, but also other) |
| 6. | Ships are required to model slave voyages |
| 7. | Enslavement, emancipation, manumission, and trade are necessary to model the start and/or end of observations |
| 8. | Person observations often contain social categories related to race, class, or religion |
| 9. | Person names contain more information than can currently be modelled in Schema.org or Person Name Vocabulary (African names, Christian names, person descriptions) |
| 10. | Person observations sometimes only state an age category (child vs adult) rather than the exact age |

## Integration of existing schemas

### Enslaved.org
3. 
4. Relations are modelled as a concept with its own entities. This approach is incongruent with the PiCo model that uses properties to directly relate two people
