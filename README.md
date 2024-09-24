# Graph of Roles and Actions Model

<img src="images/orcid.svg" alt="drawing" style="width:13px;"/> [Claude Chevaleyre](https://orcid.org/0000-0001-5770-0567); 
<img src="images/orcid.svg" alt="drawing" style="width:13px;"/> [Johan Heinsen](https://orcid.org/0000-0001-9823-9009); <img src="images/orcid.svg" alt="drawing" style="width:13px;"/> [Corinna Peres](https://orcid.org/0000-0003-2166-1599); <img src="images/orcid.svg" alt="drawing" style="width:13px;"/> [Juliane Schiel](https://orcid.org/0000-0002-9277-5887)

## GRAM: An Agnostic Framework for Social History

GRAM, or `Graph of Roles and Actions Model`, is a basic data model for graph databases. An outcome of the discussions within the working group "Grammars of Coercion" of the COST Action CA18205 [Worlds of Related Coercions in Work](https://worck.eu/), funded from November 2019 to March 2024, it is designed to be an agnostic data framework for social history. 

At the centre of the model are actions. As social historians we believe that the past can best be analysed based on what people did. As microhistorians and scholars of historical semantics we also believe that this cannot be meaningfully separated from how our sources describe those actions. GRAM provides a framework built on those basic insights. Starting from the actions described by our sources, these are related to other entities and to one another. On this footing, GRAM allows historian to tackle the granularity of information in historical text sources.

By agnostic, we mean three things. First, that the model should offer enough robustness and flexibility to store and serve data for social history projects regardless of the users' research questions and whatever the language and the type of the sources. Second, agnostic means that the sources are transformed into data in their entirety: the information that is transformed into data should not be preselected. Third, agnosticity also means that the information is recorded as it appears in the language of the sources – in its emic form – alongside a layer of translation into English offering only minimal standardization.

GRAM is conceived as a foundational framework for a variety of uses, in the sense that it does not pretend to provide an exhaustive categorization scheme (an ontology). Categorization processes are part of the research process itself and can only be achieved by the researchers according to the scope and goals of their research questions. GRAM provides a basic ingestion framework to start from. It is designed to be vertatile enough that it can then serve as the basis for additional levels of categorization when it is deemed necessary or useful. This might range from simply organizing the messiness of the sources for quantitative analysis to cross-corpora categorizations allowing comparisons across time and space.

Still in development, GRAM relies on a series of simple rules and principles. They are described below. Its performance will have to be tested against its ability to efficiently query data and thereby to produce useful subsets of data for a wide array of social history projects. The main challenge, however, resides in the ability of the model to serve the purpose of cross-cultural comparison. This is the topic of the research project that GRAM was developed for and that will involve collaboration with computational linguists. 

### An Action-Centric LPG Model

The main feature of GRAM is that it is action-centric. Historians with an extensive experience of relational database modelling[^1] have come to a similar and quite unambiguous conclusion: transforming historical information into data merely amounts to disaggregating "events" into related entities representing bits of information about `WHO` did `WHAT` to/with `WHOM`, `WHEN` and `WHERE`. From this perspective, the historical "events" that historians are interested in and try to make sense of can be conceived and digitally modelled as series of [semantic triples](https://dbpedia.org/page/Triplestore) (the three linked data pieces used in semantic graph databases, i.e., the `Subject-Predicate-Object` triple). This observation is a compelling argument in favor of a wider use of graph models in historical database projects. The creators of the [Simple Event Model](https://semanticweb.cs.vu.nl/2009/11/sem/) (SEM) have already suggested to go in this direction by explicitly adding an "Event" entity ("What") to more familiar ones like places ("Where"), persons and groups ("Who"), and time information ("When") in RDF-compliant data models. Other existing data models and ontologies, like [CIDOC-CRM](https://ontome.net/namespace/7), also insist on the efficiency of event-centric modelling.

However, defining historical events can be a daunting and rather complex task. Drawing from the [verb-oriented method](https://doi.org/10.1353/emw.2018.0057) developed by the [Gender and Work project](https://www.uu.se/en/research/gender-and-work), GRAM puts `Action` entities at the core of its modelling approach rather than more complex and abstract events. To do so, we focus on the action descriptors that can be found in textual sources: typically centering on verbs and verbal expressions. Verbs and verbal expressions are thus used as core structural elements of `Action` entities related to `Actor` entities by `Role` relationships. The role vocabulary which we rely on is derived from semantic and thematic roles ontologies (like Beatrice Primus' [Semantische Rollen](https://www.winter-verlag.de/de/detail/978-3-8253-5977-5/Primus_Semantische_Rollen/) and John F. Sowa's [Thematic Roles](https://www.jfsowa.com/ontology/thematic.htm); see also See Anthony R. Davis, [Thematic Roles](https://doi.org/10.1515/9783110626391-003)). In short, GRAM relies on a minimal structure made of `(Action)-[HAS_ACTOR_WITH_ROLE]->(Actor)` triples. Interoperability will be ensured, at least partially, by the reuse of existing vocabularies to structure the properties of its Action and Actor nodes. 

With regards to modelling, GRAM uses the [Label Property Graph](https://neo4j.com/blog/rdf-vs-property-graphs-knowledge-graphs/) (LPG) structure rather than the natively-interoperable [Resource Description Framework](https://www.w3.org/RDF/) (RDF). The LPG model (implemented in a Neo4j database) was found to be more manageable, less demanding in terms of resources and development, and more efficient to store and query historical data. First, being "schema-free", it allows progressive refactoring as the model evolves. This is especially useful since GRAM is developed from and tested against the graphing activities of our team. Second, it allows "near natural language" reading of the graph. The information contained in the graph can thus be understood by anyone by maintaining a layer of translation alongside the emic expressions of the sources. We found this to be critical for collective research. Third, the LPG model allows to structure entities in a way historians are used to. Rather than fully atomizing each element of an entity into related nodes containing one single bit of information, it allows to add structural properties to nodes and relations. The risk, however, is to overload the graph at the expense of the efficiency of the queries. Yet making verbs and verbal expressions first-class citizens in a graph data model seems to offer a more tailored solution to modelling historical information and to implementing the verb-oriented method.

### Why GRAM?

Although it allows researchers to explore data visually and although it was initially developed to serve a comparative social history project with a specific question in mind, GRAM is neither a research method nor an analytical visualization tool. GRAM is first and foremost a data framework. It is designed to record information derived from historical documents, to structure it in a particular way, and to serve data for further analysis. As an "agnostic" data framework, GRAM stands apart from the research projects, from their questions, and from the methods used to analyse the data. Its strength, we would argue, is its level of granularity. Unlike other frameworks developed for historical research that adapt the lens to the observation and to predetermined questions, GRAM adapts the lens to the sources and seeks to capture their texture, in the language of the sources and with respect for the changing nature and messiness of the social. This is what makes GRAM versatile and multifunctional. GRAM's focus on the density of the sources, on local configurations and on the trajectories and interactions of social actors also make it well-suited as a tool for the kind of experimentation encouraged by microhistorians — it suggests a microhistorical approach that does "not renounce formalization and modeling."[^2]

## GRAM's Development Plan

GRAM entered its second phase in 2024. Its underlying principles and fundamental rules were established and tested in a first phase—which corresponds to the end of the COST Action CA18205 (until March 2024). Phase 2 has two main objectives: 

1. Refining the model and its vocabulary—in particular by reusing and incorporating classes and subclasses of existing open vocabularies (reuse being crucial to ensure interoperability)—but with an eye on maintaining the minimalism of the model and on avoiding the pitfalls of preimposed categorization and standardization; 
2. Testing the flexibility and robustness of the model, in particular against newly introduced relations (the challenge being to not overloading the graph and to keep the `(Action)-[HAS_ACTOR_WITH_ROLE]->(Actor)` as its main structural element). 

One of GRAM's guiding principles is to take a bottom-up and collaborative approach. Phase 2 thus involves increased individual graphing activities and collective discussions—which will take place in a bi-monthly seminar. New node labels, relation types, and properties are derived from the graphing activities of individual researchers and decided collectively. The `ISSUES.md` file in this repository is meant to record all the problems that we encounter in our graphing activities and that we need to collectively address. It documents our decisions for our future selves and for people who would like to evaluate our decisions and the framework itself. Phase 2 also involves opening the discussion to a larger pool of researchers with experience in digital humanities and interested in GRAM's underlying concepts.

### Prospects and Challenges of an Action-Centric Graph Framework

At the present stage of development and testing, the basic `(Action)-[HAS_ACTOR_WITH_ROLE]->(Actor)` data structure has proved efficient to ingest data from a wide array of historical sources, to query the graphs and to answer research questions. However, we are aware of the intial limitations and of the numerous issues that we will have to face when we refine the vocabulary. The data model is particularly efficient to graph concrete and explicit information related to what people did to and in relation to others. Context (legal, political, cultural, economic, social, etc.), on the other hand, is more difficult to integrate; as are expressions of causality and motivations. When encountered, value judgments and utterances of the actors about acts and behaviors of others have also raised new graphing issues. The project which GRAM is developed for (but which remains distinct from GRAM) uses judicial sources from very different historical contexts. Working such texts, (legal) reasoning is an important element to be taken into consideration as it not only conveys contextual norms but is also an act of power in itself and an exercise of social and political engineering. In the same manner, the genre of a source, its narration and the positionality of its authors have to be conveyed in the graph, in particular for the sake of connection and comparison. 

Most of the already identified and future issues will certainly find solutions with the reuse of existing ontologies and open vocabularies; and through enrichment activities. Other issues (like the interpretation or the recording of implicit actions) will require more carefully evaluated decisions to find the right balance between maintaining the efficiency of the data model and fine-grained levels of recording.

## GRAM's Core Principles

### GRAM's Three Golden Rules

#### 1. Transparency and Traceability

GRAM is built on a handful of rules and guiding principles, the first among which are transparency and traceability: information recorded in the graph must be traceable and true to the source document it was extracted from. As a sematic-informed model, GRAM follows the principles of Claire Lemercier and Claire Zalc to "respect the language and details of the source material" and to distinguish "input" from "categorization".[^3] GRAM is first and foremost a data input model that records information as much as possible *as in the source material and without interpreting*. This does not mean that the data is independent of interpration. Users can absolutely decide to include their own categorization schemes in the database structure, if they choose to. But that interpretative choices, when included in the database, must be made explicit (at least in the project documentation).

#### 2. Bottom-up Graphing and Collective Deliberation

The second set of guiding principles are collective deliberation and bottom-up approach. Decisions leading to the addition of new labels, types and properties to the framework come from our individual graphing attempts, but they must be addressed and solved collectively; as they must be documented.

#### 3. Minimality

The third guiding principle of GRAM is that—for the sake of efficiency and predictability—the framework should be kept as minimal as possible. 

- First, there should be as little variation from the `(Action)-[HAS_ACTOR_WITH_ROLE]->(Actor)` structure as possible; 
- Second, a clear distinction should be made (and maintained in the documentation) between the labels and properties that are part of the framework and those that are used for project-specific categorization and data extraction. Once sources are ingested into the graph using the GRAM framework, users are free to elaborate their own categorization scheme to facilitate the analyses they want to make by adding their own labels and properties. In this respect, an efficient way to identify the data relevant to a particular research question is to flag (by adding research-related labels to) the relevant entities identified by the researchers. In all cases, labels used to flag data that are relevant to specific questions and projects, as well as project-specific categorizations should be recorded in project documentations, not in the GRAM documentation.

### GRAM's Node Labels and Relation Types

`Node labels` are the main entry points into the graph, while `relation types` form the pathways that allow queries to traverse a graph. Both should thus be primarily used for grand categorization of the entities in the graph (instead of properties).

### GRAM's Node and Relation Properties

In order to ensure that data is recorded in ways that allow for change over time, we conceive of a key difference between node and relation properties.

Node properties are used to structure coherent and *unchanging* entities. They only record the permanent attributes of entities, be they Actions, Actors, Places, etc. For instance, a Place node might record the different names, the geographic coordinates, and the type of a polity, as long as its core characters remain unchanged. If its territory expands or if its political function changes, for instance, then a new entity, related to the first one, shall be created (as is usual practice in historical gazetteers).

Relation properties only record *non-permanent* attributes that are meaningful in the context of a specific action (they are relational). A typical example is the status or occupation of a person. Since status and occupation can change over time (and also be plural for a same person at one point in time), they cannot be considered as permanent attributes of a Person entity. They might, however, be important to understand the role of an actor in an event and be recorded as a property of the role relation between the Actor and the Action.

### Interoperability

The Label Property Graph focuses more on data recording and exploration than on data exchange. However, we as much reuse of existing ontologies and vocabularies as possible in order to improve interoperability. This might include such ressources as:

- The [Linked Open Vocabularies](https://lov.linkeddata.es/dataset/lov/) portal. [CIDOC-CRM](https://www.cidoc-crm.org/), with its underlying concept that everything is an event, can be used as a reference ontology to draw inspiration from. It could serve as a means to standardize data and improve its interoperability. As reference to CIDOC-CRM, we rely on the ONTOME [Definition of the CIDOC Conceptual Reference Model](https://ontome.net/namespace/7)
- Depending on the historical contexts of the data, we encourage use of existing reference biographical databases and gazetteers, invluding
  - [World Historical Gazetteer](https://whgazetteer.org/search/) for a general reference for place names and georeferencing.
  - For late imperial China, we rely on the [China Biographical Database](http://db1.ihp.sinica.edu.tw/cbdbc/ttsweb?@0:0:1:cbdbkmeng@@0.9431388692648304) and on the [China Historical GIS](https://chgis.fas.harvard.edu/search/?)
- It might often also be of use to adopt widely-used historical standard vocabularies:
  - For instance, it might prove valuable to repurpose elements of the [Historical International Standard Classification of Occupations (HISCO)](https://iisg.amsterdam/en/hsndb/standardized-occupations) which is widely used in historical digital projects.

## GRAM's Conventions

### Null Values

As a rule, unknown values—i.e., the absence of information—*are not recorded*. We do not use notations such as "unknown" or "n/a" (for instance when the gender of a Person entity cannot be decided). The absence of information will be rendered as `null` values when querying the graph. This should be kept in mind when reusing the data with third-party analytical tools that may skip observations containing null values, like the R package ggplot.

### Dates and Time

With regard to date notations, we implement [neo4j's standards](https://neo4j.com/docs/cypher-manual/current/functions/temporal/) so that we can use its temporal analysis functions. Date notations are a crucial part of historical databases and a constant issue. Neo4j can accommodate dates, timestamps, and durations. Date and time property values can be declared by using the `date()`, `dateTime()`, `time()`, and `duration()` functions (cf. [Cypher documentation](https://neo4j.com/developer/cypher/dates-datetimes-durations/)). 

GRAM essentially uses the `date()` function, to record either a moment in time (mainly when an Action takes place) or the time boundaries of an enduring Action (or of the period of existence of an Actor entity, like the dates of birth and death of a person, or the dates of existence of an institution). Dates often being fuzzy and approximate in history, date properties can be coupled with a `date qualifier` property when necessary. Date qualifiers also serve to specify whether a date record is precise to the day, the month or the year, because Cypher automatically sets unknown months to January and unknown days to the first day of the month (e.g., when recording `1700` as the date when an action took place, Cypher will set it, in ISO format, to `1700-01-01`). In addition, we also use `Latest` and `Earliest` as specifiers of relative dates property key. 

#### Points in Time

Points in time (be they exact to the day, month or year, and be they approximate or not) are recorded under a `date` property key, with the only exception of Person entities, whose dates of birth and death are recorded under `dob` and `dod` properties:

| Point in time property keys | Point in time property values | description |
| :--- | :--- | :--- |
| `date` | `yyyy-mm-dd` | point in time when the action takes (or is said to take) place |
| `dob` `dob` | `yyyy-mm-dd` | known date of birth or death of a person |
| `dateQualif` | `circa`; `day`; `month`; `year` |qualifier of a date property, when necessary |
| `dobQualif` `dodQualif` | `circa`; `day`; `month`; `year` | qualifier of a date of birth/death property, when necessary |

#### Relative Points in Time

Oftentimes, historical sources only allow us to situate a point in time relative to another. In some cases, we are able to compute those relative dates as points in time, as when an action is said to have taken place "one year after" a specified date. In such a case, we record the computed date as a point in time, but we may want to add a `circa` date qualifier value in the record. In cases where such computation is impossible, we do not use "before" or "after" date qualifiers. Instead, we use `dateEarliest` and `dateLatest` properties (except in the case of dates of birth and death of Person entities for which we will simply use a `circa` date qualifier). `dateQualif` properties are not used with `dateEarliest` and `dateLatest` properties. 

| Relative point in time property keys | Relative point in time property values | description |
| :--- | :--- | :--- |
| `dateEarliest` | `yyyy-mm-dd` | earliest point in time when the action takes (or is said to take) place |
| `dateLatest` | `yyyy-mm-dd` | latest point in time when the action takes (or is said to take) place |

#### Durations

If time information relates to a set duration (i.e., it has a starting and ending time), we have two options, depending whether the time bouncdaries are exact or relative:

1. We use pairs of `dateStart` and `dateEnd` properties (exact or approximate) with the `date()` declaration (possibly coupled with a duration property calculated from those two dates) in cases where the two time boundaries are not relative points in time. In such cases, `dateStartQualif` and `dateEndQualifs` can also be used:

| Non-relative enduring date property keys | Non-relative enduring date property values | description |
| :--- | :--- | :--- |
| `dateEnd` | `yyyy-mm-dd` | end point of a period |
| `dateEndQualif` | `circa`; `day`; `month`; `year` | qualifier for the end point of a period, if necessary |
| `dateStart` | `yyyy-mm-dd` | starting point of a period |
| `dateStartQualif` | `circa`; `day`; `month`; `year` | qualifier for the starting point of a period, if necessary |
| `duration` | {duration declaration} | duration of an action: as specified in the source when time boundaries are not provided (e.g., `duration({years: 3})`); or calculated from time boundaries |

2. Or we use pairs of `dateEndEarliest`/`dateStartEarliest` `dateEndLatest`/`dateStartLatest` properties:

| Relative enduring date property keys | Relative enduring date property values | description |
| :--- | :--- | :--- |
| `dateEndEarliest` | `yyyy-mm-dd` | earliest end point of a period |
| `dateEndLatest` | `yyyy-mm-dd` | latest end point of a period |
| `dateStartEarliest` | `yyyy-mm-dd` | earliest starting point of a period |
| `dateStartLatest` | `yyyy-mm-dd` | latest starting point of a period |

## Content

The node (vertices) `labels` and relation (edges) `types` currently used to structure the data, as well as their basic `properties`, and some of their possible values are described in detail in two separate documents: `GRAM_nodes.md` and GRAM_relations.md. The repository also contains project-specific folders meant to host project descriptions, vocabularies, queries, datasets and more.

[^1]: Jean-Pierre Dedieu, [Designing databases for historical research. With special reference to Fichoz](https://reshist.hypotheses.org/files/2016/07/Dedieu_Historical_Databases.pdf) (accessed 04/07/2022); Mark Merry, [Designing databases for historical research](https://port.sas.ac.uk/mod/book/view.php?id=75) (accessed 04/07/2022).

[^2]: Here, we follow Claire Lemercier and Claire Zalc's remarks on the cross-fertilization of quantitative/formalization methods and microhistory, especially as a means to ask new questions and to make our "interpretative game explicit". See Claire Lemercier and Claire Zalc, *Quantitative Methods in the Humanities*, Charlottesville: University of Virginia Press, 2019, p. 32.

[^3]: Claire Lemercier and Claire Zalc, *Quantitative Methods in the Humanities*, Charlottesville: University of Virginia Press, 2019, p. 63.
