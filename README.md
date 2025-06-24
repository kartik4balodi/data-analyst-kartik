# Project 1: Descriptive Analysis

## Project Description
This project builds an AWS-based **Data Analytics Platform (DAP)** to evaluate the City of Vancouver’s **2025 Multi-Year Capital Project Budget**. The platform processes and analyzes how public funds are distributed and utilized across service categories like Housing, Childcare, Public Safety, Parks, and more.

By implementing a complete data pipeline using AWS S3, Glue DataBrew, Glue Studio, and Athena, this project enables a systematic approach for government stakeholders to monitor fiscal performance, ensure transparency, and make data-driven decisions.

![Pipeline Flow](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Descriptive%20Analysis.png)
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

![Pipeline Flow](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/DAP.png)

---

## Methodology

This project follows a structured, cloud-native data analytics workflow leveraging AWS services. The methodology was designed to ensure data quality, traceability, scalability, and cost efficiency across all stages—from data ingestion to final financial insights.

### Step 1: Data Ingestion
The analytical process began by sourcing the *2025 Multi-Year Capital Project Budget* dataset from the City of Vancouver Open Data Portal. This structured data was uploaded to an Amazon S3 bucket (`finance-raw-kartik`), which served as the **raw data zone**. The dataset was stored in CSV format under `service category/2025_budgets.csv`, forming the foundation for all subsequent data processing activities.

![Pipeline Flow](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/AWS%20S3%20Raw.png)

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

![Pipeline Flow](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/AWS%20Profiling.png)
![Pipeline Flow](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/Profiling%20Prj.png)
![Pipeline Flow](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/Profiling%20Job.png)

### Step 3: Data Cleaning
A cleaning recipe was created in **AWS Glue DataBrew** to standardize the dataset:
- Filled missing forecast values with default values (e.g., `0.00`)
- Applied sentence casing to textual fields for consistency
- Ensured uniform formatting across budget fields

This process was visualized using DataBrew's lineage tracking interface, offering full traceability from raw ingestion to cleaned output. The cleaned dataset (479 rows × 20 columns) was written back to Amazon S3 in both CSV and partitioned Parquet formats.

![Pipeline Flow](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/Data%20Lineage.png)
![Pipeline Flow](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/Recipe.png)
![Pipeline Flow](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/Cleaning.png)

### Step 4: Data Cataloging
To support structured analytics, a **Glue Crawler** (`finance-crawler-kartik`) was created to automatically extract metadata and populate the **AWS Glue Data Catalog**. The crawler detected schema, partitions, and file format, and generated corresponding tables in the catalog under the database `finance-datacatalog-kartik`. This enabled **Amazon Athena** to query the datasets directly without manual schema definition.

![Pipeline Flow](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/Crawler.png)
![Pipeline Flow](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/Datacatalog.png)

### Step 5: Data Summarization (ETL)
A visual **ETL job** was developed in **AWS Glue Studio** (`finance-dataenriching-kartik`) to transform and summarize the cleaned data. The job:
- Connected to the curated table in Glue Data Catalog
- Performed group-by operations on `Service Category`
- Calculated average project budgets and capital expenditures

The output was stored in Parquet format in the curated S3 bucket (`finance-2025budget-cur-kartik/final_output/`), partitioned by year, month, and service category. This enhanced performance for downstream querying and reporting.

![Pipeline Flow](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/ETL.png)
![Pipeline Flow](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/Summarization.png)

### Step 6: Querying and Analysis
Using **Amazon Athena**, SQL queries were executed on the curated dataset to analyze:
- The average available budget per service category
- The average capital expenditure in 2025

![Pipeline Flow](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/Query.png)
![Pipeline Flow](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/Data%20enriching.png)

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

## Insights

- **Housing** and **Public Safety** had the highest capital expenditures.
- **Parks & Public Open Spaces** were significantly underutilized based on budget vs. actual usage.
- **Childcare** and **Community Facilities** had moderate allocations but lower actual spending, suggesting either underperformance or operational constraints.

---

# Project 2 - Data Security

## Descriptive Analysis

This project showcases the design and implementation of a secure and scalable Data Analytics Platform (DAP) using AWS services for the City of Vancouver’s 2025 financial data. The solution emphasizes cloud-native principles such as automation, observability, data traceability, and security.

It focuses on three critical capabilities:

- **Data Security** – Ensuring confidentiality, integrity, and durability through encryption, versioning, and replication.
- **Data Governance** – Creating an auditable and well-documented ETL workflow using AWS Glue Studio.
- **Data Monitoring** – Leveraging AWS CloudTrail and CloudWatch for comprehensive logging and real-time alerting.

---

## Project Description

The City of Vancouver DAP project implements a robust AWS-based data pipeline to process public sector budget data. This pipeline facilitates the collection, transformation, validation, and summarization of financial data while upholding compliance and governance standards. The solution integrates Amazon S3 for data storage, AWS Glue for ETL, KMS for encryption, and AWS observability tools for continuous monitoring.

---

## Project Title

**AWS Data Analytic Platform for The City of Vancouver**

---

## Objective

To develop a reliable, secure, and traceable cloud data platform that:

- Encrypts sensitive financial datasets
- Enables version control and disaster recovery
- Implements traceable ETL pipelines
- Supports continuous monitoring and system observability

---

## Dataset

The primary dataset used is the **City of Vancouver 2025 Capital Budget**, processed through three S3 buckets:

- `finance-raw-kartik` – raw ingested files
- `finance-cln-kartik` – cleaned and validated data
- `finance-2025budget-cur-kartik` – curated output for analysis

Each bucket reflects a logical step in the ETL life cycle: ingestion, transformation, and delivery.

---

## Methodology

The methodology is divided into three major implementation phases:

### Step 6: Data Security
To ensure the integrity, confidentiality, and availability of sensitive financial data stored in the AWS cloud, a multi-layered security strategy was implemented. The design of the Data Analytics Platform (DAP) includes robust encryption, versioning, and replication across all Amazon S3 buckets used in the ETL pipeline.

**1. AWS Key Management Service (KMS)And Encryption**  
We utilized AWS KMS to apply default encryption across all data buckets—finance-raw-kartik, finance-cln-kartik, and finance-2025budget-cur-kartik. Default encryption ensures that any object uploaded to the bucket is automatically encrypted using an AWS-managed key, without manual intervention. This minimizes the risk of human error while maintaining compliance with data protection standards.

Each bucket uses AWS KMS-managed keys for default encryption. All incoming data is automatically encrypted to ensure compliance with privacy and security standards.

![KMS Key Creation](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/figure1_kms_key.png)

Shows the custom KMS key created via the AWS console. This key is used to manage access policies and control encryption for S3 buckets.

![raw](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/figure2_encryption_s3raw.png)
![cln](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/figure3_encryption_s3cln.png)
![cur](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/figure4_encryption_s3cur.png)

Depict how each S3 bucket was configured to use the KMS key for default encryption. You can see in the AWS console under "Default Encryption" that the buckets are set to use SSE-KMS (Server-Side Encryption with KMS).

**2. S3 Versioning**  
Versioning was enabled on all three buckets. This allows every version of every object to be preserved. It is particularly crucial for collaborative environments where automated pipelines could overwrite files or introduce bugs.

Show how versioning is enabled via the "Properties" tab of each S3 bucket. This configuration ensures that users can recover earlier versions of files if needed.

![raw](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/figure5_versioning_s3raw.png)
![cln](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/figure6_versioning_s3cln.png)
![cur](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/figure7_versioning_s3cur.png)

**3. Replication Rules**  
To support disaster recovery, replication rules were applied to each bucket. These rules allow automatic replication of data objects to another S3 bucket (potentially in a different region), ensuring redundancy in case of regional failures or system crashes.
Data replication is enabled across buckets and potentially regions, enhancing disaster recovery capabilities.

Illustrate the replication settings on the S3 console. Each screenshot displays the "Replication Rule Configuration" with source and destination bucket mappings, ensuring business continuity.

![raw](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/figure8_replication_s3raw.png)
![cln](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/figure9_replication_s3cln.png)
![cur](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/figure10_replication_s3cur.png)

**Conclusion:** Through encryption, versioning, and replication, the DAP achieves a high level of resilience and compliance, addressing both operational risks and industry-specific regulatory needs.

---

### Step 7: Data Governance
The governance framework for this platform ensures data traceability, lineage, accountability, and quality control through AWS Glue Studio and associated services.

**1. Visual ETL with AWS Glue Studio**  
We used AWS Glue Studio’s visual drag-and-drop interface to design ETL workflows that move data from raw to clean to curated formats. This interface allows for an intuitive setup of transformations, making it accessible even to stakeholders with limited technical backgrounds.
The workflow includes logic to validate incoming records. Records that pass the quality checks are routed to the "Pass" S3 folder, while records that fail are routed to the "Failed" folder. This automated bifurcation aids in maintaining clean datasets and helps analysts quickly investigate data anomalies.

![glue](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/figure11_etl_gluestudio.png)

Displays the Glue Studio canvas where the transformation logic is defined. You can observe the flow of components such as data sources, transformation nodes (like filter and map), and destinations.

**2. Metadata and Versioning**  
Each ETL job was named methodically based on its role and position in the pipeline. AWS Glue automatically supports job versioning, allowing users to track historical changes, roll back to earlier configurations, and maintain reproducibility. Metadata tagging further enhances discoverability and classification of jobs and datasets in the AWS Glue Data Catalog.

**3. Execution Audit**  
After developing the ETL pipeline, it was executed for testing. During this process, a job failure occurred not due to an error, but because all records passed the validation and there were no entries that matched the "Failed" logic branch.

![etl job run](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/figure12_etl_jobrun.png)

Captures the job run status in Glue Studio. The log clearly shows the success/failure status and highlights the practical scenario of a failed branch not receiving any data—confirming that the pipeline was correctly structured and logically validated.

**Conclusion:** Governance mechanisms such as lineage tracking, quality validation, and ETL job auditing enable the platform to maintain reliable, reproducible, and accountable data operations—key pillars in any enterprise-grade analytics environment.

---

### Step 8: Data Monitoring
Monitoring was implemented using two complementary AWS services: CloudTrail for user and API activity logging, and CloudWatch for real-time system monitoring and alerting.

**1. AWS CloudTrail**  
CloudTrail records all user activities and API calls within the AWS environment. For this project, it tracks actions such as:

- Access to S3 buckets
- Execution of Glue jobs
- IAM role or policy changes

This provides a full audit trail to detect unauthorized access or abnormal behavior.

![cloud trail](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/figure13_cloudtrail.png)

Shows a CloudTrail event history filtered by service (e.g., S3 or Glue), clearly listing the user, timestamp, and action performed. This enables the team to answer “who did what and when” with precision.

**2. Amazon CloudWatch**  
Monitors ETL job metrics such as duration, status, and failure. Dashboards and alarms are set to alert administrators of anomalies or delays.

![cloud watch](https://github.com/kartik4balodi/data-analyst-kartik/blob/main/Images/figure14_cloudwatch.png)

Displays a CloudWatch dashboard showing metrics such as job success rate, duration, and failure count. Alarm thresholds are also visible, configured to send notifications when thresholds are crossed.

**3. Glue Job Integration with CloudWatch**  
Glue jobs are directly integrated with CloudWatch for real-time logging of job performance and error tracking, supporting root-cause analysis and operational diagnostics.

**Conclusion:** The combination of CloudTrail and CloudWatch enables both proactive monitoring and retrospective auditing, creating a comprehensive observability framework that enhances security, performance, and accountability across the platform.

---

## Tools and Technologies

| Tool / Service           | Purpose                                                                 |
|--------------------------|-------------------------------------------------------------------------|
| Amazon S3                | Stores raw, cleaned, and curated datasets                               |
| AWS Key Management Service (KMS) | Encrypts data at rest                                            |
| AWS Glue Studio          | Visual interface for ETL transformation                                 |
| AWS Glue Data Catalog    | Manages schema and metadata                                              |
| AWS CloudTrail           | Tracks all AWS account activities                                       |
| Amazon CloudWatch        | Monitors system health and job performance                              |

---

## Deliverables

- Secure and encrypted storage in Amazon S3
- Bucket versioning and cross-region replication rules
- Transparent ETL workflows with AWS Glue Studio
- Quality control logic routing valid/invalid records
- Full audit logs using AWS CloudTrail
- CloudWatch dashboards, logs, and alarms
- Visual documentation and screenshots of implementation

---

# Project 3 - AWS Cloud Foundations Portfolio

# AWS Cloud Foundations Portfolio
This portfolio presents a comprehensive reflection on foundational AWS concepts through 12 case studies, each linked to practical labs and real-world application. The project highlights the understanding and application of AWS services including cloud deployment, cost analysis, identity management, virtual networking, serverless computing, and storage—all within an academic context.  

The following sections are organized thematically by core AWS service areas, with each case study offering a detailed analysis, real lab activities, and the key takeaways learned throughout the journey.

---

## AWS Deployment and Service Models

### Case Study 1: Traditional vs. Cloud Computing  
This case compares traditional on-premises computing with cloud computing. Traditional models require upfront investment in physical servers, cooling infrastructure, and IT staff. These environments lack scalability and require manual provisioning, which increases operational burden.

In contrast, AWS enables on-demand resource provisioning, scalability based on actual usage, and access to global services without maintaining physical hardware.

<img width="653" alt="image" src="https://github.com/user-attachments/assets/68aee31d-70de-4cf7-97f5-40bfc81cd1c3" />
<img width="516" alt="image" src="https://github.com/user-attachments/assets/79f9500f-dbae-4074-810c-35ecad7fd2f7" />

**Key Learning**: Cloud adoption transforms IT from a capital-intensive to an operational model, improving agility, reducing hardware dependency, and enhancing innovation.

---

### Case Study 2: Cloud Deployment Models  
This study explores the characteristics and use cases of public, private, hybrid, and multi-cloud deployments. Public cloud (like AWS) offers shared resources and scalability, while private clouds offer enhanced control and are suited for sensitive academic or research data. Hybrid models combine both, often used by universities needing flexibility with legacy systems.

<img width="1155" alt="image" src="https://github.com/user-attachments/assets/aab434c8-f37e-4d6c-8c1e-b726e977c59c" />
<img width="769" alt="image" src="https://github.com/user-attachments/assets/537d4dc3-2329-4a76-a68a-62756e6d85d7" />

**Key Learning**: The right deployment model depends on data sensitivity, compliance, performance needs, and budget. Hybrid and multi-cloud models offer flexibility for academic environments integrating modern and legacy systems.

---

### Case Study 3: Cloud Service Models  
There are three layers of cloud services:
- **IaaS**: Offers raw computing infrastructure (e.g., EC2, S3).
- **PaaS**: Provides pre-configured environments for development (e.g., Elastic Beanstalk).
- **SaaS**: Fully managed software solutions (e.g., Amazon WorkDocs).

This case emphasized how responsibility shifts between the cloud provider and the user. For example, in IaaS, users must manage OS patches, whereas in SaaS, AWS handles everything.

<img width="1363" alt="image" src="https://github.com/user-attachments/assets/b7691085-8f06-4158-92ef-a53a1543e534" />
<img width="604" alt="image" src="https://github.com/user-attachments/assets/04b43136-a8fb-407f-84ea-1aa086245d13" />

**Key Learning**: Service model selection should reflect the organization’s technical maturity and need for control. In academic labs, PaaS and SaaS reduce setup complexity for students and researchers.

<img width="639" alt="image" src="https://github.com/user-attachments/assets/243d41cc-b1a4-4504-8dd0-9e130a7ec219" />

---

## AWS Cost Analysis

### Case Study 4: Total Cost of Ownership (TCO)  
Using AWS’s TCO calculator, this case calculated the long-term financial benefits of using AWS instead of maintaining on-premises hardware. Elements such as hardware depreciation, electricity, IT salaries, and hardware refresh cycles were considered.

<img width="639" alt="image" src="https://github.com/user-attachments/assets/70956acd-b71d-4e75-970c-19e2eccff87c" />

**Key Learning**: Cloud services offer significant cost savings in the long term and reduce overhead, particularly beneficial for budget-constrained institutions like schools or universities.

---

### Case Study 5: AWS Pricing Calculator  
Simulated the monthly cost of AWS resources like EC2, S3, and EBS based on workload demands. Included scenarios for research projects with variable data needs and for hosting academic web applications.

<img width="1438" alt="image" src="https://github.com/user-attachments/assets/f453f203-264f-48b0-9f3a-279f7377c564" />

**Key Learning**: AWS Pricing Calculator is a crucial tool for forecasting costs and aligning infrastructure needs with financial planning. Understanding on-demand vs. reserved pricing models allows institutions to optimize expenses.

---

### Case Study 6: AWS Support Plans  
Compared four support plans—Basic, Developer, Business, and Enterprise—based on service level agreements (SLAs), response times, and access to technical support.

<img width="961" alt="image" src="https://github.com/user-attachments/assets/70a098a6-702c-44a2-a975-fa627f61a1aa" />

**Key Learning**: Choosing the right support tier helps ensure uptime and service quality.

<img width="610" alt="image" src="https://github.com/user-attachments/assets/75ca779f-2ba8-4cc7-a24f-6f5e3f6300b9" />

---

## AWS Global Infrastructure

### Case Study 7: AWS Regions, AZs, and Edge Locations  
Explored how AWS distributes resources across Regions, Availability Zones (AZs), and Edge Locations. Visualized how AWS ensures high availability and data redundancy by replicating services across AZs.

<img width="923" alt="image" src="https://github.com/user-attachments/assets/71264c04-8dab-41b4-8efa-f818712db6c0" />
<img width="664" alt="image" src="https://github.com/user-attachments/assets/2dc30a97-6c21-4eb5-9874-6cd445bb0bf0" />

**Key Learning**: Strategic region and AZ selection enables compliance with local regulations, improves app performance, and supports disaster recovery strategies for academic services.

<img width="664" alt="image" src="https://github.com/user-attachments/assets/979e1bbf-7985-40fb-b835-47ebf84c9768" />

---

## AWS IAM

### Case Study 8: Shared Responsibility Model  
Analyzed the division of responsibilities between AWS and the customer. AWS secures the underlying infrastructure, while customers manage their data, users, and application-level security.

<img width="530" alt="image" src="https://github.com/user-attachments/assets/740c69a7-ae18-4398-ad50-72c48e6a3a37" />
<img width="545" alt="image" src="https://github.com/user-attachments/assets/64894e32-bfb9-4c89-8432-b4aedf0f7901" />

**Key Learning**: For universities, understanding this model is essential to ensure data privacy, particularly in handling student records, research data, and administrative systems.

---

### Case Study 9: IAM Lab – Creating Users and Policies  
Hands-on activity involving IAM user, group, and role creation. Applied permissions using JSON-based policies and configured MFA for users accessing academic resources.

<img width="661" alt="image" src="https://github.com/user-attachments/assets/bac2e69d-e919-4bf9-8627-a07f3194be06" />

**Key Learning**: IAM ensures secure and role-based access, enabling fine-grained control in academic IT environments, especially when managing multiple departments and student labs.

<img width="661" alt="image" src="https://github.com/user-attachments/assets/3b0042b7-41a6-4a12-abd7-cecd628419e6" />

---

## AWS VPC

### Case Study 10: Build a Custom VPC  
Configured a VPC with public and private subnets, NAT gateways, route tables, and security groups. Deployed a web server in a public subnet and tested internet access while securing backend resources.

<img width="506" alt="image" src="https://github.com/user-attachments/assets/4c4c2b1f-9cf1-429c-8ade-554dfa6e8213" />

**Key Learning**: VPC allows universities to create isolated networks in the cloud, replicating on-prem data center security for research labs, administrative tools, and student portals.

<img width="506" alt="image" src="https://github.com/user-attachments/assets/4c782f28-18c9-4ea4-b5da-91fe2c860b9c" />

---

## AWS Lambda

### Case Study 11: Deploy a Serverless Function  
Created a Lambda function triggered by an S3 event and logged results to CloudWatch. Used Python code to process uploaded student files.

<img width="642" alt="image" src="https://github.com/user-attachments/assets/248fd59f-e0b0-47dd-9d1b-d42437703c8e" />

**Key Learning**: Lambda supports automated workflows (e.g., grading, notifications) without provisioning servers, ideal for academic automation and event-driven processing.

<img width="624" alt="image" src="https://github.com/user-attachments/assets/33f94368-46e0-4ea2-bfeb-b0fc8448c800" />

---

## AWS EBS

### Case Study 12: Work with Amazon EBS  
Provisioned gp3 and io1 volumes, attached them to EC2 instances, formatted them, and created snapshots for backup. Compared throughput and IOPS between volume types.

<img width="822" alt="image" src="https://github.com/user-attachments/assets/d5adfaf3-d70c-49f2-ae2d-b7c0ee345646" />

**Key Learning**: EBS provides persistent, block-level storage with backup and recovery features critical for academic databases, research applications, and file systems.

<img width="700" alt="image" src="https://github.com/user-attachments/assets/f6458ae1-8f31-435c-9a6b-7299c7816338" />

---
## Conclusion

This AWS Cloud Foundations portfolio serves as both a reflective academic project and a practical demonstration of cloud competency. Through twelve detailed case studies, it provides insight into key cloud computing principles including infrastructure design, cost optimization, secure access control, network segmentation, serverless automation, and scalable storage solutions.

Each case study connects theoretical understanding with hands-on application, enabling the translation of abstract cloud concepts into real-world scenarios. From deploying virtual private clouds to automating workflows with Lambda, this portfolio reflects an evolving capability to navigate and implement modern cloud architecture using AWS tools.
