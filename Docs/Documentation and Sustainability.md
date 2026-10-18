## Repository Overview
The repository is made up of five main folders:
- Analysis: jupyter notebooks of the analysis code
- Dataset: all datasets used, including external ones and our processed and filtered data
- Docs: all written discussions and explanations of our project
- Results: the main filtered datasets and a detailed discussion of our findings
- Visualizations: all image files of our visual presentations

## Tools and External Data

The only coding language used is python, used in jupyter notebooks. Various packages were used including Pandas, GeoPandas, and MatPlotLib. 

An external dataset was used to define district borders, which is hosted on MapOG (https://story.mapog.com/app/gisdata/germany/Postal%20Code) but can best be accessed via this link to German Post Code Districts: https://www.igismap.com/download-germany-administrative-boundary-shapefiles-states-districts-postal-codes/. This dataset has been included in the repository, so will be accessible should the host website cease to exist, though its use may not be legally guaranteed in that situation. 

## Preservation and Reuse

Currently both the original dataset and the external dataset are hosted on well-maintained sites, so their preservation may not seem to be of immediate concern. Similarly, this repository as hosted on GitHub is considered well preserved. However, there is always a concern of websites being unexpectedly removed, or servers being inaccessible without warning. An additional layer of safekeeping would be to keep individual files on personal devices, since additionally hosting this project on a personal or university server would be a considerable cost of effort and money in comparison to the relatively small scope and impact of the project. 

This project has some avenues for reuse, mainly as inspiration or a jumping-off point for similar projects. Our sectioning of the data into districts using external data could be repeated with that same data, and used to complete a similar analysis on a larger scale. All of our processes are easily reproducible, however, so any future reuse would likely not use our filtered or processed data, instead choosing to complete the same processes independently for insight and oversight.
