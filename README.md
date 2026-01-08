# European Energy Consumption Analysis (1990-2023)

## Project Overview

This project analyses long-term energy consumption trends across European countries between 1990 and 2023, focusing on four major fuel categories:

- **Oil & Petroleum Products**: include crude oil and petroleum derivatives such as gasoline, diesel, kerosene, fuel oil, heating oil, bitumen and other oil-based products. Crude oil is a naturally occurring liquid fossil fuel extracted from underground reservoirs and refined into various petroleum products for transportation, heating, and industrial use.
- **Solid Fossil Fuels**: include coal (hard coal, lignite), peat, and coke. These are carbon-rich energy sources formed from ancient plant material over millions of years, primarily used for electricity generation and industrial processes.
- **Natural Gas**: a fossil fuel composed mainly of methane, used for heating, electricity generation, and as an industrial feedstock. It is not solid like coal or liquid like oil, but exists in a gaseous state at room temperature and pressure. 
- **Renewable Energy Sources**: non-fossil energy sources that are naturally replenished, including wind, hydro, solar, geothermal, biomass, and biogases. These sources have a much lower environmental impact compared to fossil fuels and are key to the energy transition towards sustainability.

Using official Eurostat energy balance data, the project examines how energy consumption patterns have evolved at both EU level and country level, with particular attention to:
- the decline in fossil fuel usage
- the rise of renewable energy sources
- structural differences in national energy profiles
- recent trends that may shape future energy consumption

The project combines data cleaning, database storage, exploratory data analysis and geospatial visualisation to provide insights into the EU's energy transition over the past three decades.

## Data Source

The primary data source for this analysis is the Eurostat energy balance dataset, which provides comprehensive statistics on energy production, consumption, and trade for the European states. The dataset includes detailed breakdowns by fuel type and sector, allowing for in-depth analysis of energy trends.  
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
- removes metadata and unnecessary columns,
- standardises column names,
- converts years and consumption values to appropriate data types,
- removes invalid or missing observations,
- aggregates data to one row per country per year for each fuel type.

This produces consistent, analysis-ready datasets for each fuel type.
Each cleaned dataset is labelled with its corresponding fuel type and combined into a single DataFrame (`all_energy`) to enable cross-fuel comparisons, EU-level aggregations, and trend analyses.
The cleaned and aggregated dataset is stored in a MySQL database for efficient querying and analysis.  

Before proceeding with the analysis and visualization, data is reshaped into pivot tables using the `pivot_data()` function. Additional cleaning steps are then performed to ensure data integrity and consistency:
- Incomplete years (e.g., 2024) are excluded due to widespread missing data.
- Countries with insufficient data coverage across the years are excluded from comparative analyses only.
- No data imputation is performed; analyses are based solely on available data.

### Exploratory Data Analysis and Visualisation  

The exploratory data analysis (EDA) investigates long-term trends, structural shifts, and regional patterns in energy consumption across Europe between 1990 and 2023. Using harmonized Eurostat data, the analysis covers four major fuel categories: oil and petroleum products, solid fossil fuels, natural gas, and renewable energy sources, capturing both total consumption and relative shares within national and EU energy mixes.  

Key analyses include:

1. EU-level aggregated consumption trends by fuel type (1990-2023)

2. Geospatial visualisations of energy consumption by country and fuel type (2015-2023)

3. Country-level comparative analyses

4. Energy consumption by fuel type in Ireland (1990 - 2023)



## Key Findings and Conclusions

**EU-Level Trends**

- Solid fossil fuels declined ~69%, oil & petroleum ~24%, natural gas ~19%, while renewables grew ~171%, reflecting a clear shift toward cleaner energy, with natural gas serving as a transitional fuel.
- Solid fossil fuels’ share dropped 20 percentage points, while renewables rose by a similar margin
- Regional heterogeneity exists: Nordic countries lead in renewables, Western/Southern Europe show mixed adoption, Central/Eastern Europe retain higher coal reliance
- Germany shows high consumption across all four fuel types, highlighting its diversified portfolio  
- Annual consumption by country for the top 10 consuming nations per fuel type (1990–2023), reveal how large economies like Germany, France, Italy, and Spain dominate across multiple fuels, while other countries are specialized in certain fuel types.
- National energy mixes in 2023 highlight structural differences. For instance, Malta, Cyprus, and Luxembourg rely heavily on oil, while Serbia, Kosovo, Czechia, and Bosnia and Herzegovina still consume significant solid fossil fuels. Sweden, Finland, and Iceland stand out for high renewable shares.  

**Ireland-Specific Trends**
- Oil & petroleum consumption increased ~54%, solid fossil fuels fell ~77%, natural gas rose ~102%, and renewables grew ~700%

### Overall Conclusion

Europe’s energy system is transitioning toward low-carbon sources, with fossil fuels declining, renewables growing rapidly, and natural gas serving as a bridge fuel.
The surge in renewable energy consumption highlights the accelerating adoption of low-carbon technologies and the growing impact of European policies such as the 2008 [EU Climate and Energy Package](https://climate.ec.europa.eu/document/download/80f7df0c-2294-4ce9-afeb-1d1885e3063f_en) and the [European Green Deal](https://commission.europa.eu/strategy-and-policy/priorities-2019-2024/european-green-deal_en).


At the national level, Ireland has experienced significant shifts in its energy consumption patterns over the past three decades. The country has seen a substantial increase in renewable energy usage, reflecting its commitment to sustainable energy practices. 
However, Ireland's energy landscape remains complex, with oil and petroleum products still constituting a significant portion of the energy mix, particularly in the transport sector. 
Ireland continues to rely heavily on [energy imports](https://irelandenergy2050.ie/present/oil-and-gas/?q=how-dependent-on-imports-are-we), with transport, home heating, and power generation sectors still dependent on imported fuels, although the operation of the [Corrib](https://www.rpsgroup.com/projects/corrib-onshore-gas-pipeline/) gas field since 2015 has helped reduce the country’s reliance on imported gas.


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
This project uses a MySQL database to store and manage cleaned energy consumption data.
Installation of [MySQL Server](https://www.mysql.com/) and [MySQL Workbench](https://dev.mysql.com/downloads/workbench/) is required to create, inspect, and manage the database used throughout the analysis.

### End

