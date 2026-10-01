  
**Research Question**

“How did public transportation connectivity in Kreuzberg compare to Wilmersdorf during the restructuring and division of Berlin between 1949 and 1989?”

**Relevant Literature**

**Scheiner (2005)** compares activity in areas on both sides of the Berlin Wall and shows that people’s mobility was influenced not only by transport infrastructure but also by their backgrounds, experiences and attitudes towards other sides of the city. It will support our idea of analysing Berlin’s historical transportation network and examining how areas such as Kreuzberg were connected with the city. 

**Hochmuth (2017)** explains how Kreuzberg went from a central and relevant part of Berlin to a marginal district after the Wall was built in 1961\. It became home mostly to poor workers, older people, and migrants. Kreuzberg only became central again after the Wall fell in 1989, when artists and activists rediscovered the area, leading to its gentrification today. This is useful because it gives a clear historical picture of Kreuzberg's decline after 1961 that we need for the comparison with Wilmersdorf.

The government page **Bezirksamt Charlottenburg-Wilmersdorf von Berlin (2023)**, explains that this area grew fast after 1890 as politicians tried to attract wealthy families, building nice schools and housing. A new U-Bahn line opened in 1913, connecting Wilmersdorf to the city center. By the time of Berlin's division, Wilmersdorf remained a quiet, high income residential area with almost no industry. Useful as background for our research and to give us a more complete scene of the area we are trying to study.

**Mishra et al. (2012)** explain how to measure how "connected" a public transport network is. The authors use graph theory to look at connectivity at different levels: a single stop, a single line, a transfer point, and a whole area. They measure things like how often buses or trains come, how fast they are, and how many people they can carry.   
This paper is useful for this project because it shows a way to measure "connectivity" using real numbers (frequency, number of lines, etc.), instead of just describing it in words. This could give us useful insight on a way to measure connectivity for our project as well .

**Häußermann & Kapphan (2004)** look at how Berlin's districts changed from the Cold War period until after reunification. The authors explain how West Berlin's districts developed differently depending on things like industry, housing type, and connection to the rest of the city.  
It shows which areas became poorer and which stayed wealthy, and why.   
This is useful because it gives real historical background on how Berlin's neighborhoods split into rich and poor areas, which supports the comparison this paper makes between Kreuzberg (low income area) and Wilmersdorf (high income area).

**Thesis Statement**

The establishment of the Berlin Wall effectively divided the city that not only made Berlin split into two politically distinct opposed parts, but also affected transportation within one single region. Kreuzberg and Wilmersdorf were two administrative districts in West Berlin. Kreuzberg was directly adjacent to the Berlin Wall while Wilmersdorf was located further west, which means there exists a considerable distance from the border. The geographical location in relation to the construction of the wall resulted in more than only a transportational transformation, but also a social-economic one. Despite our fascination for the subject, this paper won’t be able to research the relation between the two transformations, partly due to limitations in the extent of our dataset, the available resources and time for this project.

Alternatively the focus will be put on the comparative study in connectivity between the two administrative districts. Through the different performance indicators set out by Mishra et al. (2004), this paper seeks to measure the transportation systems in Berlin (e.g. number of connections to nodes and speed coefficient). We hypothesize that Wilmersdorf’s indicators will provide an argument for better connectivity within Berlin’s transportation, relative to Kreuzberg. This might provide a basis for further research into a deeper comparative study, possibly exploring different factors or an increased number of districts.

**Dataset Critique**

Kim-Baumann’s temporal model of Berlin’s public transport system is an extensive case study into not only temporal dataset modelling, but also the integration of bottom-down collaborative source material with the historical humanities. The integration of temporal data would allow for complexer models and a more accurate historical reality, however this is only the case if it’s done systematically. Wikidata lacks the required consistency that BVG’s (Berlin Transport Company) historical data-set has on the U-Bahn and S-Bahn. Baumann’s computational investigation with SPARQLWrapper illustrates this point more clearly, the investigation showed that wikidata’s query design is inconsistent in its referencing practices and coverage (e.g. modality). Another point of tension is the frequency data and granularity.

Essentially the data-set is a group of snapshots taken in space and time. Meaning that they fail to provide detail on hourly, daily, or seasonal variations. While systematic temporal data might sound like an oxymoron, Kim-Baumann demonstrates that these two concepts can effectively be reconciled.

**Action Plan**

**Analysis**  
The given dataset mainly consists of three related csv files named stations.csv, lines.csv and line\_stops.csv. We shall first select needed station locations by latitude and longitude in file stations.csv after determining the scope of the administrative regions. Latitude and longitude data are accurate to ten significant decimal places so roughly estimating, we can extract approximately 600 records for each administrative region from nearly 18,000 site data points.  
In terms of time selection, based on 13 available years we will choose 5 years to represent the arc of the story. 

The last two certain years before 1961 are meant to be used for confirming the connectivity as the baseline before the formation of the Berlin Wall (1946 is not in the range owing to the timeframe of our research from 1949 to 1989). 1961 is going to be checked for the immediate effect of the Wall's construction and around 3-6 years after 1961 (1964 and 1967\) will help us compare the differences after the network settles into its new, divided shape. One year roughly halfway to 1989 (probably 1976\) is selected to identify the mid-period and 1984 as the last available year before 1989 represents the final state of the divided network.

The most apparent indicators we can use from the dataset include the number of U-bahn, S-bahn and bus lines in each region in each year and the number of other stations directly accessible via these lines. Frequencies provided can also be used though the many null values in particular stations may present obstacles in data processing and will need to be evaluated critically.

**Action Plan:**

1. First: Identify the locations of the two districts and Filter stations meet the requirements by latitude and longitude  
2. Link stations and lines (simultaneously marking the year)  
3. Entract specific years which are useful for research by the decided standards  
4. Define connectivities as measurable indicators according to sources and the dataset we actually have  
5. Analyze by the indicators  
6. Visualize the statistical results by charts or graphs  
7. Link conclusions to secondary literature and interpret

**Expected results:**

1. A filtered and selected dataset only showing transportation of Kreuzberg and Wilmersdorf  
2. Indicators to identify the transportation connectivity  
3. A chart or graph showing the comparisons of Kreuzberg and Wilmersdorf, where we expected to show Kreuzberg experiencing a greater decline than Wilmersdorf in transportation connectivity especially in the number of available lines and the phenomenon  is expected to exist during several sample years.  
4. Visualizations and Interpretations linked to the secondary literature  
5. Notes about uncertainties and limitations, various documentation

**Team Charter**

Team Members

* Junfeng Hsu  
  - Major: History  
  - Background: Chinese, exchanging here  
  - Project-Related Strengths: basic python  
  - Project Roles: Analytical Writer: Analysis, Writing, Problem-Solving  
* Katharina Jennrich  
  - Major: Ancient Studies specializing in the Ancient Near East  
  - Background: German parents, born in the Netherlands, attended an international High School  
  - Project-Related Strengths: research in the direction of literature reviews, writing, basic python skills  
  - Project Roles: Writer and Quality Control: Writing, Editing, Cross-Checking, Submissions  
* Micha de Tombe  
  - Major: History  
  - Background: Dutch, Indonesian family background  
  - Project-Related Strengths: critical analysis, making comparative relations and literature reviews.   
  - Project Roles: Historical contextual research lead and documentation lead: Research, Writing, Documentation  
* Martina Panzani  
  - Major: Computer Science  
  - Background: Italian, British family background, attended a science focused high school   
  - Project-Related Strengths: coding abilities and graphic abilities  
  - Project Roles: Data and technical lead and Co-Project Coordinator: Coding, Organization  
* Mai Ngo  
  - Major: Business Analytics  
  - Background: Vietnamese, attend language specialized high school  
  - Project-Related Strengths: critical thinking, using programming, statistical tools   
  - Project Roles: Documentation and Repository Manager: Organization, Writing

Communication 

Real-time communication will occur in the WhatsApp group, but details about roles and deadlines will be noted in the team charter. 

In-person discussions occur during Thursday seminars, with the goal of establishing expectations for asynchronous work. Further in-person or online meetings will be discussed for each assignment.

Deliverables Log

**Assignment 1**: Project Proposal and Team Charter

* ALL: Draft ready for Thursday (17.9), finished section by Sunday (20.9)  
* Mai: Research Question  
* Martina: Thesis Statement  
* Micha: Dataset Critique  
* Hsu: Action Plan and Formatting  
* Katharina: Team Charter and Compilation

**Assignment 1 Resit:** Rephrase RQ and Thesis to match each other and the available data

* Due **Tuesday (29.9)**, final version ready latest **Monday (28.9)**  
* Mai: GitHub repository, reference compilation, RQ editing  
* Martina: reference sourcing and summaries, dataset analysis  
* Micha: thesis statement  
* Hsu: action plan  
* Katharina: elaborate on Team Charter, add deliverables, reference sourcing

**Week 4 Project Milestone: All sections for Wednesday (30.9)**

* label the raw-data inventory  
  * Writer: Micha / Hsu (as time permits)  
* front page for GitHub  
  * Sub-Coder / Writer: Katharina / Mai (as time permits)  
* the first processing script or manual protocol;  
  * Coder: Martina  
* a processing log;  
  * Writer: Hsu  
* limitations and uncertainty logs  
  * Writer / Analysis: Katharina  
* identify data-quality problems;  
  * Martina: transfer information from presentation script to github  
  * Writer / Analysis: Mai

**Week 5 Project Milestone: for Monday (5.10)**

* two or three initial results;  
  * Coder \+ Writer  
* at least one counterexample or complication;  
  * Writer  
* one visualisation draft;  
  * (Sub-)Coder  
* an explanation of what cannot be concluded.  
  * Writer

**Week 6: Working Towards Presentation**

* final visualisations: by Saturday (10.10)  
  * Coder  
* presentation narrative: by Thursday evening (8.10)  
  * Writer  
* methods summary;  
  * Writer  
* limitations statement;  
  * Writer / Analysis

**Project Presentation: Sunday (11.10)**

* Draft of each individual part by Saturday (10.10), to be distributed as preferred  
* Practice and revisions (11.10 noon)

**Week 6: Working Towards GitHub completion: Sunday (18.10)**

* ALL: No explicitly code-heavy tasks, to be distributed as preferred, all due by 18.10  
* repository documentation  
* individual contribution records  
* dataset biography  
* workflow diagram  
* codebook or data dictionary  
* final updates to processing log and uncertainty register  
* bias and positionality statement  
* final updates to analysis files, visualisations, limitations statement  
* AI-use statement  
* contribution statement

Concerns, Observations, and Challenges

- Challenge: research question version A rejected for lacking data and for incongruous RQ \+ Thesis  
- Concern: must ensure thesis does not claim causation for elements known only via additional literature  
- Challenge: filtering our data by location \- too large to do manually, may be challenging to automate  
- Decision: do we combine all of the greater area of Wilmersdorf, or do we take just the smaller district of Wilmersdorf

**Formatted Citations**

*Geschichte Wilmersdorfs im Überblick*. (2023, August 11). [https://www.berlin.de/ba-charlottenburg-wilmersdorf/ueber-den-bezirk/geschichte/artikel.181127.php](https://www.berlin.de/ba-charlottenburg-wilmersdorf/ueber-den-bezirk/geschichte/artikel.181127.php)  
Haeussermann, H., & Kapphan, A. (2004). BERLIN: FROM DIVIDED INTO FRAGMENTED CITY. *Επιθεώρηση Κοινωνικών Ερευνών*, *113*, 25\. [https://doi.org/10.12681/grsr.9216](https://doi.org/10.12681/grsr.9216)  
Hochmuth, H. (2017). The return of Berlin-Kreuzberg. Brought back from the margins by memory. *Journal of Contemporary European Studies*, *25*(4), 470–480. [https://doi.org/10.1080/14782804.2017.1361817](https://doi.org/10.1080/14782804.2017.1361817)  
Mishra, S., Welch, T. F., & Jha, M. K. (2012). Performance indicators for public transit connectivity in multi-modal transportation networks. *Transportation Research Part A: Policy and Practice*, *46*(7), 1066–1085. [https://doi.org/10.1016/j.tra.2012.04.006](https://doi.org/10.1016/j.tra.2012.04.006)  
Scheiner, J. (2005). Daily Mobility in Berlin: On ‘Inner Unity’ and the Explanation of Travel Behaviour. *European Journal of Transport and Infrastructure Research*, *5*(3). [https://doi.org/10.18757/ejtir.2005.5.3.4399](https://doi.org/10.18757/ejtir.2005.5.3.4399)