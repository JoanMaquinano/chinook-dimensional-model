# Chinook Dimensional Model
## Project Objective

To design and implement a scalable dimensional model that enables analysis of sales performance, revenue trends, customer behavior, track popularity, genre preferences, and time-based metrics.

## Tools Used

- Databricks SQL
- Unity Catalog
- GitHub
- Draw.io

## Data Pipeline

The project follows a Medallion Architecture approach:

- **Raw Layer (Bronze)** – stores the source Chinook CSV data with minimal transformations and serves as the system of record.
- **Clean Layer (Silver)** – applies data cleansing, standardization, data type corrections, and data quality validations.
- **Mart Layer (Gold)** – contains curated fact and dimension tables optimized for analytics, reporting, and business insights.

## Dimensional Model
<!--
![Chinook Star Schema](link)
!-->

### Table Grains

- **fact_sales**
  - Grain: One row per invoice line (one purchased track on a specific invoice).
  - Measures: quantity, unit price, and line amount.

- **dim_customer**
  - Grain: One row per customer.

- **dim_track**
  - Grain: One row per track.

- **dim_employee**
  - Grain: One row per employee (sales support representative).

- **dim_date**
  - Grain: One row per calendar date.

## Repository Structure

<!--
```text
.
├── src/
│   ├── docs/
│   │   └── image/
│   │       └── chinook_star_schema.png
│   └── sql/
│       ├── 00_setup/
│       ├── 01_raw/
│       ├── 02_clean/
│       ├── 03_mart/
│       └── 04_analytics/
├── tests/
└── README.md
```

## How to Review the Project

1. Review `src/sql/00_setup/00_setup.sql` to create the required catalog and schemas.

2. Review the source inspection file in `src/sql/00_setup/01_source_inspection.py` to check the Chinook CSV source files.

3. Run the SQL scripts in `src/sql/01_raw/` to create the Raw layer tables.

4. Run the SQL scripts in `src/sql/02_clean/` to clean and standardize the source data.

5. Run the Mart scripts in this order:

   - `src/sql/03_mart/01_dim_customer.sql`
   - `src/sql/03_mart/02_dim_date.sql`
   - `src/sql/03_mart/03_dim_employee.sql`
   - `src/sql/03_mart/04_dim_track.sql`
   - `src/sql/03_mart/05_fact_sales.sql`

6. Review the validation queries in the `tests/` folder.

7. Review the business analysis queries in `src/sql/04_analytics/`.

## Data Quality

Data quality checks were included to validate:

- Missing primary keys
- Duplicate records
- Invalid numeric values
- Invalid foreign-key relationships
- Record-count reconciliation between layers

!-->

## Orchestration

The pipeline is orchestrated using Databricks Jobs to run the Raw, Clean, Mart, validation, and analytics scripts in sequence.
