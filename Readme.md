# COVID-19 Data Exploration (SQL Server)

Exploratory SQL analysis of global COVID-19 case, death, and vaccination data using T-SQL on Microsoft SQL Server.

## Overview

This project explores the relationship between COVID-19 cases, deaths, population, and vaccination rollout across countries and continents, using joins, window functions, CTEs, views, and aggregate queries.

## Dataset

Two source tables:
- **CovidDeath** — location, date, total/new cases, total/new deaths, population
- **CovidVaccinations** — location, date, new vaccinations

## Tools

- Microsoft SQL Server / T-SQL

## Analysis Covered

- **Data cleaning**: correcting column data types (`total_cases`, `total_deaths` to `INT`)
- **Cases vs. deaths**: death percentage by country, with correct handling of integer division (casting numerator to `DECIMAL` to avoid truncation)
- **Infection rate**: percentage of population infected, by country
- **Highest infection count/rate**: ranking countries by peak infection count and rate relative to population
- **Highest death count/rate**: ranking countries by death count and rate relative to population
- **Continental breakdown**: aggregating death counts and rates by continent
- **Global totals**: filtering to continent-level rows (`continent IS NULL`) for worldwide summaries
- **Vaccination rollout**: joining deaths and vaccinations tables, and calculating a rolling cumulative sum of vaccinations per location using `SUM() OVER (PARTITION BY ... ORDER BY ...)`
- **CTE**: `PopvsVac` common table expression to calculate vaccination percentage of population
- **Temp table**: `POPVSVAC` physical table storing the same rolling vaccination calculation
- **View**: `popvaccview` created for reuse in visualization tools (e.g. Power BI, Tableau)

## Key SQL Techniques Demonstrated

- Window functions (`SUM() OVER (PARTITION BY ... ORDER BY ...)`)
- Common Table Expressions (CTEs)
- Views and temporary/physical staging tables
- Type casting and data type correction (`ALTER TABLE ... ALTER COLUMN`)
- Aggregate functions (`MAX`, `SUM`) with `GROUP BY`
- Joins across related tables

## Files

- `covid_exploration.sql` — full query script, in the order the analysis was performed

## Notes

Queries include inline comments explaining reasoning at each step, including a fix for a common SQL Server pitfall: integer division truncating decimal results (resolved by casting to `DECIMAL`/`FLOAT` before dividing).
