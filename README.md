# COVID-19 Global Vaccinations Dashboard

## 🎯 **Project Goal**

- 📊 Utilize **SQL** to query a dataset and extract insights into the **COVID-19 pandemic** on a global scale.
- 🌐 Create a **Tableau Dashboard** to visualize key metrics found within the dataset, offering a comprehensive view of the pandemic's impact worldwide.

## 📈 **Dataset Information**

**Datasource:** [Our World in Data](https://ourworldindata.org/coronavirus) - A rich resource providing global data on COVID-19.

*📅 Date range used: 1/1/2020 to 3/30/2023, covering the extensive period of the pandemic.

## 🔍 **SQL Data Exploration of COVID-19 Data**

Diving deep into the data with SQL queries to uncover trends and patterns in the spread and impact of the virus.

### 🌍 1. Aggregating Cases and Deaths by Country/Region

~~~~sql
SELECT 	location, 
		MAX(total_cases) AS total_cases, 
        MAX(total_deaths) AS total_deaths 
FROM `covid19_data.covid19-data` 
WHERE 	location NOT LIKE '%income%' AND 
		location NOT LIKE '%World%' AND 
        (total_cases IS NOT NULL OR total_deaths IS NOT NULL) 
GROUP BY location 
ORDER BY total_cases DESC;
~~~~

**Result Snapshot:**

- Location: 🇺🇸 **United States**, Total Cases: **102,697,566**, Total Deaths: **1,117,054**
- Location: 🇯🇵 **Japan**, Total Cases: **33,421,785**, Total Deaths: **73,747**
- Location: 🇬🇧 **United Kingdom**, Total Cases: **24,286,411**, Total Deaths: **210,396**

### 2. Daily Trend Analysis

~~~~sql
SELECT 	date, 
		SUM(new_cases) AS daily_cases, 
    	SUM(new_deaths) AS daily_deaths 
FROM `covid19_data.covid19-data` 
GROUP BY date  
HAVING daily_cases > 0 OR daily_deaths > 0 
ORDER BY date;
~~~~

**Result Snapshot:**

- Date: **Wed Feb 12 2020**, Daily Cases: **60,641**, Daily Deaths: **1,012**
- Date: **Fri Feb 12 2021**, Daily Cases: **1,715,564**, Daily Deaths: **52,646**
- Date: **Sat Feb 12 2022**, Daily Cases: **8,326,531**, Daily Deaths: **43,797**
- Date: **Sun Feb 12 2023**, Daily Cases: **471,139**, Daily Deaths: **3,162**

### 3. Yearly Trend Analysis

~~~~sql
SELECT 	EXTRACT(YEAR FROM date) AS year, 
		SUM(new_cases) AS yearly_cases, 
        SUM(new_deaths) AS yearly_deaths 
FROM `covid19_data.covid19-data` 
WHERE continent IS NOT NULL 
GROUP BY year 
ORDER BY year;
~~~~

**Result Snapshot:**

- Year: **2020**, Yearly Cases: **82,946,139**, Yearly Deaths: **1,928,665**
- Year: **2021**, Yearly Cases: **204,181,293**, Yearly Deaths: **3,522,324**

### 4. Total Vaccinations by Location

~~~~sql
SELECT 	location, 
		MAX(total_vaccinations) AS total_vaccinations 
FROM `covid19_data.covid19-data` 
WHERE 	location NOT LIKE '%income%' AND 
		location NOT LIKE '%World%' 
GROUP BY location 
HAVING total_vaccinations > 0 
ORDER BY total_vaccinations DESC;
~~~~

**Results Snapshot**

- Location: 🇨🇳 **China**, Total Vaccinations: **3,491,077,000**
- Location: 🇺🇸 **United States**, Total Vaccinations: **673,465,377**
- Location: 🇨🇦 **Canada**, Total Vaccinations: **96,956,502**
