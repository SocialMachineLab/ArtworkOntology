# Data

This document describes the data collection process for our research project on art-related museums and collections. It provides details on the data sources, methods, tools, and preprocessing steps used to obtain and prepare the data for analysis.

Our data workflow starts with identifying the appropriate data sources. From our exploration, we found 12 data sources to be available, listed in Table \ref{tab:data}. Most of the data sources, including Europeana, Wikiart, and others, are either public or partially public. Notably, while the Louvre's text is publicly available, its other content is not. The Art Bank's data is accessible for research and study purposes. 

Once the data was collected, we conducted a comprehensive analysis of the collected data, revealing important insights into aspects such as time representation, location, media categorisation, etc. During the analysis, we noticed some issues with the data and suggested further data cleaning.

We aimed to identify and normalize these diverse time representations to achieve consistent date data, as proposed by Dorobat and Posea (2021),  who highlight the power of regular expressions in  recognizing dates and epochs. Locations also have varied formats. Location level differs - from country, cities to institutions. Ancient place names change over time, so linking data to a time period is important. The dataset has over 26,000 distinct medium categories. Consolidating similar mediums based on characteristics and art standards would simplify the data and reduce imbalance and complexity, although some information would be lost. We can mitigate this through hierarchical categorization, preserving fine-grained details when necessary.


## Data Sources

We collected data from the following sources:


| Data Source | Number of Artworks | Has Schema? | Number of Attributes | Copyright |   Attributes |
|-------------|--------------------|-------------|-----------------------|-----------|----------|
| [Europeana](https://www.europeana.eu/en) | 2,594,696 | Yes | 17 | Fully Public |title, creator, Publisher, subject,Type of item,Aggregator,Creation date,Places,Identifier, description,Language,Year,Providing country,Collection name,Is part of,Identifier,image,Format|
| [Wikiart](https://www.wikiart.org/) | 172,397 | No | 17 | Partially Public |title,year,width,height,artistName,image,description,Style,Genre,Media,Location,Original Title,Series,Period,wikipediadescription,Theme,provenance｜
| [Artic](https://www.artic.edu/) | 93,836 | No | 9 | Partially Public |  creator, description, exhibition history, provenance, title, place, medium,dimension,date|
| [American art](https://americanart.si.edu/) | 39,388 | No | 13 | Partially Public |title, artist,date,location,dimension,copyright,credit,mediums,classification,highlight,keywords,Object Number,Linked Open Data|
| [Louvre](https://www.louvre.fr/en) | 512,613 | No | 9 | Public Metadata |title, creator, date,description,collection,history,dimension,material,location|
| [Nation Museum](https://collection.nationalmuseum.se) | 82,463 | No | 6 | Partially Public |title,creator,description,Material,dimension,Exhibited|
| [NGA.gov](https://www.nga.gov/) | 139,723 | No | 26 | Fully Public |objectid,accessioned,accessionnum,locationid,title,displaydate,beginyear,endyear,visualbrowsertimespan,medium,dimensions,inscription,markings,attributioninverted,attribution,provenancetext,classification,subclassification,visualbrowserclassification,parentid,isvirtual,departmentabbr,portfolio,series,volume,watermarks|
| [MET museum](https://www.metmuseum.org) | 218,930 | No | 12 | Partially Public |artist, date, current location,description, provenance,title, period, culture, medium, classification|
| [Brooklyn Museum](https://www.brooklynmuseum.org/) | 67,529 | No | 13 | Partially Public |title, artist,medium,dimension, collection,location,caption,image,date,DESCRIPTION,period,SIGNATURE,MARKINGS|
| [Getty](https://www.getty.edu) | 86,848 | Yes | 10 | Partially Public |id,primary_name,date_created,culture,creator,Medium,dimension,Mark,classification,object type|
| [British Museum](https://www.britishmuseum.org) | 2,123,229 | No | 16 | Partially Public |title,artist,object type,description,cultures,date,material,location,subject,Acquisition date,Department,Technique,School,Production place,comments|
| [Art bank](https://www.artbank.gov.au/) | 10,727 | No | 9 | For research and study | image, title, artist, date, material, medium, size, price, description|



## Data Collection



Web scraping is for extracting data from web pages automatically. We use BeautifulSoup and httpx to extract the data.

#### Example Code

```python
import httpx
import time
import json
from bs4 import BeautifulSoup


client = httpx.AsyncClient(http2=True)
header={"Cookie": "",
"User-Agent": "",
"Accept": "application/json, text/plain, */*",
"Accept-Language": "zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2",
"Accept-Encoding": "gzip, deflate",
"X-Requested-With": "XMLHttpRequest",
"Upgrade-Insecure-Requests": "1",
"Sec-Fetch-Dest": "empty",
"Sec-Fetch-Mode": "cors",
"Sec-Fetch-Site": "same-origin",
"Te": "trailers"}

urls=["https://www.wikiart.org/en/artists-by-art-movement",
"https://www.wikiart.org/en/artists-by-painting-school",
"https://www.wikiart.org/en/artists-by-genre",
"https://www.wikiart.org/en/artists-by-field",
"https://www.wikiart.org/en/artists-by-nation",
"https://www.wikiart.org/en/artists-by-century",
"https://www.wikiart.org/en/artists-by-art-institution"]

for i in urls:
    dic={}
    response = await client.get(i,headers=header)
    soup = BeautifulSoup(response.text,'html.parser')
    s=soup.find_all('li',class_="dottedItem")
    href=[]
    for j in s:
        a=BeautifulSoup(str(j),'html.parser')
        b=a.find(href=True)
        href.append(b['href'])
    data={}
    for j in href:
        d[j]=[]
    
    with open("....json","w") as f:
        json.dump(data,f)    
        
```


## Data Preprocessing


1. Understand data scale, format, and summarize data types, missing values, and other basic information for each field

    - Use Python's Pandas library to read the data file and understand basic information such as the attribtues and the type of attributes.


2. Handle missing values by deleting or filling (e.g., with mean or mode)

    - For fields with a high proportion of missing values (e.g., >50%), consider dropping the field as it may not have much reference value


3. Identify and handle outliers, such as values with incorrect format or outside a reasonable range

    - For numeric fields, use df.describe() to view statistics such as minimum, maximum, mean, and quantiles to determine if there are outliers outside the normal range


4. Standardize names and values to ensure data consistency

    - Check attribute names and convert them to lowercase, remove spaces, and ensure consistent naming style

    - Standardize values in categorical fields, such as converting to lowercase and removing leading/trailing whitespace


    - Map different representations of the same meaning, such as mapping both 'creation date' and 'production date' to 'creation date'

## Data Analysis


- Analyze the distribution of key fields (e.g., artist nationality, art genre, creation year)

- For categorical fields, use df['field'].value_counts() to view the frequency distribution of each value
- For numeric fields, use df['field'].hist() to plot a histogram and observe the data distribution















