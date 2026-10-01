# Modelling Temporal Public Transport Systems: Cold-War Berlin

This is a Digital Humanities project which investigates the relationship between the political division of Germany and the development of Berlin’s transport network between 1946 and 1989.
 
## Context

After World War II, Germany was divided into East and West Germany, while Berlin was itself divided into different sectors. The political division had major consequences for mobility and transportation within the city as movement between the eastern and western parts became increasingly restricted. The construction of the Berlin Wall in 1961 further reinforced this separation, dividing communities and disrupting existing transportation connections.

## Dataset Biography

The dataset was created by **Noah Baumann** at Humboldt-Universität zu Berlin and is based on the manual transcription of 36 historical timetable books from the Berlin public transport authority (BVG), held in the BVG Archive and the Jacob and Wilhelm Grimm Centre Library.

Data for the whole of Berlin is available for **1946 and 1951**, while from 1956 onwards the data is divided into **East Berlin and West Berlin**. The selected years provide at least one observation per five-year period, with additional years covering historically significant periods such as the early 1960s and the construction of the Berlin Wall.

It contains **19,758 station entries, 2,099 line entries, and 28,982 unique connections** and is structured into three relational CSV files:
- `stations.csv`- information on stations, including names, transport type, geographic coordinates, served lines, and Wikidata identifiers
- `lines.csv`- information on transport lines, including year, travel time, frequency, length, administrative zone, and start and end stations
- `line_stops.csv`- the sequence of stops served by each transport line

The data includes several modes of public transportation, including **tram, underground (U-Bahn), suburban railway (S-Bahn), bus, trolleybus, and ferry**. Geographic coordinates were determined using Wikidata, historical maps, route descriptions, intersection analysis, and distance validation between consecutive stations.

Besides, the dataset has several **limitations** that are relevant to our analysis. Bus and tram stops are not recorded in full: before 1975, the timetable books include only stops considered important, while West Berlin records all stops from 1975 onwards. S-Bahn information has to be supplemented using Reichsbahn sources because the S-Bahn was not operated by the BVG. In addition, frequency data represents the scheduled service at **7:30 on weekdays** and therefore does not capture variations throughout the day, week, or season. Some historical bus and tram locations are also approximated using intersections and may not correspond exactly to their original historical locations.

## Research Question

## Thesis Statement

## Repository Structure

## Concerns, Observations and Challenges

- **Challenge:** Our first research question was rejected because of limited data availability and an insufficient alignment between the research question and the thesis. Filtering the dataset by location is also challenging, as the dataset is too large to process manually and may require an automated approach.
- **Concern:** We need to ensure that the thesis does not make causal claims about factors that are only identified through additional literature rather than directly supported by our dataset.
- **Decision:** We need to decide whether to use the broader area of Wilmersdorf or focus specifically on the smaller historical district of Wilmersdorf for our analysis.

## Use of Generative AI

## Sources




















