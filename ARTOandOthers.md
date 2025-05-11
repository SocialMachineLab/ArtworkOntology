# ARTO vs Other Artwork Ontologies: Comparison of Representational Capabilities


This document demonstrates how ARTO (ARTwork Object Ontology) differs from existing artwork ontologies in representing artwork information. Through these examples, we show ARTO's enhanced capabilities in capturing visual details, emotional content, and multi-layered interpretations.

## Comparison with Major Ontologies

For detailed information, please see [here](./examples/)

### ARTO vs CIDOC-CRM

**CIDOC-CRM Focus:**
- Cultural heritage documentation
- Provenance and historical events
- Basic artwork metadata

**ARTO Advantages:**
- Hierarchical scene-object-element structure
- Emotional and connotative expression
- Detailed compositional analysis

#### Example

##### 1. Depth and Hierarchy of Content Expression


```turtle
# CIDOC-CRM - Can only simply list depicted content
crm:P62_depicts ex:night_sky, ex:village, ex:cypress_tree, ex:church_spire ;


# ARTO - Multi-level structured expression
ex:starry_night arto:containsScene ex:sky_scene, ex:village_scene ;

ex:sky_scene arto:containsObject ex:stars, ex:moon, ex:swirls ;
    arto:expresses ex:emotion_turmoil ;
    arto:hasMetric ex:blue_dominance .

ex:swirls arto:containsElement ex:blue_color, ex:curved_line ;
    arto:expresses ex:emotion_turmoil .
```


##### 2. Expression of Inter-object Relationships


```turtle
# CIDOC-CRM - Simply lists objects without expressing their relationships
crm:P62_depicts ex:night_sky, ex:village, ex:cypress_tree, ex:church_spire ;

# ARTO - Rich relationship network
ex:houses arto:relatedTo ex:church ;
ex:cypress arto:isObjectOf ex:village_scene ;
ex:swirls arto:expresses ex:emotion_turmoil ;
ex:stars arto:isObjectOf ex:sky_scene ;
```

### ARTO vs ICON Ontology

**ICON Focus:**
- Panofsky's interpretation levels
- Iconographic recognition
- Symbolic content identification

**ARTO Advantages:**
- Spatial relationships between objects
- Quantitative metrics and measurements
- Scene coherence and atmosphere

#### Example

##### 1. Hierarchical Scene Structure

ARTO offers a sophisticated scene-object hierarchy that ICON cannot represent:

```turtle
# ARTO - Nested scene structure
ex:starry_night arto:containsScene ex:sky_scene, ex:village_scene .
ex:sky_scene arto:containsObject ex:stars, ex:moon, ex:swirls .
ex:swirls arto:containsElement ex:blue_color, ex:curved_line .

# ICON - Flat structure with limited relationships
ex:village_composition icon:hasPart ex:church_motif, ex:houses_motif .
```

##### 2. Object State and Attributes

ARTO describes object characteristics in detail:

```turtle
# ARTO
ex:stars 
    arto:size "Small" ;
    arto:state "Glowing" .
    
ex:cypress 
    arto:size "Large" ;
    arto:material "Plant matter" .

# ICON - Basic labeling only
```


##### 3. Quantitative Visual Information

ARTO provides measurable properties for visual elements:

```turtle
# ARTO - Specific measurements
ex:curved_line rdf:type arto:Line ;
    arto:direction "Curved" ;
    arto:length 20.0 ;
    sdo:width "Medium" .

# ICON - No geometric properties available
```


### ARTO vs VIR (Visual Representation Ontology)

**VIR Focus:**
- Visual heritage elements
- Iconographic attributes
- Formal motif recognition

**ARTO Advantages:**
- Dynamic element description (movement, direction)
- Sensory details (material, color values)
- Comprehensive composition analysis

#### Example

##### 1. Hierarchical Structure and Clarity

ARTO provides a clear three-level hierarchy: Artwork → Scene → Object → Element, making the structure immediately understandable.


```turtle
# ARTO
ex:starry_night arto:containsScene ex:sky_scene, ex:village_scene ;
ex:sky_scene arto:containsObject ex:stars, ex:moon, ex:swirls ;
ex:stars arto:containsElement ex:yellow_color, ex:circular_composition ;

# VIR
ex:starry_night_representation vir:K20_forms_part_of ex:sky_representation ;
ex:sky_representation vir:K17_has_attribute ex:swirl_attribute ;
```


##### 2. Rich Descriptive Properties


```turtle
# ARTO provide details about the object
ex:swirls rdf:type arto:Object ;
    arto:size "Large" ;
    arto:descriptor "Swirling" ;
    arto:coordinates "Upper region" ;
    arto:state "Dynamic motion" ;
    arto:containsElement ex:blue_color, ex:curved_line ;
```


### 3. Object Relationships

ARTO can express spatial and conceptual relationships between objects directly.

**ARTO's Advantage:**
```turtle
ex:cypress ex:next_to ex:church .
ex:houses arto:adjacent_to ex:church ;
```



### ARTO vs ArCo

**ArCo Focus:**
- Italian cultural heritage cataloging
- Conservation status
- Cultural-historical context

**ARTO Advantages:**
- Dynamic narrative expression
- Artistic technique details
- Psychological and emotional content

#### Example





### ARTO vs Linked Art

**Linked Art Focus:**
- Standardized data model
- Interoperability
- Basic visual items

**ARTO Advantages:**
- Detailed artistic technique representation
- Dynamic element description
- Color-emotion associations

#### Example








## Key Differentiators
| Feature                 | CIDOC-CRM | ICON    | VIR     | ArCo    | Linked Art | ARTO           |
|-------------------------|-----------|---------|---------|---------|-------------|----------------|
| Visual Details          | Basic     | Limited | Limited | Limited | Basic       | Comprehensive  |
| Emotional Expression    | No        | Limited | No      | No      | No          | Yes            |
| Object Relationships    | Limited   | No      | Limited | No      | Limited     | Yes            |
| Metrics                 | No        | No      | Limited | Limited | No          | Yes            |
| Multi-layer representation | No    | Limited | No      | No      | No          | Yes            |

