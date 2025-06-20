# Project 1: Descriptive Analysis

## Project Description
This project builds an AWS-based **Data Analytics Platform (DAP)** to evaluate the City of Vancouver’s **2025 Multi-Year Capital Project Budget**. The platform processes and analyzes how public funds are distributed and utilized across service categories like Housing, Childcare, Public Safety, Parks, and more.

By implementing a complete data pipeline using AWS S3, Glue DataBrew, Glue Studio, and Athena, this project enables a systematic approach for government stakeholders to monitor fiscal performance, ensure transparency, and make data-driven decisions.

---

## Project Title
**AWS Data Analytics Platform for the City of Vancouver Capital Budget Analysis**

---

## Objective
- Assess how budgeted funds for 2025 are allocated and spent across municipal service categories.
- Identify disparities between planned vs. actual expenditures.
- Support evidence-based financial decisions for city planning and resource optimization.
- Build a reusable, low-cost cloud-native data analytics pipeline for government data.

---

## Dataset
**Dataset Name**: 2025 Multi-Year Capital Project Budget  
**Source**: [City of Vancouver Open Data Portal](https://opendata.vancouver.ca/explore/dataset/2025-multi-year-capital-project-budget-requests-and-capital-expenditure-budget/analyze/?disjunctive.service_category_1&disjunctive.service_category_2&disjunctive.service_category_3&disjunctive.project_program_name&refine.service_category_1=Childcare&refine.service_category_1=Civic+facilities+%26+equipment&refine.service_category_1=Community+facilities&refine.service_category_1=Emerging+priorities,+contingency+%26+project+delivery&refine.service_category_1=Housing&refine.service_category_1=One+Water:+Potable+water,+rainwater+%26+sanitary+Water*&refine.service_category_1=Parks+%26+public+open+spaces&refine.service_category_1=Public+safety&dataChart=eyJxdWVyaWVzIjpbeyJjaGFydHMiOlt7InR5cGUiOiJsaW5lIiwiZnVuYyI6IkFWRyIsInlBeGlzIjoiYXZhaWxhYmxlX3Byb2plY3RfYnVkZ2V0X2luXzIwMjUiLCJzY2llbnRpZmljRGlzcGxheSI6dHJ1ZSwiY29sb3IiOiIjMDI3OUIxIn0seyJhbGlnbk1vbnRoIjp0cnVlLCJ0eXBlIjoibGluZSIsImZ1bmMiOiJBVkciLCJ5QXhpcyI6ImFubnVhbF9jYXBpdGFsX2V4cGVuZGl0dXJlXzIwMjVfY2FwaXRhbF9leHBlbmRpdHVyZV9idWRnZXQiLCJzY2llbnRpZmljRGlzcGxheSI6dHJ1ZSwiY29sb3IiOiIjNjFhNjQ0In1dLCJ4QXhpcyI6InNlcnZpY2VfY2F0ZWdvcnlfMSIsIm1heHBvaW50cyI6bnVsbCwic29ydCI6IiIsImNvbmZpZyI6eyJkYXRhc2V0IjoiMjAyNS1tdWx0aS15ZWFyLWNhcGl0YWwtcHJvamVjdC1idWRnZXQtcmVxdWVzdHMtYW5kLWNhcGl0YWwtZXhwZW5kaXR1cmUtYnVkZ2V0Iiwib3B0aW9ucyI6eyJkaXNqdW5jdGl2ZS5zZXJ2aWNlX2NhdGVnb3J5XzEiOnRydWUsImRpc2p1bmN0aXZlLnNlcnZpY2VfY2F0ZWdvcnlfMiI6dHJ1ZSwiZGlzanVuY3RpdmUuc2VydmljZV9jYXRlZ29yeV8zIjp0cnVlLCJkaXNqdW5jdGl2ZS5wcm9qZWN0X3Byb2dyYW1fbmFtZSI6dHJ1ZSwicmVmaW5lLnNlcnZpY2VfY2F0ZWdvcnlfMSI6WyJDaGlsZGNhcmUiLCJDaXZpYyBmYWNpbGl0aWVzICYgZXF1aXBtZW50IiwiQ29tbXVuaXR5IGZhY2lsaXRpZXMiLCJFbWVyZ2luZyBwcmlvcml0aWVzLCBjb250aW5nZW5jeSAmIHByb2plY3QgZGVsaXZlcnkiLCJIb3VzaW5nIiwiT25lIFdhdGVyOiBQb3RhYmxlIHdhdGVyLCByYWlud2F0ZXIgJiBzYW5pdGFyeSBXYXRlcioiLCJQYXJrcyAmIHB1YmxpYyBvcGVuIHNwYWNlcyIsIlB1YmxpYyBzYWZldHkiXX19fV0sInRpbWVzY2FsZSI6IiIsImRpc3BsYXlMZWdlbmQiOnRydWUsImFsaWduTW9udGgiOnRydWV9)  
**Contents**:
- 479 rows × 20 columns
- Covers categories: Childcare, Housing, Civic Facilities, Public Safety, etc.
- Includes fields like `Available Project Budget`, `Capital Expenditure`, `Service Category`

### Why this dataset?
- Clearly structured and aligned with budgeting frameworks.
- Offers both allocated and spent amounts for accurate analysis.
- Relevant to urban planning, resource allocation, and municipal governance.

---

## Methodology

This project follows a structured, cloud-native data analytics workflow leveraging AWS services. The methodology was designed to ensure data quality, traceability, scalability, and cost efficiency across all stages—from data ingestion to final financial insights.

### Step 1: Data Ingestion
The analytical process began by sourcing the *2025 Multi-Year Capital Project Budget* dataset from the City of Vancouver Open Data Portal. This structured data was uploaded to an Amazon S3 bucket (`finance-raw-kartik`), which served as the **raw data zone**. The dataset was stored in CSV format under `service category/2025_budgets.csv`, forming the foundation for all subsequent data processing activities.

### Step 2: Data Profiling
Using **AWS Glue DataBrew**, an interactive data profiling project was configured to assess the quality and structure of the raw data. This step identified:
- Missing values and nulls
- Duplicate records
- Inconsistent text casing
- Mismatched data types

Profiling metrics and visual summaries were generated for all 20 columns. Cleaned outputs were stored in a separate S3 bucket (`finance-cln-kartik`) in two subfolders:
- `user/` for human-readable CSV files
- `system/` for Parquet files optimized for querying

This stage enabled a comprehensive understanding of data readiness before applying transformations.

### Step 3: Data Cleaning
A cleaning recipe was created in **AWS Glue DataBrew** to standardize the dataset:
- Filled missing forecast values with default values (e.g., `0.00`)
- Applied sentence casing to textual fields for consistency
- Ensured uniform formatting across budget fields

This process was visualized using DataBrew's lineage tracking interface, offering full traceability from raw ingestion to cleaned output. The cleaned dataset (479 rows × 20 columns) was written back to Amazon S3 in both CSV and partitioned Parquet formats.

### Step 4: Data Cataloging
To support structured analytics, a **Glue Crawler** (`finance-crawler-kartik`) was created to automatically extract metadata and populate the **AWS Glue Data Catalog**. The crawler detected schema, partitions, and file format, and generated corresponding tables in the catalog under the database `finance-datacatalog-kartik`. This enabled **Amazon Athena** to query the datasets directly without manual schema definition.

### Step 5: Data Summarization (ETL)
A visual **ETL job** was developed in **AWS Glue Studio** (`finance-dataenriching-kartik`) to transform and summarize the cleaned data. The job:
- Connected to the curated table in Glue Data Catalog
- Performed group-by operations on `Service Category`
- Calculated average project budgets and capital expenditures

The output was stored in Parquet format in the curated S3 bucket (`finance-2025budget-cur-kartik/final_output/`), partitioned by year, month, and service category. This enhanced performance for downstream querying and reporting.

### Step 6: Querying and Analysis
Using **Amazon Athena**, SQL queries were executed on the curated dataset to analyze:
- The average available budget per service category
- The average capital expenditure in 2025

---

## Tools and Technologies

| Tool / Service             | Purpose                                                                 |
|----------------------------|-------------------------------------------------------------------------|
| **Amazon S3**              | Stores raw, cleaned, and curated datasets                              |
| **AWS Glue DataBrew**      | Profiling and cleaning the dataset visually                            |
| **AWS Glue Studio**        | Visual ETL development for transforming and summarizing data           |
| **AWS Glue Crawler**       | Automatically generates schema and populates Glue Data Catalog         |
| **AWS Glue Data Catalog**  | Stores metadata used by Athena                                          |
| **Amazon Athena**          | Serverless SQL querying engine to analyze datasets in S3               |
| **Draw.io**                | Used to design architecture and data pipeline diagrams                 |
| **AWS Pricing Calculator** | Estimated monthly cost of the entire platform (approx. $1.77/month)    |

---

## Deliverables

- Raw and cleaned datasets stored in **Amazon S3**
- Profiling and cleaning jobs implemented in **AWS Glue DataBrew**
- Metadata and schema definitions generated via **Glue Crawlers**
- Summarized and partitioned datasets in **Parquet format**
- SQL queries in **Amazon Athena** for financial insights
- Visualizations: **Budget vs. expenditure per service category**
- AWS architecture diagrams (**ETL flow**, **storage zones**, **cataloging structure**)
- Cost estimate report showing **efficient use of AWS services**
- Reusable pipeline for future **municipal or corporate data analytics**

---

## Sample Insights

- **Housing** and **Public Safety** had the highest capital expenditures.
- **Parks & Public Open Spaces** were significantly underutilized based on budget vs. actual usage.
- **Childcare** and **Community Facilities** had moderate allocations but lower actual spending, suggesting either underperformance or operational constraints.
