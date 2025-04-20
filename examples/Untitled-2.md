
# Why Create a New ARTO Ontology Instead of Extending Existing Ones

## Structural Mismatch

Existing cultural heritage ontologies (such as CIDOC-CRM) are primarily designed for museum management and artifact cataloging, with core concepts centered around physical objects, events, and actors. However, art annotation requires capturing visual elements, composition, emotions, and symbolic meanings—aspects that lack appropriate conceptual foundations in existing ontologies. ARTO's four-layer structure (visual elements, objects, scenes, connotations) is specifically designed for art content representation. This hierarchical structure fundamentally differs from the organizational approaches of existing ontologies, making it difficult to implement through simple extensions.

## Practicality and Performance Considerations

Directly extending large existing ontologies (like CIDOC-CRM) would add unnecessary complexity. As mentioned in your paper, "following the KISS principle," creating a more concise ontology for specific use cases is often more effective than extending a large, complex one. Annotation systems need to frequently query and process art content information. Adding detailed art content representations to a large general ontology would reduce query and reasoning efficiency, while a specially designed ontology can optimize these operations.

## Community and Application Requirements

The primary users of existing ontologies (such as museum workers, artifact managers) have different needs and technical backgrounds compared to ARTO's target users (such as art annotation system developers, AI researchers). A new ontology can better meet the needs of specific user groups. ARTO needs to adapt to modern AI technologies like large language models and computer vision, which may be incompatible with the design of existing ontologies.

## Balancing Semantic Interoperability

Creating a new ontology allows you to establish a semantically more consistent and complete framework without compromising on concept definitions that might not fully fit in existing ontologies. By establishing a new ontology and defining mapping relationships with existing ones (as you've done), you can maintain semantic clarity in both domains while still achieving interoperability. This approach is more conducive to accurate semantic expression than direct extension. The new ontology can use terminology and relationships more aligned with art description and annotation domain conventions, without having to follow the potentially more academic or abstract naming conventions of existing ontologies.