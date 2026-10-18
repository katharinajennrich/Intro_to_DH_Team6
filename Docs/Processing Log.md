# Processing Log

## Initial Research Question and Thesis
**Date**: 20.9.2026

**Contributor(s**): ALL

**Challenges**: The RQ was not answerable with the data available to us as it referenced specific socio-economic factors for which we have no data. We were also unable to find data to link into our project, resulting in revision of the question. 

## Revised Thesis
**Date**: 29.9.2026

**Contributor(s)**: ALL

**Description**: Initially, for the research question about the connectivity of Kreuzberg and Wilmersdorf, we hypothesized a difference in connectivity favoring Wilmersdorf. Our results support an interpretation of Kreuzberg and Wilmersdorf having had comparable connectivity. 

## Initial Data Filtering
**Date**: 25.9.2026

**Contributor(s)**: Katharina

**Description and Justification**: We chose to focus on two specific districts. Thus, we needed to be able to isolate those stations and lines relevant to the chosen districts. For this we chose to include an external dataset which defines our chosen districts as polygons. We used these polygons and the Python package “GeoPandas” to determine which stations are within each district, and subsequently which lines service those stations within each district. 

### Stations
**Tool**: python geopandas

**Code File**: filtering_stations.ipynb

**Input File**: stations.csv

**Output File**: Kreuzberg_stations.csv, Wilmersdorf_stations.csv

**Processing Steps**: 
- Read stations.csv
- Re-arrange station co-ordinates into geopandas format: reverse latitude/longitude order and read as geopandas
- The validity of this step was verified with spot-checks in google maps confirming this format incompatibility
- Import external dataset: district polygons
- Use geopandas .within() function to determine if each station is within the district polygon
- Collect all stations within kreuzberg and wilmersdorf and save as new csv: Kreuzberg_stations.csv, Wilmersdorf_stations.csv
  
**Overview**:
- This transformation is fully reversible as it creates a new file, and preserves all existing columns.
- This transformation filtered the original dataset of 19758 rows to:
  - Kreuzberg: 721 rows
  - Wilmersdorf: 476 rows
    
**Challenges**:
- Initial incorrect use of co-ordinates yielding no stations within either districts due to the reversal of latitude/longitude
- The district polygons are defined by a limited number of points, making them imprecise

### Lines
**Tool**: python geopandas

**Code File**: filtering_lines.ipynb

**Input File**: lines.csv

**Output File**: Kreuzberg_lines.csv, Wilmersdorf_lines.csv

**Processing Steps**:
- Read Kreuzberg/Wilmersdorf_stations.csv
- Read line_stops.csv
- Iterate over line_stops.csv:
- Check if each stop_id is in Kreuzberg/Wilmersdorf.csv
- Add the corresponding line_id to a list
- Save all the line_id’s identified above into new csv: Kreuzberg_lines.csv, Wilmersdorf_lines.csv
  
**Overview**:
- This transformation is fully reversible as it creates a new file, and preserves all existing columns.
- This transformation filtered the original dataset of 2099 rows into:
  - Kreuzberg: 248 rows
  - Wilmersdorf: 199 rows
    
**Challenges**:
- Relies on the accuracy of the earlier filtering step, despite our confidence in it

## Data Filtering: Years
**Date**: 2.10.2026

**Contributor**: Katharina

**Description and Justification**: Several analyses require the lines within each district to be separated into the chosen survey years. This filtering was in actuality generally done either within the code prior to visualization without saving this filtered dataset, or completely manually. However, the filtered datasets are useful for human review, and so are included along with their method of creation here.

**Tool**: python

**Code File**: this transformation occurs at the beginning of heatmap_kreuzberg.ipynb and heatmap_wilmersdorf.ipynb

**Input File**: Kreuzberg_lines.csv, Wilmersdorf_lines.csv

**Output Files**: Kreuzberg_lines_{year}.csv, Wilmersdorf_lines_{year}.csv

**Processing Steps**: 
- Read Kreuzberg/Wilmersdorf_lines.csv as a pandas dataframe
- Filter the dataframe by year (1951, 1961, 1967, 1976, 1984)
- Save the dataframe as csv: Kreuzberg_lines_{year}.csv, Wilmersdorf_lines_{year}.csv
  
**Overview**:
- This transformation is fully reversible as it creates a new file, and preserves all existing columns.
- This transformation filtered the Kreuzberg_lines.csv of 248 rows into:
  - 1951: 23 rows
  - 1961: 28 rows
  - 1967: 20 rows
  - 1976: 17 rows
  - 1984: 13 rows
- This transformation filtered the Wilmersdorf_lines.csv of 199 rows into:
  - 1951: 13 rows
  - 1961: 23 rows
  - 1967: 20 rows
  - 1976: 15 rows
  - 1984: 13 rows
    
**Challenges**:
- Relies on the accuracy of the earlier filtering steps, despite our confidence in them


## Coverage: Map visualizations and plotted percentages
**Date**: 6.10.2026

**Contributor(s)**: Martina

**Justification**: This analysis helps to answer the research question by comparing the public transportation coverage of Kreuzberg and Wilmersdorf in different years. We chose the coverage as a significant indicator to determine spatial connectivity because to some extent, the distance between citizen and transportation spots can reflect the convenience level of public transportation. In this part, we used three coverage radii to check the situation at different distances, which are 250, 500 and 1000 meters. By chasing the varying trend during continuous years, we tried to visualize the diachronic changes of the two districts. The results derived from the spatial location (shown as longitude and latitude in the dataset) and time of year, and we used percentages to present the data.

**Alternatives**: 
- Simple comparison of stations per square unit of area of each district: this would have flattened the impact of station location on their accessibility. 
- Complexified coverage analysis: taking into account topography or population density. This was not performed due to time and data constraints.

**Input File**: stations.csv, lines.csv, line_stops.csv

**Processing Steps**:
1. Load the data → We read the three timetable files (stations, lines, line stops) and the table with the Berlin district polygons. The raw files are not changed.
2. Districts → From the 97 Berlin sub-districts we keep only Kreuzberg and Wilmersdorf (the sub-district of Wilmersdorf only). Their outlines are converted to a coordinate system measured in metres, so that distances and areas are correct.
3. Stations → The dataset has no date column, so we take the year from the first four digits of each station ID. The location text (“latitude, longitude”) is split into two numbers and turned into a point on the map. The points are also converted to the metre-based coordinate system.
4. Year selection → We keep the stations of five years: 1951, 1961, 1967, 1976 and 1984. 7,409 station records out of 19,758.
5. For each year we draw a circle of a fixed radius around every station in Berlin, not only those inside the district, because a stop just outside the border can still serve people inside it. We do this three times, with radii of 250 m, 500 m and 1000 m.
6. For each year and radius, all circles are merged into one shape, so that areas where circles overlap are counted only once.
7. We keep only the part of the merged shape that lies inside Kreuzberg or Wilmersdorf. This is the covered area. What remains of the district outside this shape is the uncovered area.
8. We divide the covered area by the total area of the district to get the percentage covered. We also count how many station records lie inside each district. The results (30 rows: 2 districts, 5 years, 3 radii) are saved as a table.
9. For each district and year we also calculate stations per square kilometre, rail stations versus bus and tram stations, the number of lines serving the district, the typical time between vehicles, and the average distance from a point in the district to the nearest station. For the distance we place a grid of points every 100 m inside the district and measure to the nearest station. 
10. We draw maps of each district for each year (grey is not covered, blue is covered, red dots are stations), and a line chart showing how coverage changes over time for each radius.
When reading the results it’s important to consider that coverage is measured in a straight line. It ignores streets, the Wall, and whether a station could actually be used.

**Challenges**:
- This analysis was difficult to find the correct tools for (how to merge the area of the radii especially), which is why ultimately we consulted Claude AI in the design of the code.

## Frequency: Histogram of lines
**Date**: 7.10.2026

**Contributor(s)**: Katharina

**Justification**: This analysis helps to answer the research question by visualizing the frequency of departure intervals at 7:30 on weekdays in histogram form. Frequency was already presented in the original dataset and we filtered the dataset to centralize them to an intuitive form. Compared to spatial differences, frequency can directly show the connectivity between two regions. It is worth noting that 0 values are still ambiguous in the dataset, therefore we used a separate bin to demonstrate them.

**Tool**: python Matplotlib

**Code File**: histograms.ipynb

**Alternatives**: 
- Simple mean frequency, which was not selected due to obscuring details

**Input File**: Kreuzberg_lines.csv, Wilmersdorf_lines.csv

**Processing Steps**:
- Select for each year only the relevant lines
- Use the .plot.hist() function to create histograms for each sample year in each district
  - Box sizes: [0, 0.5, 5,10,15, 20,25,30,35,40,45,50,55,60,65,70,75,80,85,90,95,100,105,110,115,120]
  - The boxes are sized in intervals of 5, except for the box created to catch the zero values.

**Challenges**:
- A decision had to be made about 0 values, which we ultimately chose to separate from other lines 
- This visualization is does not show different transit types, which might provide more detail, but we decided against in order not to overcomplicate the visualization

## Range: Heat Map
**Date:** 2.10.2026

**Contributor(s)**: Katharina

**Justification**: This analysis helps to answer the research question by investigating inter-district connectivity of the two regions, which means the scope and intensity of other Berlin administrative districts by public transport lines in different years. Which area can be reachable from Kreuzberg and Wilmersdorf, and how many stations and lines are directly connected to them were mapped in heatmaps. The heatmaps excluded the values of the two regions themselves for we did not seek for within-district connectivity and the results are presented in uniform color scale to show similarity and difference.

**Tool**: python geopandas

**Code Files**: heatmap_kreuzberg.ipynb, heatmap_wilmersdorf.ipynb, heatmap_mapping.ipynb

**Alternatives**: 
- Network analysis: a similar visualization of inter-district connectivity would have been possible with a network visualization. This was not chosen due to time and expertise constraints.
Input File: line_stops.csv, Kreuzberg_lines.csv, Wilmersdorf_lines.csv, stations.csv

**Processing Steps**: 

**heatmap_kreuzberg/wilmersdorf.ipynb**
- Read Kreuzberg/Wilmersdorf_lines.csv as dataframe
- Read line_stops.csv as dataframe
- Filter line_stops dataframe by whether the line each stop is a part of (line_id) is included in Kreuzberg/Wilmersdorf_lines
  - Yields filtered dataframe including all stations that have a connection to Kreuzberg/Wilmersdorf
- Read stations.csv as dataframe
- Filter stations dataframe by whether their stop_id is included in the filtered line_stops dataframe
  - Yields all stations that are on a line that runs through Kreuzberg/Wilmersdorf
- Format all stations co-ordinates into geopandas (by reversing longitude/latitude as in the initial filtering)
- Add column to the filtered stations dataframe with the year, which is taken from the first 4 digits of the stop_id
- Filter the dataframe by year
- Read external data giving district polygons as geopandas dataframe
- Add column to district dataframe, whose value is determined as:
  - The number of stations in the filtered stations dataframe that is within each district
- Save the district dataframe as json file, ex.: stations_bydistrict_Wilmersdorf_1951.json
  
**heatmap_mapping.ipynb**
- Read stations_bydistrict_{district}_{year}.json as geopandas dataframe
- Set the number of stations for the row Kreuzberg/Wilmersdorf to 0
  - Because we are not interested in intra-district connectivity in this analysis, and setting the value to 0 allows us to set a different color for the district being analysed
- Use the geopandas .plot() function to produce a heat map giving the amount of stations connected to Kreuzberg/Wilmersdorf in each of the districts as a varying shade of blue
  - Maximum value is given universally as 42

**Challenges**:
- Data is stored intermediately as a json file, which allows all years to be reopened automatically in the secondary jupyter notebook. This separation of the process into two separate notebooks is the result of challenges while writing the code related to automating the chart creation. 

## Modes: Pie Charts
**Date**: 6.10.2026

**Contributor(s**): Martina

**Justification**: This analysis helps to contextualize, rather than answer, the research question by comparing public transport modes in different years. We primarily utilize the transportation mode categorization variable “typ“ from the route data to classify routes into four categories: buses, trams, U-Bahns, and S-Bahns. We then calculate their proportions within the total number of routes in each administrative region and year. A pie chart was chosen because it visually displays the relative proportions of different transportation modes, facilitating comparisons of the composition of the transportation systems in two regions and their historical changes. While the proportions of transportation modes cannot directly measure connectivity, they provide necessary context for other analyses, helping us understand the structural adjustments accompanying changes in transportation network connectivity.

**Tool**: Google Sheets

**Alternatives**: 
- Segmented bar plots: these would also show the difference in total amounts of lines. We prioritized the simplicity of the visualization in this case.

**Input File**: Wilmersdorf_lines.csv, Kreuzberg_lines.csv

**Processing Steps**:
- Manually transfer the number of lines per transit type in each year into a google spreadsheet
- Create pie charts using the google sheet pie chart option, keeping the same colors for transit modes across all charts

**Challenges**:
This analysis is descriptive in nature for our chosen research question, which we only fully realized after its completion

