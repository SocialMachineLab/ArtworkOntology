# Data

This document describes the data collection process for our research project on art-related museums and collections. It provides details on the data sources, methods, tools, and preprocessing steps used to obtain and prepare the data for analysis.

Our data workflow starts with identifying the appropriate data sources. From our exploration, we found 12 data sources to be available, listed in Table \ref{tab:data}. Most of the data sources, including Europeana, Wikiart, and others, are either public or partially public. Notably, while the Louvre's text is publicly available, its other content is not. The Art Bank's data is accessible for research and study purposes. 

Once the data was collected, we conducted a comprehensive analysis of the collected data, revealing important insights into aspects such as time representation, location, media categorisation, etc. During the analysis, we noticed some issues with the data and suggested further data cleaning.

We aimed to identify and normalize these diverse time representations to achieve consistent date data, as proposed by Dorobat and Posea (2021),  who highlight the power of regular expressions in  recognizing dates and epochs. Locations also have varied formats. Location level differs - from country, cities to institutions. Ancient place names change over time, so linking data to a time period is important. The dataset has over 26,000 distinct medium categories. Consolidating similar mediums based on characteristics and art standards would simplify the data and reduce imbalance and complexity, although some information would be lost. We can mitigate this through hierarchical categorization, preserving fine-grained details when necessary.


## Data Sources

We collected data from the following sources:


| Data Source | Number of Artworks | Has Schema? | Number of Attributes | Copyright |
|-------------|--------------------|-------------|-----------------------|-----------|
| [Europeana](https://www.europeana.eu/en) | 2,594,696 | Yes | 17 | Fully Public |
| [Wikiart](https://www.wikiart.org/) | 172,397 | No | 17 | Partially Public |
| [Artic](https://www.artic.edu/) | 93,836 | No | 9 | Partially Public |
| [American art](https://americanart.si.edu/) | 39,388 | No | 13 | Partially Public |
| [Louvre](https://www.louvre.fr/en) | 512,613 | No | 9 | Public Metadata |
| [Nation Museum](https://collection.nationalmuseum.se) | 82,463 | No | 6 | Partially Public |
| [NGA.gov](https://www.nga.gov/) | 139,723 | No | 26 | Fully Public |
| [MET museum](https://www.metmuseum.org) | 218,930 | No | 12 | Partially Public |
| [Brooklyn Museum](https://www.brooklynmuseum.org/) | 67,529 | No | 13 | Partially Public |
| [Getty](https://www.getty.edu) | 86,848 | Yes | 10 | Partially Public |
| [British Museum](https://www.britishmuseum.org) | 2,123,229 | No | 16 | Partially Public |
| [Art bank](https://www.artbank.gov.au/) | 10,727 | No | 9 | For research and study |



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





## Data Analysis






## Data Preprocessing



