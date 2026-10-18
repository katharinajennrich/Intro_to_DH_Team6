# Modelling Temporal Public Transport Systems: Cold-War Berlin

After the end of the second World War, Berlin went through a political division between the communist East and capitalist West, which then followed by the construction of the Berlin Wall in 1961. This has prompted a much deeper division in the societal fabric of the city, best exemplified by the division of the public transport systems. For our project, we want to focus on two separate districts within West-Berlin: Kreuzberg and Wilmersdorf, and turn this into a comparative analysis of both districts in the light of these transformations in connectivity. 


## Table of Contents

- [Research Question](#research-question)
- [Thesis Statement](#thesis-statement)
- [Dataset](#dataset)
- [Workflow Diagram](#workflow-diagram)
- [Main Findings](#main-findings)
- [Team Members](#team-members)
- [Use of Generative AI](#use-of-generative-ai)
- [References](#references)


## Repository Structure

| Folder            | Description                                                        |
| ----------------- | -------------------------------------------------------------------|
| `Analysis`       | contains Jupyter notebooks, scripts, and queries                   |
| `Dataset`        | stores raw, processed, and external datasets                       |
| `Docs`           | contains all project and analysis documentation  |
| `Results`        | stores summary of findings and presentation materials            |
| `Visualizations` | contains graphs, figures, charts and other visual outputs          |


## Research Question

How did public transportation connectivity in Kreuzberg compare to Wilmersdorf during the restructuring and division of Berlin between 1949 and 1989?


## Thesis Statement

The connectivity of Kreuzberg and Wilmersdorf throughout the division of Berlin is largely comparable. However, a general trend in improved connectivity after 1951 can be observed in both districts.

## Dataset 

The dataset was created by Noah Baumann at Humboldt-Universität zu Berlin and is based on the manual transcription of 36 historical timetable books from the Berlin public transport authority (BVG), held in the BVG Archive and the Jacob and Wilhelm Grimm Centre Library.

Data for the whole of Berlin is available for 1946 and 1951, while from 1956 onwards the data is divided into East Berlin and West Berlin. The selected years provide at least one observation per five-year period, with additional years covering historically significant periods such as the early 1960s and the construction of the Berlin Wall.

It contains 19,758 station entries, 2,099 line entries, and 28,982 unique connections and is structured into three relational CSV files:

- `stations.csv` - information on stations, including names, transport type, geographic coordinates, served lines, and Wikidata identifiers
- `lines.csv`- information on transport lines, including year, travel time, frequency, length, administrative zone, and start and end stations
- `line_stops.csv` - the sequence of stops served by each transport line

The data includes several modes of public transportation, including tram, underground (U-Bahn), suburban railway (S-Bahn), bus, trolleybus, and ferry. Geographic coordinates were determined using Wikidata, historical maps, route descriptions, intersection analysis, and distance validation between consecutive stations.


## Workflow Diagram

Our workflow combines **data preprocessing, network analysis, and comparative analysis** to investigate public transport connectivity in Kreuzberg and Wilmersdorf across five snapshot years.

### 1. Data preprocessing 

Using GeoPandas, a Python mapping library, we assigned stations to the Kreuzberg and Wilmersdorf polygons, after swapping latitude and longitude, which the dataset stores in reverse order. We then linked stations to lines through the line stops table and selected five snapshot years: 1951, 1961, 1967, 1976 and 1984.

### 2. Four connectivity analyses
   
We turned connectivity into four measurable analyses: a histogram of how often each line runs, a heat map of how many stops are reachable from each district, a coverage analysis of how much district area lies close to a station, and pie charts of transport modes, which we use only as a rough overview.

### 3. Comparison and validation

We kept lines with zero frequency as a separate grey category, because they only affect S-Bahn lines and look like irregular service, not removals. For coverage, a one kilometre radius covered everything, so we added 250 and 500 metres as a sensitivity check, to see whether results depend on distance. We also considered calculating an average frequency but total rides per day was not feasible so we made histograms instead. To validate, we visually checked the district on maps, and checked that our calculations add up to the total lines per district. Finally, we fixed scales across all charts, so years and districts are directly comparable.


## Main Findings

- **Heatmap**: no overwhelming differences visible in how far or how well reachable surrounding districts are, only a slight increase in districts with medium connectivity in later years
- **Histogram**: both districts show similar changes in service frequency, with more lines departing every 5-10 minutes and fewer at intervals over 20 minutes in later years
- **Coverage**: around 90% of both Kreuzberg and Wilmersdorf are within 500 meters of any public transit station, with no consistent advantage for either district 
- **Piechart**: a decline in the diversity of transport types, with trams disappearing by 1976 and S-Bahn services becoming very limited by 1984, later be replaced with buses


## Team Members
- **Junfeng Hsu**: analytical writer (analysis, writing, problem-solving)
- **Katharina Jennrich**: writer and quality control (writing, coding, cross-checking, submissions)
- **Micha de Tombe**: historical research lead documentation lead (research, writing, documentation)
- **Martina Panzani**: data and technical lead, coordinator (coding, organization)
- **Mai Ngo**: documentation and repository manager (organization, writing, editing)


## Use of Generative AI
Our project mainly uses AI as a brainstorm instrument. In our beginning stage we use AI to help us clarify division of labor for each person and determine everyone’s work aim and summary. After that we use AI to generate a poll for our teammates to choose their expected work. Definitely, this work was after our discussion, so AI was just utilized to clarify. The majority of the subsequent writing of content, code, visualizations and PPT creation were all done manually. The exception to this is the coverage analysis, where Claude AI was used to assist with finding the correct packages and functions to perform the tasks related to calculating coverage area. ChatGPT was also used to identify grammatical errors and improve word choices, with all suggested changes reviewed and corrected manually.


## References
Geschichte Wilmersdorfs im Überblick. (2023, August 11). https://www.berlin.de/ba-charlottenburg-wilmersdorf/ueber-den-bezirk/geschichte/artikel.181127.php

Haeussermann, H., & Kapphan, A. (2004). BERLIN: FROM DIVIDED INTO FRAGMENTED CITY. Επιθεώρηση Κοινωνικών Ερευνών, 113, 25. https://doi.org/10.12681/grsr.9216

Hochmuth, H. (2017). The return of Berlin-Kreuzberg. Brought back from the margins by memory. Journal of Contemporary European Studies, 25(4), 470–480. https://doi.org/10.1080/14782804.2017.1361817

Mishra, S., Welch, T. F., & Jha, M. K. (2012). Performance indicators for public transit connectivity in multi-modal transportation networks. Transportation Research Part A: Policy and Practice, 46(7), 1066–1085. https://doi.org/10.1016/j.tra.2012.04.006

Scheiner, J. (2005). Daily Mobility in Berlin: On ‘Inner Unity’ and the Explanation of Travel Behaviour. European Journal of Transport and Infrastructure Research, 5(3). https://doi.org/10.18757/ejtir.2005.5.3.4399






















