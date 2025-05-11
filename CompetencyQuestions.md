
# Competency Questions | EXAMPLES OF SPARQL QUERIES

### 1. Basic Information Queries

- **CQ1.1**: What are the basic properties (title, year, dimensions, material) of a given artwork?
```sparql
PREFIX arto: <http://w3id.org/arto#>
PREFIX dc: <http://purl.org/dc/terms/>
PREFIX sdo: <https://schema.org/>

SELECT ?title ?year ?height ?width ?medium
WHERE {
    ?artwork a arto:Artwork ;
            dc:title ?title ;
            dc:medium ?medium ;
            sdo:height ?height ;
            sdo:width ?width .
    OPTIONAL { ?artwork dc:created ?year }
}
```
- **CQ1.2**: How can we retrieve all artworks by a specific artist?
```sparql
PREFIX arto: <http://w3id.org/arto#>
PREFIX dc: <http://purl.org/dc/terms/>

SELECT ?artwork ?title 
WHERE {
    ?artwork a arto:Artwork ;
            dc:title ?title ;
            dc:creator ?artist .
    ?artist a arto:Artist ;
            rdfs:label "Artist Name" .
}
```
- **CQ1.3**: What is the current location and collection information of an artwork?
```sparql
PREFIX arto: <http://w3id.org/arto#>
PREFIX dc: <http://purl.org/dc/terms/>

SELECT ?artwork ?title ?location ?locationType
WHERE {
    ?artwork a arto:Artwork ;
            dc:title ?title ;
            arto:currentLocation ?loc .
    ?loc a arto:Location ;
         dc:type ?locationType .
}
```
- **CQ1.4**: How should incomplete or uncertain information be handled?
```
PREFIX arto: <http://w3id.org/arto#>
PREFIX dc: <http://purl.org/dc/terms/>
PREFIX sdo: <https://schema.org/>
SELECT ?artwork ?missingProperty
WHERE {
    ?artwork a arto:Artwork .
    # Check required properties
    FILTER NOT EXISTS {
        { ?artwork dc:title ?title } UNION
        { ?artwork dc:creator ?creator } UNION
        { ?artwork dc:medium ?medium } UNION
        { ?artwork dc:description ?description } UNION
        { ?artwork sdo:height ?height } UNION
        { ?artwork sdo:width ?width } UNION
        { ?artwork edm:isShownBy ?image } UNION
        { ?artwork arto:style ?style } UNION
        { ?artwork sdo:genre ?genre } UNION
        { ?artwork arto:currentLocation ?location }
    }
    
    # Identify specific missing properties
    BIND(
        IF(!EXISTS { ?artwork dc:title ?title }, "Missing title",
        IF(!EXISTS { ?artwork dc:creator ?creator }, "Missing creator",
        IF(!EXISTS { ?artwork dc:medium ?medium }, "Missing medium",
        IF(!EXISTS { ?artwork dc:description ?description }, "Missing description",
        IF(!EXISTS { ?artwork sdo:height ?height }, "Missing height",
        IF(!EXISTS { ?artwork sdo:width ?width }, "Missing width",
        IF(!EXISTS { ?artwork edm:isShownBy ?image }, "Missing image",
        IF(!EXISTS { ?artwork arto:style ?style }, "Missing style",
        IF(!EXISTS { ?artwork sdo:genre ?genre }, "Missing genre",
        IF(!EXISTS { ?artwork arto:currentLocation ?location }, "Missing location",
        "Complete"))))))))))
    ) as ?missingProperty)
}
```

### 2. Visual Description Queries

- **CQ2.1**: How are visual elements (color, line, composition) represented and queried in an artwork?
```sparql
PREFIX arto: <http://w3id.org/arto#>

SELECT ?artwork ?element ?elementType ?descriptor
WHERE {
    ?artwork a arto:Artwork ;
            arto:containsScene ?scene .
    ?scene arto:containsObject ?object .
    ?object arto:containsElement ?element .
    ?element a ?elementType ;
             arto:descriptor ?descriptor .
    FILTER (?elementType IN (arto:Color, arto:Line, arto:Composition))
}
```

- **CQ2.2**: What objects are present in the artwork and how do they relate to each other?
```sparql
PREFIX arto: <http://w3id.org/arto#>

SELECT ?object1 ?relationship ?object2
WHERE {
    ?artwork a arto:Artwork ;
            arto:containsScene ?scene .
    ?scene arto:containsObject ?object1 .
    ?object1 arto:relatedTo ?object2 .
    ?object1 arto:descriptor ?relationship .
}
```
- **CQ2.3**: How are multiple scenes structured and connected within the artwork?
```
PREFIX arto: <http://w3id.org/arto#>

SELECT ?mainScene ?subScene
WHERE {
    ?artwork a arto:Artwork ;
            arto:containsScene ?mainScene .
    ?mainScene arto:containsScene ?subScene .
}
```
- **CQ2.4**: What artistic techniques and stylistic features are used in the artwork?
```sparql
SELECT DISTINCT ?artwork ?title ?style ?technique
WHERE {
    # Basic artwork information
    ?artwork a arto:Artwork ;           # Find items that are artworks
            dc:title ?title ;           # Get their titles
            arto:style ?style .         # Get their artistic styles
    
    # Creation technique (optional)
    OPTIONAL {
        ?artwork dbp:technique ?technique .  # Get technique if available
    }
}
GROUP BY ?artwork ?title ?style ?technique 
ORDER BY ?artwork
```

### 3. Semantic Interpretation Queries

- **CQ3.1**: How can we represent the symbolic meanings and allegories in an artwork?
```sparql
PREFIX arto: <http://w3id.org/arto#>

SELECT ?artwork ?symbolism ?source
WHERE {
    ?artwork a arto:Artwork ;
            arto:hasConnotation ?connotation .
    ?connotation a arto:Symbolism ;
                 arto:source ?source .
}
```
- **CQ3.2**: What is the relationship between visual features and emotional expression?
```sparql
PREFIX arto: <http://w3id.org/arto#>

SELECT ?visualElement ?emotion ?intensity
WHERE {
    ?artwork a arto:Artwork .
    ?visualElement arto:expresses ?emotion .
    ?emotion a arto:Emotion ;
            arto:hasMetric ?metric .
    ?metric a arto:EmotionIntensity .
}
```
- **CQ3.3**: What is the main theme or subject matter of the artwork?
```
PREFIX arto: <http://w3id.org/arto#>
PREFIX dc: <http://purl.org/dc/terms/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
SELECT DISTINCT ?artwork ?title ?mainTheme ?symbolism ?relatedScene ?sceneObject
WHERE {
    # Basic artwork information
    ?artwork a arto:Artwork ;
            dc:title ?title .
    
    # Get themes
    ?artwork arto:hasConnotation ?themeConnotation .
    ?themeConnotation a arto:Theme ;
                     rdfs:label ?mainTheme .
    
    # Get related symbolism
    OPTIONAL {
        ?artwork arto:hasConnotation ?symbolismConnotation .
        ?symbolismConnotation a arto:Symbolism ;
                            rdfs:label ?symbolism ;
                            arto:source ?symbolSource .
    }
    
    # Get scenes expressing the theme
    OPTIONAL {
        ?artwork arto:containsScene ?scene .
        ?scene rdfs:label ?relatedScene ;
               arto:expresses ?themeConnotation .
        
        # Key objects in the scene
        OPTIONAL {
            ?scene arto:containsObject ?object .
            ?object rdfs:label ?sceneObject ;
                    arto:expresses ?themeConnotation .
        }
    }
}
GROUP BY ?artwork ?title ?mainTheme ?symbolism ?relatedScene ?sceneObject
ORDER BY ?artwork ?mainTheme
```

### 4. Context Information Queries

- **CQ4.1**: What was the historical context during the artwork's creation?
```
PREFIX arto: <http://w3id.org/arto#>

SELECT ?artwork ?event ?time
WHERE {
    ?artwork a arto:Artwork ;
            arto:relatedToEvent ?event .
    ?event arto:hasTime ?time .
    ?time a arto:Time .
}
```
- **CQ4.2**: How did the artist's personal experiences influence the artwork?
```
PREFIX arto: <http://w3id.org/arto#>
PREFIX dc: <http://purl.org/dc/terms/>
PREFIX event: <http://purl.org/NET/c4dm/event.owl#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
SELECT DISTINCT ?artwork ?artist ?event ?eventTime ?theme ?emotion ?symbolism
WHERE {
    # Get artwork and its creator
    ?artwork a arto:Artwork ;
            dc:creator ?artist ;
            dc:title ?artworkTitle .
    ?artist a arto:Artist .
    # Get events related to the artist
    ?event a arto:Event ;
           event:agent ?artist ;
           arto:hasTime ?timeEntity .
    ?timeEntity a arto:Time .
    
    # Time information of the event
    OPTIONAL {
        ?timeEntity sdo:startDate ?eventTime .
    }
    # Association between event and artwork content
    OPTIONAL {
        ?artwork arto:relatedToEvent ?event .
    }
}
ORDER BY ?eventTime
```
- **CQ4.3**: What was the social and cultural background of the time?
```sparql
PREFIX arto: <http://w3id.org/arto#>
PREFIX dc: <http://purl.org/dc/terms/>
PREFIX event: <http://purl.org/NET/c4dm/event.owl#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX sdo: <http://schema.org/>

SELECT DISTINCT ?artwork ?period ?event ?eventType
WHERE {
    # Basic artwork information
    ?artwork a arto:Artwork ;
            dc:title ?title ;
            arto:style ?artStyle .
    
    # Get creation period
    ?artwork arto:relatedToEvent ?timeEvent .
    ?timeEvent a arto:Event ;
              arto:hasTime ?period .
    
    # Historical events from the same period
    ?event a arto:Event ;
           arto:hasTime ?eventTime ;
           dc:type ?eventType .
    
    # Ensure events occurred in a similar timeframe
    ?eventTime sdo:startDate ?startDate .
    ?period sdo:startDate ?periodStart .
    
    # Can add time range filter
    FILTER (
        abs(year(?startDate) - year(?periodStart)) <= 10
    )
    
    # Filter event types
    FILTER (?eventType IN (
        "Cultural_Movement",
        "Social_Movement",
        "Historical_Event",
        "Art_Movement"
    ))
}
ORDER BY ?period ?eventType
```
