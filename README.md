# Analysis of NYPD Hate Crimes Dataset — 2019-01-01 to 2024-09-30

This repository contains data and code analyzing NYPD Hate Crime data. 

## Data

This analysis uses the NYPD Hate Crimes public dataset (produced by requirement under [New York City Administrative Code § 14-161](https://codelibrary.amlegal.com/codes/newyorkcity/latest/NYCadmin/0-0-0-25275). 

- Name of source:
  - `NYPD_Hate_Crimes_20241206.csv`: Raw data
  - Live and updated at [`NYC OpenData`](https://data.cityofnewyork.us/Public-Safety/NYPD-Hate-Crimes/bqiq-cu78/about_data) on a quarterly basis

The sheet contains the following columns (as defined by the OpenData dataset info):

- `Full Complaint ID` — Identifier for each hate crimes incident
- `Complaint Year Number` — Year in which incident occurred
- `Month Number` — Month in which incident occurred
- `Record Create Date` — Date report was filed
- `Complaint Precinct Code` — NYPD Precinct in which incident occurred
- `Patrol Borough Name` — NYPD Patrol Borough in which incident occurred
- `County` — County in which incident occurred
- `Law Code Category Description` — Category of offense
- `Offense Description` — A description of the offense
- `PD Code Description` — The NYPD description of the offense
- `Bias Motive Description` — NYPD category of hate crime or bias type
- `Offense Category` — General categorization of hate crime type
- `Arrest Date` — Date arrest was made (if arrest happened)
- `Arrest Id` — Identifier for arrest (if made)

We'll also be using a key for further contextualizing NYPD Hate Crime data in the context of UCR/NIBRS Federal reporting and NY State DCJS reporting. 

- Name of source:
  - `offense_categorization_key.xlsx`
 
This sheet contains the following columns (further explained in the 'Data Dictionary' tab of the file): 

- `Offense` — Offense sourced from aggregate 'PD Code Descriptions' from NYPD Hate Crimes dataset
- `Legal_Level` — Law Code Category Description keypairs sourced from NYPD Hate Crimes dataset
- `NYS_Specified` — "Specified Offense" status defined in NYS Penal Code § 485.05(3) Hate Crimes
- `NIBRS_Code` — Matching NIBRS Offense Code(s) from the federal NIBRS User Manual
- `NIBRS_Group` — NIBRS Offense group classification. Group A offenses are considered more serious and are reported federally even without an arrest. Group B offenses are only reported federally if there has been an arrest.
- `Crime_Against` — UCR/NIBRS Crime Classification by motivation: crimes against persons, crimes against society, crimes against property. Defined in UCR portal methodology.
- `DCJS_Hate_Crimes` — Whether the offense is listed in the DCJS 'Hate Crime Penal Law Reference Table'
- `Violent` — Whether the offense code indicates direct physical harm in the complaint


## Methodology

The notebook [`2019-24-nypd-hate-crimes-analysis.ipynb`](notebooks/2019-24-nypd-hate-crimes-analysis.ipynb) performs the following analyses on NYPD hate crime data:

### Comparing Hate Crimes: Simple Counts
- Examines count of incidents per:
  - NIBRS Crime category (persons/property/society)
  - Borough
  - Precinct
  - Offense category
  - Bias motive

### Comparing Hate Crimes: Bias Category Tables 
- Analyzes three groupings:
  - Full list of Bias Motive Description categories from NYPD
  - Aggregated Offense Categories grouping bias motives from NYPD 
  - Custom aggregate comparison of Anti-LGBTQ, Anti-Religious and Anti-Race/Ethnicity bias motives
- Creates dataframes with calculated statistics about hate crime data per grouping

### Comparing Hate Crimes: Plotting Hate Crime Data Over Time by Category 

- Creates plotly graph visualizations of:
  - Monthly incident counts with overlaid bar charts showing total vs violent incidents 
  - Quarterly percentage trends of violent incidents on the opposite axis
  - Iteratively creates and displays comparative graphs at three levels of aggregation:
    - Full dataset by NYPD Offense Category 
    - Full dataset by specific Bias Motive Description
    - Individual category deep-dives (e.g., "Sexual Orientation" or "Anti-Jewish")

### Mapping Hate Crime Data by Precinct

For this section we move to a second notebook [`precinct_hate_crime_map.ipynb`](notebooks/precinct_hate_crime_map.ipynb) to map our data across the NYPD precinct does in our dataset using the [datawrapper](https://datawrapper.readthedocs.io/en/latest/) library. 

- Creates interactive choropleth maps showing hate crime distribution across NYPD precincts
- Includes detailed tooltips showing breakdowns by category, violence rates, and arrest rates

### Reporting Resource: Filtered Arrest List
- Creates filtered datasets of reported hate crimes with arrests
- Outputs arrest data that can be used to request NYPD Arrest Reports or identify specific cases in ECourts. 


## Outputs

The notebooks output these spreadsheets:

- [`output/hate_crimes_w_codecats.csv`](output/hate_crimes_w_codecats.csv) which contains the raw data with the added column futher categorizing PD Code Descriptions from 'Part 1.'
- [`output/anti_lgbt_hate_crime_arrests.csv`](output/anti_lgbt_hate_crime_arrests.csv) which contains the arrest data from 'Part 3.' 

It also generates an interactive datawrapper map on the user's datawrapper account. 

## Running the analysis yourself

You can run the analysis yourself. To do so, you'll need the following installed on your computer:

- Python 3
- pandas for data analysis
- plotly for visualizations
- datawrapper for mapping (requires [API token](https://developer.datawrapper.de/docs/getting-started))
- The rest of the Python libraries specified in [`requirements.txt`](requirements.txt)

## Licensing

All code in this repository is available under the [MIT License](https://opensource.org/licenses/MIT). The data file in the output/ directory is available under the [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0) license. All files in the data/ directory are released into the public domain.

## Feedback / Questions?

Contact Audrey Nielsen at [nielsenau@gmail.com](mailto:nielsenau@gmail.com)