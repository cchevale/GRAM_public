# Node Labels & Properties

In GRAM, nodes can be of two different kinds only. They are either `Actions` or `Actors`.  Places are treated as any other actors, but due to their particular nature, they are labelled as `Places`. One should nonetheless keep in mind that they are first and foremost instances of actor nodes.

Nodes can have as many `labels` as necessary. Labels serve to categorize entities and to efficiently traverse the graph. Good practice in graph databases is (usually) not to add more than four labels to a node. In GRAM's framework, nodes can thus have up to four labels:

1. One general label differentiating between entity types (Actor, Action, Place);
2. One sub-label for additional categorization (one subclass). For instance, an Actor being also a Person, a Group, or an Institution;
3. One additional sub-label, in such cases where one entity with the same properties refers to things of a different nature. For instance, a Place which also corresponds to a human-made (architectural) Object;
4. Finally, one last research-/domain-related label used to flag entities as of interest to a particular project or question.

Nodes may have numerous `properties`, depending on the information contained in the source. The level of enrichment can be as detailed as necessary, but will mostly depend on the research questions and the time dedicated to recording information. However, if enrichment can be as detailed as necessary, users must clearly distinguish between GRAM's limited set of `basic` properties and the unlimited numbers of project-`specific` properties. As a granular and source-related model, GRAM is committed to engaging with the semantics of the sources and to avoiding encoding the researchers' interpretation. We thus strongly advocate in favor of recording only the information provided by the source, in the language of the source. Hence, GRAM's basic properties are usually recorded in both their emic form *and* in English.

In any case, nodes in GRAM have at least the following basic properties:

1. `date` information: exact, relative, or approximate dates of existence of a node (see the Conventions section for date notations);
2. `emic`: designation(s) of the entity in the language of the sources (for Action nodes, the emic expressions are collected under the `verbEmic` property key);
3. `id`: a unique identifier (for this one may want to call random UUIDs);
4. `name`: one canonical (standardized) name chosen to represent the entity in Latin alphabet (for Action nodes, the canonical name is the `verb` property key).

## 1 (:Action) Nodes

`Action nodes` record actions in their verbal form(s). By default, Action nodes are considered to represent unique actions that actually happened (according to the sources). However, actions can also be repetitive, hypothetical (e.g., when said to possibly have happened, to be intended, situated in the future or prescribed) or conditional (like a condition stated in an agreement). Oftentimes, an action is flanked with adverbs that carry a value judgement, specify its intensity, etc. (e.g., when it is presented as ungodly or unlawful). If such information is explicit in the source, it must be recorded. Instead of using possibly limitless property keys to categorize these qualities, GRAM's basic model only uses one action qualifier property key (`actionQualif`, a string array that can record many such qualifiers). Categorization and interpretation, as well as addition of implicit or context-informed qualifiers are left to further stages of the research workflow (when the users manipulates and analyze the data) or to the researcher's decision to develop their own properties.

### 1.1 Action Nodes Optional Labels

Action nodes have no optional labels, except those used to flag actions to answer a specific question.

### 1.2 Action Nodes Properties

One tricky yet crucial issue that GRAM faced was to keep track of the source of the information and, at the same time, disentangle the voices and perspectives conveyed by the source documents or parts of them. Action nodes thus *systematically* have one property key (`assetId`) referencing either the whole text itself, or a section of the source text carrying a specific point of view (e.g., a court records with many testimonies). For this, we advise to record references to different parts of a source text (assets) in a separate spreadsheet with as many variable as necessary but with at least a unique identifier used as the value of the `assetId` property key. Each action can then be related to the node of the the "speaking" Actor with a `[ACCORDING_TO] relationship.

| Action property key | property values | notation | description |
| :--- | :--- | :--- | :--- |
| `actionQualif` |  | {string array} | generic record of the action qualifier(s) |
| `actionQualifEmic` |  | {string array} | generic record of the action qualifier(s), in their emic form |
| `assetId` |  | {string} | code of the text snippet (see above) |
| `comment` |  | {string} | any relevant comment explaining an action or the researcher's choices and interpretation |
| `date` |  | {date} | date of an action |
| `id` |  | {string}{unique} | unique identifier of an action |
| `gramMode` | `passive` | {string} | grammatical mode used in the sentence. If active, the value remains `null` |
| `term` |  | {duration} | when deadline/term is set for enduring action. If dates are given use date notation instead of duration |
| `verb` |  | {string} | canonical verbal form in English |
| `verbEmic` |  | {string array} | verb(s) and verbal form(s) by which the action is designated in a text, in original language |

## 2 (:Actor) Nodes

`Actor nodes` represent entities that are involved and *play a role* in an Action. Actor properties only record permanent characters of an Actor for the duration of its existence (with the exception of proper names and aliases, which may not be permanent but are still recorded as properties). For instance, a Person's title or status might be temporary and thus cannot be attached to the Actor's node as a permanent character. Actors can be of any kind: `human` and `non-human`, `material` and `immaterial`. Additional labels can thus be added to Actor nodes for better categorization.

### 2.1 Actor Nodes Optional Labels

| Actor optional label | description |
| :--- | :--- |
| `:Animal` | non-human living creatures |
| `:Environment` | environmental actors that play a role in the Action, often as "effectors" |
| `:Group` | groups of more than one (not necessarily human) individual involved in an action. Groups can be composed of indistinct and/or named individuals |
| `:Immaterial` | immaterial objects, including beliefs, statuses, titles, and occupations. Immaterial labels are used to manipulate as actors "things" that have no physical manifestations, like a "concept", a "status", an "occupation", an "information", or an "appellation". E.g., when a person is "sentenced to" a "punishment", "assigned" to a legal category, etc. |
| `:Institution` | institutions |
| `:NonHuman` | creatures that are non-human and have no material existence like gods, spirits, etc. |
| `:Object` | material things involved in the action, often as a "medium" or "instrument" (like a contract, an amount of money, a vehicle, etc.). They can be unique, indistinct groups of, or numerable objects |
| `:People` | groups of human beings only designated in the sources as populations of a given territory or polity (not as individuals or groups) |
| `:Person` | individual human beings. Properties only record permanent information about a person. Features that may have a time validity, like a title, an occupation, a status, are only stored as properties of the relationship between a person and an action |

#### 2.2 Actor Nodes Properties

Depending on their optional Labels, Actor nodes can have different properties. Below are examples of some common Actor node properties that our team has used:

| Actor additional Label | property key | property values | notation | description |
| :--- | :--- | :--- | :--- | :--- |
| `:Animal` | `comment` |  | {string} | additional information about the actor or the researcher's interpretation |
|  | `dob`; `dod ` |  | {date} | dates of birth and death of an animal |
|  | `type` |  | {string} | type of animal when specified |
|  | `sex` | `female`; `male` | {string} | when known and applicable |
|  | `id` |  | {string}{unique} | unique identifier of animal |
|  | `name` |  | {string} | canonical name of an animal |
||||||
| `:Environment` | `comment` |  | {string} | additional information about the actor or the researcher's interpretation |
|  | `date` | | {date} | dates of existence of an environmental actor |
|  | `emic` |  | {string array} | emic designation(s) of an environmental actor |
|  | `id` |  | {string}{unique} | unique identifier of an environmental actor |
|  | `name` |  | {string} | canonical name of an environmental actor |
||||||
| `:Group` | `age` | `children`; `adults`; `adults-children`| {string array} | age composition of a group of persons |
|  | `comment` |  | {string} | additional information about the actor or the researcher's interpretation |
|  | `date` |  | {date} | dates of existence of a group |
|  | `emic` |  | {string array} | emic designation(s) of a group |
|  | `gender` | `female`; `male`; `mixed` | {string} | gender composition of a group |
|  | `id` |  | {string}{unique} | unique identifier of a group |
|  | `name` |  | {string} | canonical name of a group |
|  | `number` |  | {integer} | number of persons in a group |
|  | `numberQualif` | `above`; `approx`; `below`; `multipleOf` | {string} | qualifier of the number of a group, when approximate |
|  | `size` |  | {string array} | size of the group, if not provided as number (e.g., "numerous") |
||||||
| `:Immaterial` | `comment` |  | {string} | additional information about the actor or the researcher's interpretation |
|  | `date` |  | {date} | dates of existence of an immaterial actor |
|  | `emic` |  | {string array} | emic designation(s) of an immaterial actor |
|  | `id` |  | {string}{unique} | unique identifier of an actor |
|  | `name` |  | {string} | canonical name of an immaterial actor |
||||||
| `:Institution` | `comment` |  | {string} | additional information about the actor or the researcher's interpretation |
|  | `date` |  | {date} | dates of existence of an institutional actor |
|  | `emic` |  | {string array} | emic designation(s) of an institutional actor |
|  | `id` |  | {string}{unique} | unique identifier of an institutional actor |
|  | `name` |  | {string} | canonical name of an institutional actor |
||||||
| `:NonHuman` | `aliases` |  | {string array} | names of a non-human entity (emic, social names, aliases, etc.), in different languages and scripts |
|  | `bio` |  | {url} | identifier of the non-human entity in a reference index |
|  | `comment` |  | {string} | additional information about the actor or the researcher's interpretation |
|  | `dob`; `dod ` |  | {date} | dates of birth and death of a non human entity, when applicable |
|  | `ethnicity` |  | {string} | when specified |
|  | `gender` | `female`; `male` | {string} | gender of non human entity |
|  | `id` |  | {string}{unique} | unique identifier of a non human entity |
|  | `name` |  | {string} | canonical name of a non human entity |
||||||
| `:Object` | `comment` |  | {string} | additional information about the actor or the researcher's interpretation |
|  | `date` |  | {date} | dates of existence of an object |
|  | `emic` |  | {string array} | emic designation(s) of an object |
|  | `id` |  | {string}{unique} | unique identifier of an object |
|  | `name` |  | {string} | canonical name of an object |
|  | `number` |  | {float} | quantity, for numerable material objects |
|  | `objectQuality` |  | {string} | quality of the object, when stated |
|  | `objectType` | commodity; currency; document; medicine; product; vehicle; etc. | {string} | for further categorization, object entities are added a type property |
|  | `unit` |  | {string} | unit of the value associated with an object |
|  | `value` |  | {float} | value of the object |
||||||
| `:People` | `comment` |  | {string} | additional information about the actor or the researcher's interpretation |
|  | `id` |  | {string}{unique} | unique identifier of an Actor |
|  | `name` |  | {string} | canonical name of a people actor |
||||||
| `:Person` | `aliases` |  | {string array} | names of a person (emic, social names, aliases, etc.), in different languages and scripts |
|  | `bio` |  | {url} | identifier of a person in a bibliographical reference index like the [China Biographical DB](https://projects.iq.harvard.edu/cbdb/home) |
|  | `comment` |  | {string} | additional information about the actor or the researcher's interpretation |
|  | `dob`; `dod ` |  | {date} | dates of birth and death of a person |
|  | `ethnicity` |  | {string} | when specified |
|  | `gender` | `female`; `male` | {string} | gender of a person |
|  | `id` |  | {string}{unique} | unique identifier of person |
|  | `name` |  | {string} | canonical name of a person |

## 3 (:Place) Nodes

`Places` can play various roles in an action and are considered as a specific category of Actors. Places are sometimes confused with human-made constructions and can, for instance, also have an Object label. Place nodes have at least one geographical point for geo-referencing (links to existing polygon information may be added when existing). Place nodes can be of different nature (administrative, natural, religious, etc.) and thus also have Type and Subdivision properties. We only used these two basic categories because categorizing places can be very contentious (e.g., how does one define a "polity"?). Again, we strongly advise to record the information only when it is specified in the source and in the language of the source. Users can develop their own vocabulary, but this operation of categorization can be achieved at later stages of the research workflow. Dependency relations between Place nodes (like a region being part of a Polity) can be recorded in relations between different Place nodes.

### 3.1 Place Nodes Properties

| Place property key | property values | notation | description |
| :--- | :--- | :--- | :--- |
| `dateEnd` |  | {date} | date when a Place set of attributes stop to be valid due to a change in name, in administrative level, territory, etc. |
| `dateStart` |  | {date} | date when a Place ste of attributes start to be valid (due to a change in name, in administrative level, territory, etc.) |
| `gazetteer` |  | {url} | url/uri identifier of the place in reference gazetteer ([Getty thesaurus](https://www.getty.edu/research/tools/vocabularies/tgn/index.html), [CHGIS](http://chgis.fas.harvard.edu/), etc.) |
| `id` |  | {string}{unique} | unique identifier of a place|
| `latitude` |  | {float} | latitude of the point chosen for geo-referencing |
| `longitude` |  | {float} | longitude of the point chosen for geo-referencing |
| `name` |  | {string} | canonical name chosen to represent a place (in Latin alphabet)|
| `nameAlt` | | {string array} | known alternative names for a place, in any language |
| `placeSubdiv` | e.g., `area`; `city`; `country`; `district`; `pass`; `polity`; `prefecture`; `settlement`; `subprefecture`; etc. | {string} | type of spatial subdivision |
| `placeType` | e.g., `administrative`; `natural`; `religious` | {string} | nature of the space |