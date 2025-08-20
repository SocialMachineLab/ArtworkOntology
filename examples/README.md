# Artwork Object Ontology Examples

This document demonstrates how various artworks can be represented using the ARTO (ARTwork object Ontology) framework through concrete examples. Each example shows how both descriptive content and contextual information can be captured in a structured manner.


## Comparison Across Art Forms

These examples demonstrate how ARTO can be applied to diverse art forms while maintaining a consistent ontological framework:

| Artwork | Medium | Descriptive Focus | Contextual Focus |
|---------|--------|-------------------|------------------|
| Composition II | Abstract Painting | Geometric elements, colour relationships | De Stijl movement, modernism |
| The Thinker | Sculpture | Posture, physicality, bronze material | Gates of Hell commission |
| The Greeting | Video Art | Temporal sequence, emotional progression | Renaissance influence, technical specs |
| The Shepherdess | Painting | Rural figure, pastoral symbolism | 19th century French context |


Despite these artworks differing in medium and form, ARTO offers a unified representation method for all. Whether dealing with two-dimensional paintings, three-dimensional sculptures, or time-based video art, ARTO captures both their attributes and visual features. This flexibility makes ARTO a truly comprehensive artwork representation framework capable of adapting to the diversity and complexity of the art domain.


The complete RDF-star and RDF representations of these examples are available as `.ttl` files in this directory:
- [arto_abstract_composition_ii.ttl](./arto_abstract_composition_ii.ttl)  
- [arto_sculpture_the_thinker.ttl](./arto_sculpture_the_thinker.ttl)  
- [arto_video_the_greeting.ttl](./arto_video_the_greeting.ttl)  
- [arto_TheShepherdess.ttl](./arto_TheShepherdess.ttl)



> **Note:** Some properties shown in the examples (e.g., `arto:talkTo`, `arto:whisper`, `arto:greets`, `arto:ignores`) are illustrative extensions used to demonstrate the expressive power of RDF-star for interaction modelling. They are **not** part of the core ARTO ontology (`arto.ttl`). For the official class and property definitions, please refer to the main ontology file [`arto.ttl`](../arto.ttl).

## Composition II with Red, Blue and Yellow (Piet Mondrian, 1930)

![Composition II with Red, Blue and Yellow by Piet Mondrian](../images/composition_ii.jpg)

"Composition II with Red, Blue and Yellow" is an iconic abstract painting by Dutch artist Piet Mondrian, characterised by its geometric composition of primary colours and black grid lines on a white background. This work exemplifies Mondrian's neoplasticism style.

### Contextual Model Representation

![ARTO Contextual Model of "Composition II"](../images/abstract_1.png)

### Descriptive Model Representation

![ARTO Descriptive Model of "Composition II"](../images/abstract_2.png)


```turtle
:composition_ii a arto:Painting ;
    dc:title "Composition II in Red, Blue, and Yellow"@en ;
    dc:creator :mondrian ;
    arto:style :neoplasticism ;
    arto:genre :Abstract_art ;
    arto:containsScene :main_scene .

:main_scene a arto:Scene ;
    arto:containsObject :red_rectangle , :blue_rectangle , :yellow_rectangle ;
    arto:hasConnotation :universal_balance .

:red_rectangle a arto:Object ;
    arto:containsElement :red_colour ;
    arto:hasConnotation :energy_warmth .

```


## The Thinker (Auguste Rodin, 1880-1881)

![The Thinker by Auguste Rodin](../images/Musée_Rodin_1.jpg)

"The Thinker" is one of Auguste Rodin's most famous bronze sculptures, depicting a nude male figure in deep contemplation. Originally titled "The Poet," it was conceived as part of Rodin's larger work "The Gates of Hell," inspired by Dante's Divine Comedy.

### Contextual Model Representation

![ARTO Contextual Model of "The Thinker"](../images/the%20thinker_1.png)


### Descriptive Model Representation

![ARTO Descriptive Model of "The Thinker"](../images/the%20thinker_2.png)


```turtle
:the_thinker a arto:Sculpture ;
    dc:title "The Thinker"@en ;
    dc:creator :auguste_rodin ;
    arto:medium aat:300010957 ;         # Bronze
    arto:technique :Lost-wax_casting ;
    arto:style :Neoclassicism ;
    arto:containsScene :contemplation_scene .

:contemplation_scene a arto:Scene ;
    arto:containsObject :male_figure ;
    arto:hasConnotation :philosophical_contemplation_theme .

:male_figure a arto:Object ;
    arto:state "Seated, contemplative pose" ;
    arto:material aat:300010957 ;
    arto:containsElement :flesh_texture .
```


## The Greeting (Bill Viola, 1995)

![The Greeting by Bill Viola](../images/thegreeting.jpg)

"The Greeting" is a video art installation by Bill Viola, inspired by Pontormo's 16th century painting "The Visitation." The work shows an encounter between three women in extreme slow motion, stretching a 45-second action to 10 minutes, allowing viewers to observe subtle emotional changes.

### Contextual Model Representation

![ARTO Contextual Model of "The Greeting"](../images/greeting_1.png)

### Descriptive Model Representation

![ARTO Descriptive Model of "The Greeting"](../images/greeting_2.png)



<div style="text-align: center;">
  <img src="../images/greeting_3.png" alt='ARTO Descriptive Model of "The Greeting"' style="width: 60%; ">
</div>

``` turtle
<< ex:WomanOne arto:isObjectOf ex:InitialConversationScene >> 
    arto:state "Standing and conversing" ;
    arto:talkTo << ex:WomanTwo arto:isObjectOf ex:InitialConversationScene >> .

<< ex:WomanTwo arto:isObjectOf ex:InitialConversationScene >> 
    arto:state "Standing and conversing" ;
    arto:talkTo << ex:WomanOne arto:isObjectOf ex:InitialConversationScene >> .
```


<div style="text-align: center;">
  <img src="../images/greeting_4.png" alt='ARTO Descriptive Model of "The Greeting"' style="width: 60%; ">
</div>

``` turtle
<< ex:WomanOne arto:isObjectOf ex:ApproachScene >> 
    arto:state "Turning body" .

<< ex:WomanThree arto:isObjectOf ex:ApproachScene >> 
    arto:state "Entering" ;
    arto:approach << ex:WomanOne arto:isObjectOf ex:ApproachScene >> .
```

<div style="text-align: center;">
  <img src="../images/greeting_5.png" alt='ARTO Descriptive Model of "The Greeting"' style="width: 60%; ">
</div>

``` turtle
<< ex:WomanOne arto:isObjectOf ex:GreetingMomentScene >> 
    arto:state "Hugging" .

<< ex:WomanTwo arto:isObjectOf ex:GreetingMomentScene >> 
    arto:state "Feeling excluded" .

<< ex:WomanThree arto:isObjectOf ex:GreetingMomentScene >> 
    arto:state "Hugging" ;
    arto:greets << ex:WomanOne arto:isObjectOf ex:GreetingMomentScene >> ;
    arto:ignores << ex:WomanTwo arto:isObjectOf ex:GreetingMomentScene >> .
```

<div style="text-align: center;">
  <img src="../images/greeting_6.png" alt='ARTO Descriptive Model of "The Greeting"' style="width: 60%; ">
</div>

``` turtle
<< ex:WomanTwo arto:isObjectOf ex:WhisperingScene >> 
    arto:state "Feeling excluded" .

<< ex:WomanThree arto:isObjectOf ex:WhisperingScene >> 
    arto:whisper << ex:WomanOne arto:isObjectOf ex:WhisperingScene >> .
```

<div style="text-align: center;">
  <img src="../images/greeting_7.png" alt='ARTO Descriptive Model of "The Greeting"' style="width: 60%; ">
</div>

``` turtle
<< ex:WomanOne arto:isObjectOf ex:IntroductionScene >> 
    arto:state "Talking and awkwardness" .

<< ex:WomanTwo arto:isObjectOf ex:IntroductionScene >> 
    arto:state "Talking and awkwardness" .

<< ex:WomanThree arto:isObjectOf ex:IntroductionScene >> 
    arto:state "Talking and awkwardness" .
```



## The Shepherdess
![The picture of the artwork "The Shepherdess"](../images/example.jpg)

"The Shepherdess", also known as "The Little Shepherdess", is a painting by William-Adolphe Bouguereau completed in 1889. The title is taken from the Southern French dialect. The painting depicts an idyllic, pastoral scene of a lone young woman in peasant attire posed for the artist, balancing a stick (likely her crook) across her shoulders, standing barefooted in the foreground. In the background are oxen grazing in a field.


### Contextual Model of The Shepherdess using RDF-star
![The contextual model of The Shepherdess using RDF-Star](../images/example_rdfstar.png)

### Contextual Model of The Shepherdess using RDF
![The contextual model of The Shepherdess using RDF](../images/example_rdf.png)

### Descriptive Model of The Shepherdess
![The Descriptive model of The Shepherdess](../images/example_adm.png)




