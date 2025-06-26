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
### profiles.yml:
Configures dbt connection to BigQuery via service account with specified project and dataset.
set trips_data_all as default dataset

### dbt_project.yml:
dbt project configuration including model paths(where the models are saved), materializations(how to build models like view, table etc.), and dataset targets(dataset or schema in the warehouse).


### Seeds
Contains static CSV files to be loaded directly into the data warehouse as reference tables.
For example, taxi_zone_lookup.csv is stored here and loaded as a seed table. This seed provides geographic zone metadata used to enrich fact tables and dimension models.

### Models:
**staging models**:

Handle raw data cleaning

Standardize column types

Remove duplicate entries using row_number() over (...)

Generate surrogate keys

**Core models**:
  
Join and unify taxi trip records from multiple sources.

Enrich data with geographic zone details.

Provide aggregated insights such as fare trends and trip volumes.

**Dimension Tables**

Contain cleaned metadata (e.g., pickup/dropoff zones).

Used to join contextual information into fact models.

### Use of Macro

This project leverages custom dbt macros to simplify and standardize repetitive logic across models. For example, the macro get_payment_type_description converts payment type codes into meaningful labels, improving readability and maintainability of SQL.

## Steps to Build the Pipeline
### Step 1: Configure dbt Project and Profiles
Define your dbt_project.yml to set model paths, materializations (e.g., table, view), and dataset targets.

Set up your profiles.yml to configure connection to BigQuery using your GCP service account and specify the default dataset (trips_data_all).

### Step 2: Load Seed Data into BigQuery
Place static lookup CSV files (e.g., taxi_zone_lookup.csv) in the seeds/ folder.

Run dbt seed to upload these files as tables in BigQuery.

These seed tables are used to enrich trip data with geographic zone information.

### Step 3: Develop Staging Models for Raw Data Cleaning
Write SQL models in the staging/ folder that:

Clean raw Green and Yellow taxi data.

Deduplicate rows using window functions.

Cast columns to correct data types.

Generate surrogate keys for unique identifiers.

### Step 4: Create Core Models to Build Fact and Dimension Tables
Build core models in the core/ folder to:

Union cleaned Green and Yellow taxi data into a unified fact table.

Join with dimensional tables such as zones.

Calculate analytical aggregates like fare percentiles.

### Step 5: Define and Use Custom Macros
Develop macros (e.g., get_payment_type_description) in the macros/ folder for reusable SQL logic.

Use these macros in models to improve maintainability and clarity.

### Step 6: Run and Test the Pipeline
Execute dbt build --vars '{is_test_run: false}' to compile, run, and test all models.

Use dbt run --select <model_name> to run individual models as needed.

Validate outputs by querying the resulting tables in BigQuery or connected BI tools.


## Technologies Used
dbt (Data Build Tool) — for version-controlled ELT workflows

Google BigQuery — data warehouse and execution engine

SQL / Jinja — for transformation logic and macros

Service Account Key — secure authentication to BigQuery

Modular Environment Setup — separate datasets for staging and analytics



## skills demonstrated 
Demonstrates practical knowledge of dbt and BigQuery for real-world ELT pipelines.

Illustrates ability to work with multiple data sources, union and join complex datasets.

Applies best practices in data modeling, materialization strategies, and environment separation.

Builds foundation for downstream analytics and dashboarding use cases.


