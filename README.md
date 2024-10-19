# Analysis of NYPD Hate Crimes Dataset — 2019-01-01 to 2024-06-25 

This repository contains data and code analyzing NYPD Hate Crime data. 

## Data

This analysis uses the NYPD Hate Crimes quarterly dataset. 

- Name of source:
  - `NYPD_Hate_Crimes_20240929.csv`: Raw data
  - Live and updated at [`NYC OpenData`](https://data.cityofnewyork.us/Public-Safety/NYPD-Hate-Crimes/bqiq-cu78/about_data) 

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

## Methodology

The notebook [`2019-24-nypd-hate-crimes-analysis.ipynb`](notebooks/2019-24-nypd-hate-crimes-analysis.ipynb) performs the following analyses:

##### Part 1: Comparing Hate Crimes by Bias Category and Criminal Code Category

- Prepare the data and add a column grouping PD Codes into categories
- Examine the count of incidents by:
  - Code Category
  - Patrol Borough
  - Bias (category and specific)
- Group anti-LGBTQ bias motives
- Filter incidents with bias motives targeting:
  - religious groups,
  - ant-LGBTQ bias motives, and
  - Race/Color and Ethnicity/Ancestry
- Plot incidents against those bias groups against each other over time

##### Part 2: Violent Hate Crimes 

- Analyze and plot frequency of VIOLENT code category hate crimes by bias motive
- Plot the percentage of total reports per bias category that were violent by month
- Plot reported hate crimes by code category as pie charts


##### Part 3: Analyzing Arrest Data

- Filter reported hate crimes by those Arrest ID and Arrest Date to identify those incidents that resulted in an arrest
- Create dataframe and csv of arrests for reported hate crimes with an anti-LGBTQ bias motive. 


## Outputs

The notebooks output these spreadsheets:

- [`output/hate_crimes_w_codecats.csv`](output/hate_crimes_w_codecats.csv) which contains the raw data with the added column futher categorizing PD Code Descriptions from 'Part 1.'
- [`output/anti_lgbt_hate_crime_arrests.csv`](output/anti_lgbt_hate_crime_arrests.csv) which contains the arrest data from 'Part 3.' 



## Running the analysis yourself

You can run the analysis yourself. To do so, you'll need the following installed on your computer:

- Python 3
- The Python libraries specified in [`requirements.txt`](requirements.txt)

## Licensing

All code in this repository is available under the [MIT License](https://opensource.org/licenses/MIT). The data file in the output/ directory is available under the [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0) license. All files in the data/ directory are released into the public domain.

## Feedback / Questions?

Contact Audrey Nielsen at [nielsenau@gmail.com](mailto:nielsenau@gmail.com)