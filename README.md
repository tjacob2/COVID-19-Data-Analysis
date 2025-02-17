# COVID-19-Data-Analysis


## Table of Contents

- [Project Overview](#project-overview)
- [Tools](#tools)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Methodology](#methodology)
  - [Data Collection](#1-data-collection)
  - [Data Cleaning](#2-data-cleaning)
  - [Data Exploration](#3-data-exploration)
  - [Visualization and Dashboard](#4-visualization-and-dashboard)
- [Results](#results)


### Project Overview

COVID-19 is a highly infectous respiratory illness caused by the novel coronavirus. The first occurance of the disease emerged from a laboratory in Wuhan, China, in December 2019 and has since rapidly spread worldwide. The symptoms of COVID-19 include fever, coughing, difficulty breathing, headaches, and fatigue. Therefore, it is best to socially distance,follow health guidlines, and most importantly taking care of ones self by drinking lots of fluids and plenty of rest.
This data analysis projects aims to provide insight into the COVID-19 deaths for each country from the time period,January 2020 to April 2021.
By analyzing the various aspects of the data, we are can identity the number of people infected during the given time perid to further understand the gravity and impact the pandemic had on the world.


### Tools

- Excel - Data Cleaning
- SQL Server - Data Analysis
- Tableau - Creating Dashboard/Report


 ### Exploratory Data Analysis
 
 A few questions needed to be answered in order to analyze the data:
 - What is the total number of confirmed cases and deaths in the world during the time period?
 - Which continent had the largest death count?
 - What is average population percentage on March 2021 and what the forecast throughout the year for the United States?


### Methodology

#### 1. Data Collection

Covid-19 Data: The primary dataset used for this analysis is "covid_deaths.xlsx", containing the number deaths and vaccinations for each country from 2020 to 2021


#### 2. Data Cleaning

In the inital stage, I performed the following tasks to reorgize the ncessary data needed for analysis:
1. Data loading and inspection
2. Handling missing values
3. Data cleaning and formatting


#### 3. Data Exploration

The dataset below was imported from the newly cleaned Excel file for data analysis
```sql
Select *
From PortfolioProject..CovidDeaths
Where continent is not null 
order by 3,4
```

The query below shows the number of cases, number of deaths, and the death percentaage from COVID-19 during the time period

```sql
Select location, SUM(cast(new_deaths as int)) as TotalDeathCount
From PortfolioProject..CovidDeaths
--Where location like '%states%'
Where continent is null 
and location not in ('World', 'European Union', 'International')
Group by location
order by TotalDeathCount desc
```


The query below is for the number of deaths for each continent

```sql
Select location, SUM(cast(new_deaths as int)) as TotalDeathCount
From PortfolioProject..CovidDeaths
--Where location like '%states%'
Where continent is null 
and location not in ('World', 'European Union', 'International')
Group by location
order by TotalDeathCount desc
```


The query below is for the number of deaths for each country

```sql
Select Location, Population, MAX(total_cases) as HighestInfectionCount,  Max((total_cases/population))*100 as PercentPopulationInfected
From PortfolioProject..CovidDeaths
--Where location like '%states%'
Group by Location, Population
order by PercentPopulationInfected desc
```


The query below is for the percent population infected for the countries of India, China, Mexico, United States, and the United Kingdom

```sql
Select Location, Population,date, MAX(total_cases) as HighestInfectionCount,  Max((total_cases/population))*100 as PercentPopulationInfected
From PortfolioProject..CovidDeaths
--Where location like '%states%'
Group by Location, Population, date
order by PercentPopulationInfected desc
```

#### 4. Visualization and Dashboard

The dashboard below shows the results from the above questions that are answered in the results section below

![Covid-19Dashboard](https://github.com/tjacob2/COVID-19-Data-Analysis/assets/165331511/223df23f-9748-4fe1-b73a-c45c9cb642c0)


### Results

 The analysis results are summarized as follows
 1. The total confirmed cases from 2020 to April 2021 was 150,574,977 and the number of deaths were 3,180,206 which was shows that 2.11% of people died from COVID-19.
 2. Europe had the largest number of deaths during the time period with 1,016,750 deaths during the time period.
 3. The percentage population infected on March 2021 was 8.93%, it is believed to increase throughout 2021 to 10-20%.


### Limitations

I had to add all the data sets that were blank or N/A for the accuracy of my data as well as being ableto use SQL. There were a few countries such as Turkmenistan and Western Sahara that didn't have any data given so they wer removed.


### References

  #### 1. Website for dataset: [Coronavirus (COVID-19) Deaths](https://ourworldindata.org/covid-deaths)
