# Artwork Object Ontology (ARTO)

In this repo, you will find an [overview](#overview) of ARTO and its contextual and descriptive models, followed by an [example](#an-example-of-using-arto-to-represent-the-shepherdess-artwork) using RDF and RDF-star to demonstrate how ARTO can be used to represent artworks. A set of [queries and competency questions](./CompetencyQuestions.md) are also provided to support the use of ARTO.

We further explore the [literature](#unique-contributions-of-arto-in-relation-to-the-literature) to highlight ARTO’s unique aspects and compare it with major ontologies used to meta-represent artworks. Finally, we present how ARTO was [evaluated](#interview-arto-conceptual-evaluation).

You can track the evolution of ARTO and find answers to **frequently asked questions [here](ARTOVersioning.md)**. 

**Contributions to this project are welcome** — see more details [here](#how-to-contribute).

---





## Overview
![The Artwork Object Ontology](images/adm_acm.png)
*Figure 1. Overview of the ARTO Ontology*


The Artwork Object Ontology (ARTO) ([ARTO TTL file](v0.1/arto.ttl)) is a comprehensive ontology designed for describing and contextualizing artworks. It aims to provide a structured and detailed representation of artworks, facilitating tasks such as artwork captioning and information retrieval. 


ARTO consists of two main components briefly described as follows. 


The *Artwork Descriptive Model* is designed to encapsulate the representation of the content of artworks. It focuses on detailed content representation including visual elements, scenes, and emotional undertones that are conveyed through the artwork. This model aims to provide a framework that allows users to visually reconstruct the artwork and capture multiple perspectives and emotions related to and triggered by the artwork, which may foster a better understanding and representation of them.

![The Artwork Descriptive Model](images/aom.png)
*Figure 2. Overview of ARTO's Descriptive Model*

The *Artwork Contextual Model* complements the descriptive aspects by incorporating contextual information about the artwork. This model includes metadata, historical context, and related events, enriching the viewer’s appreciation and understanding of the artwork beyond its physical appearance.

![The Artwork Contextual Model](images/acm.png)
*Figure 3. Overview of ARTO's Contextual Model*

### Main highlights of ARTO

- An Artwork Descriptive Model for the representation of artistic expression of artworks, including visual elements, scenes, and emotions.
- An Artwork Contextual Model to capture background information such as related events about the artwork besides common artwork metadata.
- ARTO was created following a data-driven approach and standard ontology creation practices, incorporating concepts from established cultural heritage ontologies such as [CIDOC-CRM](http://www.cidoc-crm.org/cidoc-crm/) and [EDM](https://pro.europeana.eu/page/edm-documentation).
- ARTO has been validated using the [OntOlogy Pitfall Scanner (OOPS!)](https://github.com/oeg-upm/OOPS) and refined through interviews following a Think-Aloud Protocol with art experts.
- ARTO provides a comprehensive framework to represent diverse artwork types (e.g., paintings and sculptures) and support next-generation AI/ML applications in artwork captioning, retrieval, analysis, cataloguing, and recreation.
---
## An example of using ARTO to represent "The Shepherdess" artwork

![The picture of the artwork "The Shepherdess"](images/example.jpg)
*Figure 4. The picture of the artwork "The Shepherdess"*

To demonstrate the application of the ARTO models, consider Figure 4, the artwork “[The Shepherdess](https://www.wikiart.org/en/william-adolphe-bouguereau/shepherdess-1889)” by William-Adolphe Bouguereau (see more examples [here](examples/README.md)).

The Contextual Model provides insights into the painting’s creation in 1889, during the artist's life, reflecting the social and historical aspects of that era in France. 

> We use RDF-star to represent "The Shepherdess", specifically focusing on the Event class. Standard RDF increases modeling complexity due to its limitation to binary relationships (see [RDF example](RDFExampleContextualModel.md)).

### Contextual Model of The Shepherdess 

The Contextual Model illustrated in Figure 5 demonstrates how ARTO captures the historical context surrounding "The Shepherdess". Using RDF-star, this model efficiently represents complex relationships between the artist, locations, time periods, and events relevant to the artwork's creation. The graph shows William-Adolphe Bouguereau's life timeline, including his birth in La Rochelle in 1825, his move to Paris in March 1846, and his teaching activities at Académie Julian during the 1860s.  The model also captures the artwork's metadata including its style, dimensions, medium, genre, and its creation date. 

![The contextual model of The Shepherdess using RDF-Star](images/example_rdfstar.png)
*Figure 5. RDF-Star representation of The Shepherdess*

``` turtle
# Artist information
<#William-AdolpheBouguereau> <#bornOn> <#Time-30-November-1825> .
<<#William-AdolpheBouguereau> <#bornOn> <#Time-30-November-1825>> <arto:hasLocation> <#LaRochelle> .

# Artist's professional history
<#William-AdolpheBouguereau> <#teachingAt> <#AcadémieJulian> .
<<#William-AdolpheBouguereau> <#teachingAt> <#AcadémieJulian>> <arto:hasTime> <#Time-1860s> .
<<#William-AdolpheBouguereau> <#teachingAt> <#AcadémieJulian>> <arto:hasLocation> <#Paris> .

# Artist's activities
<#William-AdolpheBouguereau> <#moveTo> <#Paris> .
<<#William-AdolpheBouguereau> <#moveTo> <#Paris>> <arto:hasTime> <#Time-March-1846> .

# Creation place and time
<<#TheShepherdess> <#createdBy> <#William-AdolpheBouguereau>> <arto:hasTime> <#Time-1889> .
```

### Descriptive Model of The Shepherdess


The Descriptive Model shown in Figure 6 breaks down the visual content of "The Shepherdess" into a hierarchical structure of scenes, objects, and visual elements. There are two primary scenes: Foreground and Background. The Foreground scene contains key objects including a Young Woman (the shepherdess herself), a Bush, and a Stick that she holds. The Background contains secondary elements: Oxen grazing in a Field, along with Sky and Mountain elements. Each object is described through visual properties, relationships to other objects, and detailed attributes. For example, the Young Woman is "barefooted" and wears a "Rural dress with a plaid scarf," while also showing the spatial relationships between objects (the Bush is behind the Young Woman, who holds the Stick). Color elements are precisely represented for each object, creating a comprehensive visual representation that could support detailed artwork captioning or analysis.

![The Descriptive model of The Shepherdess](images/example_adm.png)
*Figure 6. RDF representation of The Shepherdess*

---

## Unique Contributions of ARTO in relation to the literature
ARTO's main contributions include integrating both descriptive content and contextual information into a unified framework, providing an ontological structure specifically for artwork caption generation.

Existing ontologies focus on museum management and artifact cataloging, while artwork captioning requires capturing detailed visual content and the relation to the context. ARTO‘s target users are artwork captioning developers and AI researchers who have distinctly different requirements compared to existing ontology users. ARTO users demand fine-grained artwork representations that are machine-understandable, enabling seamless integration into AI models for automated caption generation. They require representations that enable visual-semantic alignment and support the development of comprehensive, context-aware captions. These captions go beyond simply stating artworks' provenance, metadata, etc., instead encompassing detailed content representations and connecting them with cultural context and artistic interpretation. This shift from cataloging-oriented to content-analysis-oriented ontology reflects the evolving demands in digital art analysis and automated understanding systems.

The table below summarizes previous works in the field. The "Motivation for ARTO" column briefly introduces the need for ARTO (For detailed examples of ARTO and other ontologies, please see [here](./ARTOvsOthers.md)). 

| Name      | Domain           | Goal       | Ontology Scope                         | Strengths    | Motivation for ARTO                   |
|-----------|------------------|---------------------------|---------------------|--------------------------------------|-----------------------------------------------------------------------|
| CIDOC-CRM                                               | Cultural Heritage | To provide a theoretical and practical tool for integrating information in the cultural heritage domain, facilitating complex data queries and explorations. |  Events, actors, artifacts, and their relationships in cultural heritage contexts |  Comprehensive model, high-level data integration and retrieval |   Lacks detailed visual description capabilities for artwork content. ARTO provides comprehensive visual element representation (color, line, composition) and multi-level content modeling         |
| Visual Representation (VIR)                             | Visual Arts       | To extend CIDOC-CRM to describe the representation and relationships of visual features.                         | Visual elements, media, representation, and relationships        | Enhances visual data accessibility and retrieval                   | Lacks a multi-level representation structure and comprehensive contextual modeling. ARTO provides both detailed visual content representation and rich contextual information for artwork captioning. |
| Functional Requirements for Bibliographic Records (FRBR)| Bibliography      | To provide a comprehensive model for bibliographic records, focusing on the relationships between different entities such as works, expressions, manifestations, and items. | Bibliographic records, works, expressions, manifestations, items, and their relationships  | Clear structure for bibliographic data management               | Only cover bibliographic resources. ARTO provides detailed modeling for artworks                     |
| ArCo                                                    | Cultural Heritage | To describe and manage Italian cultural heritage, including artifacts, sites, and other cultural assets.                |  Italian cultural artifacts, heritage sites, and their relationships | Focused on Italian cultural heritage, detailed descriptions     | Focuses on cataloging Italian cultural heritage; ARTO provides a domain-agnostic framework for detailed artwork description |
| Europeana Data Model (EDM)                              | Digital Libraries | To provide a flexible framework for integrating and managing cultural heritage data from various sources across Europe.  |  Digital objects, metadata, cultural heritage collections, and their relationships  | Supports multilingual data integration  | Mainly for data organization and retrieval. ARTO offers in-depth content representation beyond basic metadata |
| Visual Resources Association Core (VRA CORE)            | Visual Resources  | To manage and describe visual resources, including images and visual works, in a standardized way.      | Visual works, images, titles, artistic styles, materials, etc.       | Improves visual data interoperability                           | Lacks descriptions of visual elements. ARTO provides detailed modeling of visual elements, objects and their connotations |
| ICON                                                    | Art History       | To catalog and describe iconographic content, including symbols, motifs, and other iconographic elements.               | Icons, symbols, motifs, background information, artwork interpretation                  | Specialized in iconographic data.           Facilitates iconographic research                               | Lacks multi-level representation for comprehensive artwork captioning. ARTO integrates descriptive, contextual, and interpretive information              |
| Art & Architecture Thesaurus (AAT)                      | Art & Architecture| To provide a structured vocabulary for art and architecture, including terms and concepts used in these fields.          | Art and architectural terms, concepts, and relationships       | Widely adopted in art and architecture communities. Enhances data consistency and retrieval                         | Need connect to other concepts to facilitate artwork captioning |
| Union List of Artist Names (ULAN)                       | Art               | To provide a structured and standardized list of artist names and biographical information.                             | Artist names, biographical data, and their relationships           | Standardized artist identification.   Enhances artist data accuracy and linkage                       | ULAN and AAT are controlled vocabularies rather than comprehensive frameworks. ARTO incorporates these vocabularies while providing structural modeling |
|  [Linked Art ](https://linked.art/)     | Art & Cultural Heritage | To link art data across different institutions and provide a comprehensive and interconnected view of art-related information. | Artworks, artists, events, and their relationships               | Facilitates cross-institutional data integration. Promotes data interoperability     | Focused on cross-institutional data integration rather than captioning. ARTO is specifically designed for comprehensive artwork description and captioning  |

---

## Interview: ARTO Conceptual Evaluation

Art experts verbally described some example artworks, labelling their own captions according to descriptive, contextual, and interpretive categories. The experts listed and ranked the aspects they considered most crucial when describing artworks, shared their approaches to describing art, and provided insights on depicting subjective elements like emotion and subject matter. They also outlined the most challenging elements to describe and their thoughts on verifying the accuracy of descriptions. Finally, after being introduced to the initial ontology design, the experts applied the new ontology to create captions for four artwork examples and assessed the comprehensiveness and structure of the generated content. You can access and check the detailed interview questionnaire and results in the folder [interview](/interview). 

---

## Application for ARTO: Pipeline to Artwork Image Captioning (ongoing work)
Integrating KG with artwork image captioning requires a systematic and clearly defined process. This pipeline elaborates on the steps involved, from initial analysis to the construction of the knowledge graph and the potential ways to collaborate with LLMs. The aim is to create a robust, scalable knowledge graph that aligns with the FAIR principles[^1] and apply it to the artwork image captioning task.

![The pipeline of integrating KG with artwork image captioning](images/pipeline.png)

- **Data Workflow**
  - **Data Sources**:  
    The available data sources are mainly from online museums or galleries. Given our goal to construct an artwork knowledge graph aimed at facilitating subsequent tasks related to artworks, especially the captioning of artwork images, we filter based on the information contained in the data sources. The available data sources are listed in Table 1.

  - **Data Processing**:  
    Given the vast and varied size of collected data, the Data Processing step is essential. It deals with inconsistencies, duplicates, and errors in the data, and standardizes the data format for the knowledge graph. This process ensures that only high-quality, reliable data is used for building the knowledge graph.

  - **Data Analysis**:  
    It's essential to conduct exploratory analysis in the data processing phase to identify errors and outliers within the data. Once the data is processed and cleaned, we then proceed with a descriptive analysis. This helps us understand the distribution, trends, and other characteristics of various attributes in the data, providing crucial insights to inform our ontology design decisions.

- **Ontology Design**:  
  According to the results of the data analysis, we collaborated with domain experts to define the main entities (e.g., people, places, and events) and establish a structured model that captures the relationships and hierarchies of these entities.

- **Knowledge Graph**:  
  In the knowledge graph construction phase, we process the cleaned data to identify and extract meaningful entities and their relationships, guided by our designed ontology. Our dataset primarily consists of metadata, which can be directly mapped, and text data, which necessitates the use of NLP techniques for entity extraction. Given the diverse origins of our data, inconsistencies often emerge, such as overlaps, contradictions, or varied representations of similar facts. To address these challenges and enrich our KG, we integrated trusted external resources like Wikidata and DBpedia. With these additions, we aligned with different sources, extended the information, and merged them to build a unified knowledge graph.

- **Knowledge Graphs work with LLMs**:  
  The combination of LLMs and KG provides a promising solution. LLMs could generate human-like text, while KGs offer structured knowledge about artworks. Together, they can generate captions that are coherent, contextual, and accurate.

[^1]: [FAIR principles](https://www.go-fair.org/fair-principles/)

--- 
## How to contribute?

To extend the Artwork Object Ontology (ARTO) for specific domains or use cases, follow these steps: First, identify the concepts, relationships, or properties that are not currently covered in ARTO. Next, design new classes to represent the missing concepts, ensuring consistency with ARTO's existing class hierarchy and naming conventions. Then, determine the new properties and relationships needed to capture additional information, specifying their data types, domains, ranges, and cardinality. Integrate the newly designed classes, properties, and relationships into ARTO's structure, update the documentation, and test the extended ontology with sample data to validate its effectiveness. Finally, maintain and update the extension over time to accommodate new requirements and feedback, ensuring compatibility with future versions of ARTO.



We welcome contributions to enhance and expand the *Artwork Object Ontology*. If you'd like to contribute, please follow these steps:

1. Fork the repository. 
2. Create a new branch for your feature or bug fix. 
3. Make your changes and commit them with descriptive messages. 
4. Push your changes to your forked repository. 
5. Submit a pull request detailing your changes and their benefits. 

--- 
## License

This project is licensed under the [MIT License](LICENSE).