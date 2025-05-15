### Contextual Model of The Shepherdess using RDF
![The contextual model of The Shepherdess using RDF](images/example_rdf.png)
*Figure 1. RDF representation of the The Shepherdess*

``` turtle
# Artwork connected to Creation event
<#TheShepherdess> <hasEvent> <#Creation> .

# Creation event information
<#Creation> <createdBy> <William-Adolphe Bouguereau> .
<#Creation> <arto:hasTime> <1889> .

# Artist information
<William-Adolphe Bouguereau> <hasEvent> <#Birth> .
<William-Adolphe Bouguereau> <hasEvent> <#Teaching> .
<William-Adolphe Bouguereau> <hasEvent> <#MoveHouse> .

# Birth event information
<#Birth> <arto:hasLocation> <#LaRochelle> .
<#Birth> <arto:hasTime> <30 November 1825> .

# Teaching event information
<#Teaching> <teachAt> <Académie Julian> .
<#Teaching> <arto:hasLocation> <#Paris> .
<#Teaching> <arto:hasTime> <1860> .

# Move event information
<#MoveHouse> <arto:hasLocation> <#Paris> .
<#MoveHouse> <arto:hasTime> <March 1846> .

# Academic institution events
<Académie Julian> <hasEvent> <#Creation> .
<#Creation> <arto:hasLocation> <#Paris> .
<#Creation> <arto:hasTime> <1867> .
```