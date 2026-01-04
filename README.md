# EU Energy Consumption Analysis (1990-2023)

## Project Overview

This project analyses long-term energy consumption trends across European countries between 1990 and 2023, focusing on four major fuel categories:

- Oil & Petroleum Products
- Solid Fossil Fuels
- Natural Gas 
- Renewable Energy Sources

Using official Eurostat energy balance data, the project examines how energy consumption patterns have evolved at both EU level and country level, with particular attention to:
- the decline in fossil fuel usage
- the rise of renewable energy sources
- structural differences in national energy profiles
- recent trends that may shape future energy consumption

The project combines data cleaning, database storage, exploratory data analysis and geospatial visualisation to provide insights into the EU's energy transition over the past three decades.

## Data Source

The primary data source for this analysis is the Eurostat energy balance dataset, which provides comprehensive statistics on energy production, consumption, and trade for EU member states. The dataset includes detailed breakdowns by fuel type and sector, allowing for in-depth analysis of energy trends.  
This project utilises the following Eurostat dataset:
- [Eurostat Energy Balance Data](https://ec.europa.eu/eurostat/databrowser/view/nrg_bal_c/default/table?lang=en) (nrg_bal_c)
  - Unit: Thousands tonnes of oil equivalent (KTOE)
  - Coverage: European countries from 1990 to 2024
  - Frequency: Annual
  - Fuel Categories: Oil & Petroleum Products, Solid Fossil Fuels, Natural Gas, Renewable Energy Sources
- Natural Earth for geospatial visualisations (1:110m):
  - [Natural Earth Data](https://www.naturalearthdata.com/downloads/10m-cultural-vectors/10m-admin-0-countries/)

All datasets used in this project are publicly available and can be accessed through the provided links.

## Project Structure
The project is structured as follows:

- `notebook/`: Jupyter notebook for data cleaning, analysis, and visualisation.
- `README.md`: Project overview and documentation.
- `requirements.txt`: List of Python dependencies.
- `.gitignore`

### Data Preparation
The raw Eurostat energy balance data is cleaned and aggregated using the `clean_and_aggregate()` function that:
- removed metadata and unnecessary columns,
- standardises column names,
- converts years and consumption values to appropriate data types,
- removes invalid or missing observations,
- aggregates data to one row per country per year for each fuel type.

This produces consistent, analysis-ready datasets for each fuel type.
Each cleaned dataset is with its corresponding fuel type and combined into a single DataFrame (`all_energy`) to enable cross-fuel comparisons, EU-level aggregations, and trend analyses.
The cleaned and aggregated dataset is stored in a MySQL database for efficient querying and analysis.  

Before proceeding with the analysis and visualization, data is reshaped into pivot tables using the `pivot_data()` function. Additional cleaning steps are then performed to ensure data integrity and consistency:
- Incomplete years (e.g., 2024) are excluded due to widespread missing data.
- Countries with insufficient data coverage across the years are excluded from comparative analyses only.
- No data imputation is performed; analyses are based solely on available data.

### Exploratory Data Analysis and Visualisation  

The exploratory data analysis (EDA) focuses on identifying key trends and patterns in energy consumption across the EU. Key analyses include:

1. EU-level aggregated consumption trends by fuel type from 1990 to 2023.

   - Bar charts for each fuel type showing total consumption per year (KTOE)
   - Line charts comparing consumption trends across fuel types (KTOE)
   - Percentage share of each fuel type in total EU energy consumption over time (% share)

2. Geospatial visualisations of energy consumption by country and fuel type from 2015 to 2023.
3. Country-level comparative analyses.

   - heatmaps showing consumption levels by country and year for the top 10 consuming countries per fuel type (1990-2023)
   - stacked percentage bar charts showing national energy mixes for 2023.  

4. Energy consumption by fuel type in Ireland.

## Requirements
The project requires the following Python libraries:
- pandas
- matplotlib
- seaborn
- mysql-connector-python
- geopandas

These can be installed via pip using the provided `requirements.txt` file:

``` 
pip install -r requirements.txt
```

### End

