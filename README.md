# COVID-19 Global Vaccinations Dashboard

## Project Goal

- Utilize **SQL** to query a dataset and extract insights into the **COVID-19 pandemic** on a global scale.
- Create a **Tableau Dashboard** to visualize key metrics found within the dataset.

## Dataset Information

Datasource: [Our World in Data](https://ourworldindata.org/coronavirus)

*Date range used of 1/1/2020 to 3/30/2023

## SQL Data Exploration of COVID-19 data

### 1. Aggregating Cases and Deaths by Country/Region

SELECT 	location, 
		MAX(total_cases) AS total_cases, 
        MAX(total_deaths) AS total_deaths 
FROM 	`covid19_data.covid19-data` 
WHERE 	location NOT LIKE '%income%' AND 
		location NOT LIKE '%World%' AND 
        (total_cases IS NOT NULL OR total_deaths IS NOT NULL) 
GROUP BY location 
ORDER BY total_cases DESC;