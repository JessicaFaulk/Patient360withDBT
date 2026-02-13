# Patient 360 Analytics Project

## Overview

This project demonstrates building a **Patient 360 view** using the **Synthea dataset**, **dbt**, and **BigQuery**. It transforms raw patient, encounter, and condition data into a set of **dimension tables**, **fact tables**, and **seeded lookup tables**, enabling analysis of patient journeys, condition prevalence, and demographic patterns.

The goal is to showcase skills in:

- Data modeling and transformation with **dbt**
- Using **seeds**, **staging**, and **dimension tables**
- Incremental builds and surrogate key generation
- Writing **dbt tests** for data quality
- Performing exploratory analytics to visualize patient journeys

---

## Project Structure

patient_360_dbt_project/
  dbt_project.yml           # dbt project configuration
  profiles.yml              # dbt connection profile (not usually in repo)
  models/
    staging/                # staging tables (raw → cleaned)
      stg_patients.sql
      stg_encounters.sql
      stg_conditions.sql
    marts/                  # dimension and fact tables
      dimensions/
        dim_patient.sql
        dim_encounter.sql
        dim_condition.sql
      facts/
        fct_claims.sql
  seeds/                    # CSV lookup/reference tables
    gender_lookup.csv
    zipcode_zcta.csv
  snapshots/                # snapshots for slowly changing dimensions
  tests/                    # custom dbt tests
  macros/                   # custom dbt macros
  notebooks/                # exploratory analysis notebooks
  README.md                 # project documentation






---

## Data Sources

- **Synthea**: synthetic healthcare dataset including:
  - Patients
  - Encounters
  - Conditions
  - Claims
  - EOBs

- **Seed files**:
  - `gender_lookup.csv` maps gender codes to labels


## DBT Highlights

- **Dimension Tables**:
  - `dim_patient` with surrogate key
  -  <i> planned: </i>  `dim_encounter`, `dim_claim`, `dim_condition`, `dim_eob` (extendable)

- **Staging Tables**:
  - Cleaned tables ready for transformations, preserving raw data

- **Data Quality Tests**:
  - Not-null and unique constraints on key columns
  - Accepted value tests (e.g., gender codes)
  - Historical consistency tests to ensure patient_ids do not disappear

- **Seeds & Lookup Tables**:
  - CSV-based seeds loaded with `dbt seed`
  - Example: gender lookup, ZIP/ZCTA mapping






```bash
pip install dbt-bigquery pandas-gbq google-cloud-bigquery
