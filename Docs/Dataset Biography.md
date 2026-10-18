# Dataset Biography
## Background
The dataset was created by Noah J. Kim-Baumann, research assistant and digital historian and chair at the Humboldt Üniversität zu Berlin. The dataset was created between 2024-03-01 and 2025-10- 26 (including expansion) and was published on October 26, 2025 and named ‘Berliner Nahverkehrsnetz 1946-1989: Transkribierte Fahrplandaten aus dem geteilten Berlin’  (Berliner local transportation network 1946-1989: transcribed travel schedule data from divided Berlin) and a discussion paper was later published in Feb 26 2026 by Baumann in journal of open Humanities Data vol12 article36, ‘Modelling Temporal Public Transport Systems in Wikidata: A Workflow for Integrating Historical Infrastructure Data’. 

The Data-set’s publication on Zenodo was supported by NFDI4Memory FAIR Data Fellowship, the Deutsches Museum and funded by NFDI4Memory and the publication charge of the paper was done through an Open Access publication fund by the Humboldt Üniversität.

The published discussion paper presents the data-set as a case study on the application of a systematic workflow that would allow integration between wiki-data and the digital-humanities. While the initial research question was: “How accessibility to essential urban services via public transport diverge between East and West Berlin, and asks what these patterns reveal about the relationship between political systems and infrastructure development?”. At the time of publishing there was no combined data-set including both East and West Berlin over the division period 1946-1989. Besides this the data-set enables more research on the examination of Berlin’s public transport system, while the temporal coverage allows for examination of the evolution and changes within the system. 

It’s unknown to us whether the workflow was always the intended purpose of the data-set or an unintended result. As it stands the data-set’s current purpose is an application of a workflow that could allow for temporal data integration, the inclusion of uncertain variables and more historical complexity.

The majority of the data-set is created through 36 Fahrplanbücher provided by BVG (Berlin’s public transport authority), stored in the BVG archive and the Jacob and Wilhelm Grimm Centre Library. The data consists of 19758 station records, 2099 line records and 28982 connections. The temporal coverage spreads over 13 snapshots from 1946-1989 (1946,”51,”56,”60,”61,”64,”67,”71,”76,”80,”82,”84,”89), making sure that there is a data point within every 5 year period. The data is divided over four transport modalities: the U-Bahn (Metro), S-Bahn (urban rail), straßenbahn (the tram) and the bus.


The data-set is structured around three CSV tables capturing these different modes of transport. 
- Line Stops_CSV (551.0kB):
The stop order for each line.
- Lines_CSV (173.7kB):
The data related to the line including mode, time, and frequency.
- Stations_CSV (1.7MB): 
The data related to the station, located with geolocation, in line with wiki-data source.
- README_Fahrplanbuch_Daten.txt (10.0kB):
A small description and abstract on the data-set and source.

## Data processing
The data-set was founded on a doctoral research investigation into Berlin’s political division in relation to its transportation connectivity between 1946-1989. Basing himself on analog records of Berlin’s public transport system, through the BVG archive. Using fahrplanbücher, timetables and route maps Baumann collected the data, proceeding to the processing Baumann made selections and isolated elements from the data. Systematized the annotation to make the data machine-readable and allows for later reconciliation.
After this Bauman made use of Linked Open Data (LOD) leveraging a community driven data model, that of Wikidata. LOD can allow for a larger linking with pre-existing geographic, biographical and institutional authorities. Baumann decided on Wikidata as a platform, because it had a near complete coverage on the S-Bahn and U-bahn networks, including geographical data on the stations. Through the integration of these historical research projects. Additionally, Wikidata uses reification so that you can assert a property into an instance and thus you would be able to refer to it, enabling temporal scoping. 
Baumann made sure to keep all the decisions documented in the README, As to ensure that the modelling is not treated as the creation of a technical entry, but as an interpretive act. During transcription, Baumann reconciled both the Wikidata and the  loading station names into OpenRefine. The reconciliation results were then stored within the wikidata_id_column. Creating a percentile for every mode of transport and their coverage, revealing the quantitative data coverage gaps. This in turn allowed for a mapping on data coverage, depicting where data had to be created or enhanced. This was done through close reading manual entity inspection of the wiki-data entries, their classification patterns, property usage, temporal modelling approaches, reference practices and administrative geography. (3.2.1). This resulted in a depiction of the inconsistencies found in the multi-level taxonomies on Wikidata entries. 
Next Baumann and his team did a distant reading through the development and use of a Python-based investigation framework, named SPARQLWrapper to query Wikidata systematically. The code of this framework was designed and structured to be used as reusable functions for querying Wikidata into pandas Dataframes, and visualisations. 
After consistent alteration between distant and close reading a data model was created. Finally the data-set was uploaded as an open publication on Wiki-data and Zenodo, so as to create accessibility. Which was done through an upload strategy where historical accuracy and nuance, compatibility with Wikidata’s practices and long-term maintainability had to be balanced, through decision heuristics the upload process was systematized and completed. 


## Limitations
As mentioned before, the scope of Baumann's data-set is limited in a number of ways.
Station coverage is limited, fahrplanbücher only depicts “important stops” for bus and tram. Selection criteria changed over time.
The data-set is based on a series of 13 snapshots taken at 7:30 on weekdays. Holidays and weekend schedules are excluded as are seasonal, hourly and daily changes.
Geographic precision is limited, While U-Bahn and S-Bahn coordinates derived from Wiki-Data are largely accurate, tram and bus base themselves on rough intersections.
Time Coverage is 1 in every 5 years, but does not cover every year.


## Categories inherited from the source.
According to the investigation done by Baumann into Wikidata’s design, there are certain tensions in the use of the platform. While there is frequency data captured in the Fahrplanbücher, this is not adequately modelled on Wikidata. Event intervals with point in time offer a partial solution to this problem according to Baumann. Additionally, operational discontinuation is close to impossible to represent adequately as stated by Baumann. Stations that open, close and re-open will need multiple property-qualifier combinations. Lastly any historical entity forming a cyclical state faces these problems. How this complexity of the temporal is handled can only be done through community guidance on Wikidata as a platform. Any research working with multiple entries will face these tensions, and any systematized categories using Wikidata as a source.


## Usage
The data-set has been created with the goal of providing a basis for research into Berlin’s transport history. While temporal coverage supports “distant reading” of infrastructure evolution. Distant reading could be combined with quantitative sources in order to understand debates on Berliners' experience and tensions during the division period. Qualitative research could provide context behind urban-planning decisions. 
