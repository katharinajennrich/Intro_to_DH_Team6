
# Codebook Analysis

The variables used, produced by the coverage analysis (Analysis/coverage\_analysis\_en.ipynb) for the years 1951, 1961, 1967, 1976 and 1984\.

**How to read this document**

- Origin says whether a variable is Original (taken unchanged from the source file) or Created (calculated or recoded by the team).  
- Original German column names are kept exactly as they appear in the source files (for example standort, typ, frequenz). English adaptations are ours.  
- All distances and areas in the analysis are in metres and square metres (reported as km²) in the coordinate system EPSG:25833 (ETRS89 / UTM zone 33N). The source coordinates are in EPSG:4326 (WGS84, degrees) and the district polygons are in EPSG:3857 (Web Mercator).   
- Counts quoted below were checked directly against the files in the repository.

Files described:

| File | Role | Rows |
| :---- | :---- | :---- |
| Dataset/Raw/stations.csv | Original data: stops per year and transport mode | 19,758 |
| Dataset/Raw/lines.csv | Original data: lines per year | 2,099 |
| Dataset/Raw/line\_stops.csv | Original data: ordered stops of each line | 28,982 |
| Dataset/External/a0000000b.gdbtable | External data: Berlin district polygons | 97 |
| Results/coverage\_results.csv | Created: coverage per district, year and radius | 30 |
| Results/indicators\_by\_district.csv | Created: further indicators per district and year | 10 |
| Results/Kreuzberg\_\*.csv, Results/Wilmersdorf\_\*.csv | Created earlier: stations and lines filtered by district |  |

## Original Data: stations.csv

One row is one stop served by one transport mode in one survey year. A place served by U-Bahn, S-Bahn and bus appears in several rows. Source: transcription of BVG timetable books (plus Reichsbahn sources for the S-Bahn) by Noah Baumann, Humboldt-Universität zu Berlin. See Dataset/Raw/README\_Fahrplanbuch\_Daten.txt 

| Variable | Definition | Type | Values / unit | Origin and rule | Blank, missing, unknown | Limitations and ambiguities |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| stop\_id | Identifier of the stop record. The first 4 digits are the survey year, the rest is a running number (README: format YEAR+NUMBER). | integer | 5 to 8 digits. Prefixes seen: 1946, 1951, 1956, 1960, 1961, 1964, 1967, 1971, 1976, 1980, 1982, 1984, 1989\. | Original. The team extracts the year from it  | Never blank. | Not unique: 34 IDs appear twice (68 rows), all in 1956 to 1967\. Each pair has the same name and coordinates but a different typ (bus and trolleybus). |
| stop\_name | Name of the stop as in the timetable book. | text | Free text. 2,326 names contain Ecke ("corner"), e.g. Badstr. Ecke Pankstr.. | Original. The dataset creator added the crossing street after Ecke to make geolocation possible, and standardised street suffixes. | Never blank. | Spelling varies between rows (e.g. Pankstr. vs Pankstrassse), so names are not used for matching. Not used in the analysis. |
| typ | Transport mode of the line serving this stop record. | text (category) | autobus 12,413; straßenbahn 3,869; s-bahn 1,767; u-bahn 1,459; oberleitungsbus 164; omnibus 55; fähre 25; bus (umlandlinie) 6 | Original. Used by the team to separate rail (u-bahn, s-bahn) from other modes in the indicators. | Never blank. | The categories are those of the 1946 to 1989 timetable books, not modern ones. omnibus (55 rows, almost all 1946\) is not defined separately from autobus in the README. We treat it as a bus. |
| standort | Location of the stop. | text | "latitude, longitude" in decimal degrees (WGS84), e.g. "52.5213, 13.4119". Range: lat 52.2944 to 52.7536, lon 13.0587 to 13.9084. | Original. Latitude comes first. The team splits it into lat and lon (section 3.1). | Never blank. | U-Bahn and S-Bahn locations come mostly from Wikidata. Many bus and tram locations are estimated at street intersections and may differ from the real historical position. Some rows contain a space after the comma. |
| in\_linien | Lines serving the stop. | text (a Python-style list stored as a string) | e.g. "\['1', '9'\]" | Original. | Never empty. | Line names, not IDs. Names are reused across years. Not used in the analysis. |
| wikidata\_id | Wikidata identifier of the station. | text | e.g. Q323551 | Original. | Blank for 15,116 rows (76.5%). Present for all U-Bahn and S-Bahn rows, 1,404 tram rows and 12 bus rows. | Blank means "no Wikidata item used", not "no such stop". Not used in the analysis. |

## Original Data: lines.csv, line\_stops.csv, district polygons

**lines.csv** (One row is one line in one survey year)

| Variable | Definition | Type | Values / unit | Origin and rule | Blank, missing, unknown | Limitations and ambiguities |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| line\_id | Identifier of the line record. First 4 digits equal jahr (checked for all rows). | integer | unique | Original. Links to line\_stops.csv. | Never blank. |  |
| jahr | Year of the timetable book. | integer | 1946, 1951, 1956, 1960, 1961, 1964, 1967, 1971, 1976, 1980, 1982, 1984, 1989 | Original. | Never blank. | Only 13 snapshots exist. Nothing is known about years in between. |
| linien\_name | Line label. | text | e.g. 1, A37, KBS 100a | Original. | Never blank. |  |
| typ | Transport mode of the line. | text (category) | autobus 1,240; straßenbahn 495; s-bahn 203; u-bahn 130; oberleitungsbus 17; fähre 12; bus (umlandlinie) 2 | Original. | Never blank. |  |
| dauer (min) | Travel time between end stops. | number | minutes | Original. | 331 blank. | Not used. |
| ost\_west | Administrative zone of the line. | text (category) | West 993; Ost 806; both/unkown 221; ost 62; west 11; Ost/West 6 | Original. Not recoded in the analysis so far. | both/unkown means zone not given or not applicable. | Inconsistent spelling (Ost vs ost, West vs west, typo unkown). In 1946 and 1951 almost every line is both/unkown because the city was recorded as one network. The label is political and historical (see section 4). Not used yet. |
| frequenz | Headway: minutes between vehicles at 7:30 on a weekday. | integer | minutes, 0 to 274 | Original. Used for median\_headway\_min (section 3.3). | 171 lines have 0, which we read as "not available" (our assumption, the README does not say). 129 of these 171 are S-Bahn lines. | One time of day only. Extreme values exist (e.g. line A35E, 1964: 274 min; ferry 1946: 120 min). |
| länge (km) | Line length. | number | km | Original. | 2,013 blank (about 96%). | Not used. |
| start, ziel | First and last stop names. | text |  | Original. | Never blank. | Not used. |

**line\_stops.csv**

| Variable | Definition | Type | Values / unit | Origin and rule | Blank, missing, unknown | Limitations and ambiguities |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| line\_id | Line of the record. | integer | all values exist in lines.csv | Original. | Never blank. |  |
| stop\_order | Position of the stop along the line. | integer | 0, 1, 2, ... | Original. Not used in the coverage analysis. | Never blank. |  |
| stop\_id | Stop served. | integer | all values exist in stations.csv | Original. Used to find lines serving a district (section 3.3). | Never blank. | For the 34 duplicated stop\_id values it is unclear which of the two station rows is meant. |

**district polygons**

One row is one Berlin sub-district (Ortsteil), stored as a MultiPolygon. The file is one table taken from an Esri File Geodatabase. The rest of the geodatabase in the repository is incomplete, so only this table can be opened. Source as noted in the repository README: iGISMap / MapOG download of German administrative boundaries. The publisher's own metadata and the reference date of the boundaries have not been verified.

| Variable | Definition | Type | Values / unit | Origin and rule | Blank, missing, unknown | Limitations and ambiguities |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| name | Name of the sub-district. | text | 97 unique names. We use Kreuzberg and Wilmersdorf. | Original. | Never blank. | These are present-day sub-district boundaries, not the 1951 to 1984 boundaries (section 4). |
| schlüssel | Administrative key. | text | 12 digits, e.g. 110000020202 (Kreuzberg) | Original. | Never blank. | Meaning not documented by the source. Not used. |
| gdf | Area of the sub-district. | number | Kreuzberg 10,377,495; Wilmersdorf 7,161,063 (looks like m²) | Original. | Never blank. | Unit not documented. Our own area (10.44 and 7.16 km²) is within 0.6% of these values. |
| SHAPE\_Length, SHAPE\_Area | Perimeter and area stored by the GIS software. | number | Wilmersdorf SHAPE\_Area \= 19,277,280 | Original. | Never blank. | Do not use. They are computed in EPSG:3857, which inflates areas at Berlin's latitude by a factor of about 2.7. |
| geometry | Boundary polygon. | geometry | MultiPolygon, EPSG:3857 | Original. Reprojected to EPSG:25833 in the notebook. | Never blank. | Only the sub-district Wilmersdorf is used, not the larger historical borough (open decision, section 7). |

## Created Variables

**station-level variables** (created in the notebook) 

| Variable | Definition | Type | Values / unit | Origin and rule | Blank, missing, unknown | Limitations and ambiguities |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| year | Survey year of the stop record. | integer | 1951, 1961, 1967, 1976, 1984 (analysis years; 13 exist in the data) | Created. int(str(stop\_id)\[:4\]). | None blank. | The dataset has no opening or closing dates. A stop exists in the analysis for a year only if it appears in that year's timetable book. |
| lat, lon | Latitude and longitude as numbers. | float | decimal degrees | Created. Split standort at the comma, first value lat, second lon. | None blank. |  |
| geometry | Point location of the stop in metres. | geometry (Point) | EPSG:25833 | Created. Point built as x \= lon, y \= lat in EPSG:4326, then reprojected. | None blank. | Inherits the location uncertainty of standort. |
| buffer (not stored as a column) | Circle of radius radius\_m around each station. | geometry (Polygon) | metres | Created. geometry.buffer(r). All circles of one year are merged with union\_all(). |  | Straight-line distance, not walking distance. |

**coverage\_results.csv**  
One row is one district, one year and one radius (2 districts x 5 years x 3 radii \= 30 rows).

| Variable | Definition | Type | Values / unit | Origin and rule | Blank, missing, unknown | Limitations and ambiguities |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| year | Analysis year. | integer | 1951, 1961, 1967, 1976, 1984 | Created. | None blank. |  |
| district | District analysed. | text (category) | Kreuzberg, Wilmersdorf | Created. Chosen by the team. | None blank. | Discussed in the next section.  |
| radius\_m | Distance within which a station counts as covering a point. | integer | 250, 500, 1000 (metres) | Created. Parameter set by the team. | None blank. | At 1000 m both districts are 100% covered in every year, so this radius does not distinguish them.   |
| stations\_total | Station records of that year in all of Berlin used to build the buffers. | integer | 940 (1951), 1,379 (1961), 1,381 (1967), 1,796 (1976), 1,913 (1984) | Created. Count of rows with that year. | None blank. | Counts stop-mode records, not distinct places. Stations outside the district are included on purpose, because they can cover part of it. |
| stations\_inside | Station records of that year whose point lies inside the district polygon. | integer | e.g. Kreuzberg 39 (1951), 64 (1976) | Created. within(district polygon). | None blank. | Stations exactly on or very near the boundary are classified by estimated coordinates |
| area\_km2 | Area of the district polygon. | float | km². Kreuzberg 10.44, Wilmersdorf 7.16 | Created. Polygon area in EPSG:25833 divided by 1,000,000. | None blank. |  |
| covered\_km2 | Area of the district within radius\_m of at least one station. | float | km², from 0 to area\_km2 | Created. Area of (union of buffers) intersected with the district polygon. | None blank. | Overlapping circles count once. |
| coverage\_pct | Share of the district that is covered. | float | percent, 0 to 100 | Created. covered\_km2 / area\_km2 \* 100\. Saved unrounded. | None blank. | Shown rounded to one decimal in the notebook summary table. Measures spatial proximity only |

### 

**indicators\_by\_district.csv**  
One row is one district and one year. 

| Variable | Definition | Type | Values / unit | Origin and rule | Blank, missing, unknown | Limitations and ambiguities |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| stations\_inside | As in 3.2. | integer |  | Created. | None blank. |  |
| per\_km2 | Station records per km² of district. | float | records per km² | Created. stations\_inside / area\_km2. | None blank. |  |
| rail\_stations | Inside records of mode u-bahn or s-bahn. | integer |  | Created. Filter on typ. | None blank. | Interchange stations count once per mode. Rail stops are recorded completely, unlike bus and tram. |
| bus\_tram\_stations | Inside records of all other modes. | integer |  | Created. All records not counted as rail. | None blank. | Before 1975 only stops considered "important" are in the data. Increases up to 1976 are partly an effect of recording. |
| lines\_serving | Number of line records (a line in one year) with at least one stop inside the district. | integer |  | Created. line\_stops joined to inside stations, then to lines. | None blank. | A line that was renamed between years counts as a different record. |
| rail\_lines | Subset of lines\_serving with typ u-bahn or s-bahn. | integer |  | Created. | None blank. |  |
| median\_headway\_min | Median frequenz of the lines serving the district. | float | minutes at 7:30 on a weekday | Created. Lines with frequenz \= 0 are excluded. | None blank in the current output. | The exclusion removes mostly S-Bahn lines (129 of 171), so the median mostly reflects BVG modes.  |
| mean\_dist\_nearest\_m | Mean straight-line distance from a point in the district to the nearest station of that year. | float | metres | Created. Regular grid with 100 m spacing, points inside the polygon only, distance to the nearest station among all Berlin stations of that year. | None blank. | Result depends on grid spacing (100 m). Straight line, ignores streets, the Wall and rivers. |
| p90\_dist\_nearest\_m | 90th percentile of the same distances. | float | metres | Created. | None blank. | 90% of the district is closer than this value to a station. |

**Kreuzberg\_\*.csv and Wilmersdorf\_\*.csv**  
Created by Dataset/Processed/filteringstationsdataset.ipynb and filteringlinesdataset.ipynb (stations and lines inside each district, all 13 years together). They contain 722 (Kreuzberg) and 477 (Wilmersdorf) station rows and 249 and 200 line rows. They are not used for the coverage calculation, because that needs stations outside the district as well.

| Variable | Definition | Type | Values / unit | Origin and rule | Blank, missing, unknown | Limitations and ambiguities |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| Unnamed: 0 | Row number written by pandas when saving. | integer | 0, 1, 2, ... | Created by accident (index saved as a column). |  | Can be ignored or dropped. |
| location | Coordinates as a list of two text values. | text | "\['52.50', '13.38'\]" as \[lat, lon\] | Created. Split of standort. |  | Text, not numbers. |
| point | Station point in WKT. | text | POINT (lon lat) in EPSG:4326 | Created. |  | Longitude first, opposite order to location. |
| other columns | Same as the original file (stop\_id, stop\_name, typ, in\_linien, wikidata\_id). |  |  | Original. |  |  |

 

## Categories Created or Inherited  
None of these categories is neutral. Following the course readings the team discussed (Gitelman on data as always already shaped; Thylstrup on who controlled the infrastructure), we state each choice instead of hiding it.

1. District (Kreuzberg, Wilmersdorf). These are modern Ortsteil boundaries. In 1951 to 1984 the administrative units were boroughs (Bezirke), and the borough of Wilmersdorf was, to our knowledge, larger than the present sub-district (it also included Schmargendorf, Grunewald and Halensee; this should be verified before we publish). The two areas we compare are therefore a present-day construction applied to the past.   
2. ost\_west (East, West, both or unknown). This label reproduces the administrative and political division of the city as recorded by the timetable books. It belongs to lines, not to stations. Border-crossing lines, and the whole-city recording of 1946 and 1951, do not fit this split. We have not recoded it.   
3. typ (transport mode). The categories are those of the transport operators of the time (BVG, Reichsbahn, VEB Kraftverkehr). The team groups them into rail (u-bahn, s-bahn) and other. Reason: rail stops are recorded completely, while bus and tram stops are recorded selectively before 1975, so the groups differ in how complete the data are. The grouping hides differences between bus, tram, trolleybus and ferry.  
4. "Covered" (the central created category). A point of a district is covered if it lies within radius\_m metres, in a straight line, of at least one station record of that year. The category ignores direction of travel, frequency, walking routes, barriers such as the Wall, canals and rivers, and the fact that a station may not have been usable by residents of the other side of the Wall. It measures spatial proximity in the recorded data, not access in daily life.  
5. Analysis years (1951, 1961, 1967, 1976, 1984). Five of the 13 years in the dataset. 1951 is a whole year before the division of the network, 1961 is the year of the Wall, and 1976 is the first selected year after West Berlin timetables list all stops (from 1975). 1967 is chosen next to 1976 to have two years after the creation of the wall to see how things progressively settle down or evolve after the division of the city and 1984 was chosen as the last full year in the dataset before the fall of the wall.   
6. Radii (250, 500, 1000 m). Chosen by the team as a sensitivity range. 1000 m was kept as a reference even though it gives 100% everywhere. No historical source tells us how far people actually walked to a stop.

Disagreements and how they were resolved. No disagreement about these categories has been recorded so far. 

## Meaning of Blank, Zero and Missing Values (summary)

| Where | Value | Meaning |
| :---- | :---- | :---- |
| stations.csv, wikidata\_id | blank | No Wikidata item linked (76.5% of rows). |
| lines.csv, frequenz | 0 | Probably "headway not available". Not confirmed by the source. 171 lines, 129 of them S-Bahn. |
| lines.csv, dauer (min), länge (km) | blank | Not recorded (331 and 2,013 rows). |
| lines.csv, ost\_west | both/unkown | Zone not given or line serves both. Used for nearly all lines in 1946 and 1951\. |
| coverage\_pct | 100.0 | At least 99.95% covered (rounded). It may not be exactly 100\. |
| Whole dataset | no row for a stop | Stop not recorded. It may have existed but not been listed as "important". Absence is not evidence of no service. |

## Difficult and Borderline Cases

1. In the five analysis years, 61 station records lie within 30 m of the Kreuzberg boundary and 61 within 30 m of the Wilmersdorf boundary. Examples for Kreuzberg in 1951: Dudenstr. Ecke Mehringdamm (tram, 8.7 m inside), Schönleinstr. (U-Bahn, 23.5 m inside), Hermannplatz (tram, 23.8 m outside). Because many bus and tram locations are estimated, whether such a stop is "inside" is uncertain. The coverage percentages are not affected, because they use all Berlin stations, but stations\_inside is.  
2. Alt-Marzahn, Kirche (stop\_id 195618\) appears once as autobus (line A37) and once as oberleitungsbus (line O37) at identical coordinates. There are 34 IDs like this. We keep both rows. None of the 68 rows lies inside Kreuzberg or Wilmersdorf, so the station counts of the two districts are not affected. They are included in stations\_total and, because the two rows share one location, they do not change the buffers.  
3. In 479 cases, two or more rows of the same year share the same coordinates. These are interchange stations (one row per mode) or stops estimated at the same intersection. stations\_total and stations\_inside therefore count stop-mode records, not distinct places.  
4. Badstr. Ecke Pankstr. (stop\_id 194623\) and Badstr. Ecke Pankstrassse (194624) are only a few metres apart and appear to be the same location. Matching by name fails, so the analysis uses coordinates.  
5. Headway outliers and zeros. Line A35E (1964) has frequenz 274 and the 1946 ferry Wannsee to Pichelsberg 120\. S-Bahn lines mostly have 0\. Both affect median\_headway\_min.  
6. Ost (806 lines) and ost (62) mean the same, as do West and west. The six Ost/West lines are from 1956 and 1960\.   
7. Coordinate order. standort is "latitude, longitude", while GIS software expects x \= longitude, y \= latitude. Using the wrong order places the stations in the wrong country. The district polygons and the station file use opposite orders, which is why the team's first notebook reversed one of them.

## Known Limitations and Decisions  
### Limitations of the variables

- Bus and tram stops are incomplete before 1975\. All coverage and station-count comparisons across the 1976 boundary are partly an effect of recording.  
- The data are 13 snapshots of timetable books. They show the planned network at 7:30 on weekdays.  
- Straight-line coverage ignores the Wall, rivers, canals and street layout.  
- District boundaries are the ones recognized today.

### Decisions

1. Main radius (500 m proposed) and sensitivity radius (250 m).  
2. Only use the sub-district of Wilmersdorf and not the larger historical area.  
3. Treat frequenz \= 0 as missing   
   

## Filtered Datasets
### Heatmap Analysis:  
- Intermediate data  
  - Filename structure: {district}\_connected\_stations\_allyears.csv
  - All original columns with the exception of {district}\_connected, which is a Boolean that is always set to true, due to it being the variable filtered for in creating the dataset. Its calculation is given in heatmap\_{district}.ipynb, but can be described as whether or not the station’s coordinates fall within the polygon shape of the {district} in question, calculated using the geopandas package.  
- Final graphed data  
  - Filename structure: stations\_bydistrict\_{district}\_{year}.csv for the districts \[Kreuzberg, Wilmersdorf\] and years \[1951,1961,1967,1976,1984\].  
  - **Note**: the data used when graphing was retrieved from the json file with the same filepath, which was necessary for the geolocations to be properly preserved. The csv is given here because it is much easier to open and view the data structure. Some columns are inherited from the external dataset but were never used in analysis (schlüssel, gdf, SHAPE\_length, SHAPE\_area), so they are not elaborated on here.

| name | name | geometry | num\_{district} |
| :---- | :---- | :---- | :---- |
| Plain language definition | Name of district of Berlin | Geometric shape of the district via a series of coordinates | Number of stations in that district accessible from {district} |
| Data Type | string | Geopandas polygon | integer |
| Possible values | N/A | N/A | N/A |
| Unit | N/A | lat/long | N/A |
| source | External dataset | External dataset | Calculated in “heatmap\_{district}.ipynb” |
| original/created | original | original | created |
| Rules of creation | N/A | unknown | \+1 for every station from “Kreuzberg\_stations.csv” within district |
| Blank values | N/A | N/A | Zeros are true zero values |
| Limitations / ambiguities | Represents modern names | Cannot be perfectly exact due to limited number of points | Does not distinguish between transit types |
| Used in analysis? | True | True | True |

### Histogram Analysis:

Filename structure: {district}\_lines\_{year}.csv  
**Note**: These are just the original dataset lines.csv filtered by district and year. Thus, only the used columns are elaborated on.

| name | line\_id | jahr | frequenz |
| :---- | :---- | :---- | :---- |
| Plain language definition | Digits giving a unique value to each line, starts with the year | Year during which the lines were observed | Every how many minutes the line runs |
| Data Type | integer | integer | integer |
| Possible values | N/A | N/A | 0-120 |
| Unit | N/A | N/A | minutes |
| source | Original dataset | Original dataset | Original dataset |
| original/created | Original | Original | Original |
| Rules of creation | N/A | N/A | N/A |
| Blank values | N/A | N/A | N/A |
| Limitations / ambiguities | N/A | Specificity: time of year not given | Limitations: ideal case times, weekdays only |

### Pie Chart Analysis:

Filename structure: {district}\_lines\_{year}.csv  
**Note**: These are just the original dataset lines.csv filtered by district and year. Thus, only the used columns are elaborated on.

| name | jahr | typ |
| :---- | :---- | :---- |
| Plain language definition | Year during which the lines were observed | What kind of vehicle the line uses  |
| Data Type | integer | string |
| Possible values | N/A | “autobus” (bus) “straßenbahn” (tram) “s-bahn” (regional train) “u-bahn” (underground train/subway) |
| Unit | N/A | N/A |
| source | Original dataset | Original dataset |
| original/created | Original | Original |
| Rules of creation | N/A | N/A |
| Blank values | N/A | N/A |
| Limitations / ambiguities | Specificity: time of year not given | Limitations: does not provide any detail on the vehicles (capacity, accessibility, year of construction, etc.) |
