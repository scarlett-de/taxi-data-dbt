# NYC Taxi Analytics with dbt & BigQuery

This project demonstrates a full data engineering pipeline built using dbt (data build tool) and Google BigQuery. It processes and transforms NYC taxi trip data (Green and Yellow taxi datasets) into analytics-ready tables for downstream analysis.

## Project Overview
The goal of this project is to build an efficient, scalable, and modular ELT pipeline to clean, join, and enrich raw taxi trip data stored in BigQuery. Key highlights:

Use of dbt for modular, version-controlled data transformations

Integration with BigQuery as the data warehouse

Separation of environments and datasets (raw, staging, analytics)

Materialization strategies using views and tables for optimized querying

Joining taxi trip data with geographic zones dimension for enriched insights

Use of SQL and Jinja templating within dbt models

## Project Structure
**profiles.yml**: Configures dbt connection to BigQuery via service account with specified dataset and project.

**dbt_project.yml**: dbt project configuration including model paths, materializations, and dataset targets.

Models:

staging: Contains views for raw external tables (Green and Yellow taxi trips).

core: Contains materialized tables that combine, clean, and enrich data for analytics.

Sources: Defined for raw external datasets ext_green_taxi and ext_yellow_taxi.

Transformations: SQL models that:

Union Green and Yellow taxi trip data, adding service type labels.

Join trip data with dim_zones table for location context (borough, zone).


## Technologies Used
dbt (Data Build Tool) — for version-controlled ELT workflows

Google BigQuery — data warehouse and execution engine

SQL / Jinja — for transformation logic and macros

Service Account Key — secure authentication to BigQuery

Modular Environment Setup — separate datasets for staging and analytics

## Key dbt Configuration Details
Connection Profile (profiles.yml)

Connects to BigQuery project: dbt-project-451121

Default dataset: trips_data_all (raw data)

Authentication via service account key stored locally

Project (dbt_project.yml)

Models under namespaces:

staging materialized as views in dataset dbt_nytaxi_staging

core materialized as tables in dataset dbt_nytaxi_analytics

## skills demonstrated 
Demonstrates practical knowledge of dbt and BigQuery for real-world ELT pipelines.

Illustrates ability to work with multiple data sources, union and join complex datasets.

Applies best practices in data modeling, materialization strategies, and environment separation.

Builds foundation for downstream analytics and dashboarding use cases.



Make sure you’ve installed dbt and initialized your project:

```dbt init dbt_ny_taxi```
