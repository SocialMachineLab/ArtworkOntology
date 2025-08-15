## Versioning

### ARTO CREATION
*Version 0.1 | Date: 2024-02-05*

The initial version of ARTO introduced the *Artwork Contextual Model* and *Artwork Descriptive Model*. The *Artwork Contextual Model* consist of five main classes (Artwork, Event, Location, Time, Agent), capturing essential background information including artwork metadata, historical events with time and location and related agent relationships. The *Artwork Descriptive Model* established a four-level hierarchical framework that represents artwork content from basic visual elements (colours with RGB/HSV values, lines, composition) to objects (with properties like size, material, state) to scenes (meaningful groupings of objects) to high-level connotations (symbolism, emotion, theme). A decision was made to incorporate RDF-star to simplify complex relationship representation, particularly valuable for modelling interconnected events, people, locations, and times. The main focus of ARTO is defined as a unified framework designed for comprehensive artwork representation rather than cataloguing, offering machine-understandable representations that support artwork captioning, analysis, and information retrieval.


### Theoretical foundation of ARTO - The Panofsky iconographic levels
*Version 0.1.1 | Date: 2024-06-05*

ARTO's design is now informed by Panofsky's influential three-level method of art interpretation, while extending this classical framework to meet the requirements of digital representation and computational analysis. Table [1](#table1) illustrates and documents how ARTO maps to and extends Panofsky's interpretative layers. The pre-iconographic description corresponds to ARTO's VisualElement and Object classes, capturing the primary visual content. The iconographic analysis maps to ARTO's Scene class and object relationships, representing the identification of themes and conventional subject matter. And the iconological interpretation is represented through ARTO's Connotation class and its subclasses (Symbolism, Emotion, Theme), connecting visual content to deeper cultural meanings and historical context.

While grounded in Panofsky's theoretical framework, ARTO extend it in several ways for advanced computational analysis. First, it transforms these interpretative processes into machine-processable structured data that supports computational analysis and automated caption generation. Second, ARTO introduces the Metric class system, enabling quantitative representation of artistic features such as color distribution, compositional balance, and emotional intensity. Third, ARTO's scene-object-element hierarchy provides a more granular organization of visual content that facilitates both human understanding and machine processing, addressing the hierarchical relationships between visual elements that Panofsky's original framework did not explicitly model.



<a id="table1"></a>
| **Panofsky Level** | **Definition**                                               | **ARTO Components**                                          | **ARTO Extensions**                                          |
| ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Pre-iconographical | Identification of primary subject matter: factual and expressional forms | `VisualElement` class and subclasses (`Color`, `Line`, etc.) `Object` class | • Precise color representation (RGB/HSV values)<br>• Quantifiable visual attributes<br>• Object state and material properties |
| Iconographical     | Recognition of secondary subject matter: stories, allegories, personifications | `Scene` class and the relationships to `Connotation`         | • Hierarchical scene representation<br>• Connect `Scene` and `Object` to `Connotation` connections |
| Iconological       | Intrinsic meaning: cultural, historical, and symbolic values | `Connotation` class and subclasses (`Symbolism`, `Emotion`, `Theme`) Links to `Event` and contextual information | •  Quantifiable emotional intensity<br>• The connections from connotation to historical events |




### What artworks types are supported by ARTO?

*Version 0.1.2 | Date: 2024-09-24*


ARTO supports various visual art forms. The descriptive model has the ability to represent 2D visual arts (e.g., paintings, drawings, photographs), 3D sculptures, and time-based media like videos. The contextual model can also represent the basic information of these kind of arts.



### Reuse of existing ontologies

*Version 0.1.3 | Date: 2025-02-15*

Our latest ontology version has improved alignment with existing ontologies in the Art domain. We now have better integration with CIDOC-CRM, EDM, [ICON](https://w3id.org/icon/ontology/), and [Getty AAT](https://www.getty.edu/research/tools/vocabularies/aat/) vocabularies. The definition and scope of some properties are not exact match with our definition. Thus, we are also followed the "Keep It Simple, Stupid" design principle to create more lightweight, domain-specific classes for the art domain, while maintaining interoperability with existing ontologies through subclass relationships. 






### The use of controlled vocabularies vs the use of text literals

*Version 0.1.3 | Date: 2025-02-15*

The first version of ARTO relied on text literals but to enhance semantic interoperability and precision version 0.1.3 of ARTO incorporated controlled vocabularies from Getty AAT and ICONCLASS for representing art-related concepts.

 <!-- The latest version addresses this by incorporating controlled vocabularies from Getty AAT and ICONCLASS for representing art-related concepts. This shift from text literals to structured vocabulary terms enhances semantic precision and interoperability. -->


### Defined Competency Questions 

*Version 0.1.3 | Date: 2025-02-15*

The latest version includes [Competency Questions](#competency-questions) that outlines the types of queries ARTO supports. These include basic information queries, visual description queries, semantic interpretation queries, and contextual information queries, with specific examples provided. 



### Bidirectional queries

*Version 0.1.3 | Date: 2025-02-15*

Version 0.1 of ARTO did not explicit inverse relations. This has been added in version 0.1.3 for all significant object properties to enable bidirectional navigation through the knowledge graph. 
Example:
- `containsScene` / `isSceneOf`
- `containsObject` / `isObjectOf`  
- `containsElement` / `isElementOf`
- `hasPart` / `isPartOf`



### Maturity and Accessibility

ARTO has been under development since beginning of 2023 and we are constantly improving it. We have created more [examples](examples) here to showcase ARTO's capabilities. We are also constantly collecting expert feedback to better meet their needs. We have also created a pipeline for building knowledge graphs, which can extract entities and relations from text and store them in the knowledge graph. We are also continuously improving our algorithms to improve the quality and accuracy of the knowledge graph. We are also developing the pipeline for extracting knowledge graphs from the content of the artwork (images). And the webpage is accessible [here](website/Artwork%20Object%20Ontology.html). Contact the authors of this page if you want to [contribute](#how-to-contribute) to this project.




### Ontology Improvement, Vocabulary Enhancement, and Multi-Perspective Emotion Support
*Version 0.2 | Date: 2025-08-13*

Version 0.2 represents a comprehensive overhaul of ARTO that addresses critical integration issues while significantly enhancing the ontology's semantic precision and usability. This version resolves fundamental integration problems by importing all referenced external ontologies with their complete axioms and constraints, providing a solid foundation for semantic interoperability. All missing properties that appeared in documentation diagrams but were absent from the ontology file have been systematically implemented, including crucial spatial relationships like `arto:behind` and `arto:holds`, ensuring consistency between theoretical documentation and practical implementation.

The version significantly improves semantic precision by replacing problematic string literals with structured references to established controlled vocabularies. Following the "Keep It Simple, Stupid" principle established in version 0.1.3, this release adopts a pragmatic approach to external references, using local declarations for rarely-used concepts instead of importing entire ontologies, which reduces complexity while maintaining semantic clarity. Concepts such as genres, techniques, materials, and colors now link to standardized terminologies like Getty AAT rather than relying on free text representations, with the genre framework seamlessly integrated with Getty AAT's authoritative hierarchies while supporting custom definitions for emerging artistic practices. The color representation system has been streamlined to use string values with clear format specifications, eliminating complex mathematical vector representations while preserving analytical capabilities through a unified framework that connects computational color analysis with art historical interpretation via standardized color terminology (`arto:ColorTerm`), precise numerical representation (`arto:ColorValue`), and analytical metrics (`arto:ColorHistogram` and `arto:MainColor` classes).

The integration of the Mental Functioning Ontology Emotion Module (MFOEM) significantly enhances the semantic precision of emotion representation by providing standardized terminology, whereby arto:Emotion becomes a subclass of both arto:Connotation and mfoem:MFOEM_000001. Through this structural enhancement, the ontology enables standardized classification of both basic emotions (happiness, sadness, anger, fear, surprise, disgust) and complex emotions (love, anxiety, hope, despair, serenity) while using the `arto:emotionPerspective` property that distinguishes between artist's intended emotions, emotions expressed by the artwork itself, and viewer emotional responses. This multifaceted framework enables a clear and comprehensive representation of emotions in artworks from multiple perspectives, ensuring that different emotional dimensions are captured with appropriate semantic context and computational precision.