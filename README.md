# COVID-19 Global Vaccinations Dashboard

## Project Goal

- Utilize **SQL** to query a dataset and extract insights into the **COVID-19 pandemic** on a global scale.
- Create a **Tableau Dashboard** to visualize key metrics found within the dataset.

## Dataset Information

**Datasource:** [Our World in Data](https://ourworldindata.org/coronavirus)

*Date range used of 1/1/2020 to 3/30/2023

## SQL Data Exploration of COVID-19 data

### 1. Aggregating Cases and Deaths by Country/Region

~~~~sql
SELECT 	location, 
		MAX(total_cases) AS total_cases, 
        MAX(total_deaths) AS total_deaths 
FROM 	`covid19_data.covid19-data` 
WHERE 	location NOT LIKE '%income%' AND 
		location NOT LIKE '%World%' AND 
        (total_cases IS NOT NULL OR total_deaths IS NOT NULL) 
GROUP BY location 
ORDER BY total_cases DESC;
~~~~

**Result Snapshot:**

- **Location:** United States of America, Total Cases: **102,697,566**, Total Deaths: **1,117,054**
- **Location:** Japan, Total Cases: **33,421,785**, Total Deaths: **73,747**
- **Location:** United Kingdom, Total Cases: **24,286,411**, Total Deaths: **210,396**

### 2. Trend Analysis

~~~~sql
SELECT date, SUM(new_cases) AS daily_cases, SUM(new_deaths) AS daily_deaths 
FROM `covid19_data.covid19-data` 
GROUP BY date  
HAVING daily_cases > 0 OR daily_deaths > 0 
ORDER BY date;
~~~~

**Result Snapshot:**

- **Date:** Wed Feb 12 2020, Daily Cases: **60,641**, Daily Deaths: **1,012**
- **Date:** Fri Feb 12 2021, Daily Cases: **1715564**, Daily Deaths: **52,646**
- **Date:** Sat Feb 12 2022, Daily Cases: **8326531**, Daily Deaths: **43,797**
- **Date:** Sun Feb 12 2023, Daily Cases: **471139**, Daily Deaths: **3162**
