🚀 Azure End-to-End Data Engineering Pipeline
<p align="center"> <img src="https://img.shields.io/badge/Azure-Data%20Engineering-blue?logo=microsoftazure&logoColor=white" height="30"/> <img src="https://img.shields.io/badge/Databricks-Lakehouse-red?logo=databricks&logoColor=white" height="30"/> <img src="https://img.shields.io/badge/ETL-Pipeline-green?logo=apache-spark&logoColor=white" height="30"/> </p>
📌 Project Overview

This project demonstrates the design and implementation of a real-world Azure Data Engineering pipeline.
It integrates Azure SQL Database, Azure Data Factory (ADF), Azure Data Lake, Databricks, Delta Lake, Unity Catalog, and Power BI under the Medallion Architecture (Bronze → Silver → Gold).

👉 Key Highlights:

⚡ Incremental data ingestion using Change Data Capture (CDC)

🗂️ Star schema modeling (Facts & Dimensions)

🔄 Slowly Changing Dimensions (SCD Type 1) handling

🔑 Parameterized pipelines for scalable deployment

🧾 Data governance, lineage, and schema enforcement with Unity Catalog

📊 Power BI dashboards for visualization

🏗️ Architecture
<p align="center"> <img src="https://miro.medium.com/v2/resize:fit:1400/format:webp/1*zVnWJtyGOX_kUIDm6ccCFQ.png" width="700"/> </p>
🔹 Data Flow Breakdown

Data Source (Azure SQL Database)

Source tables hosted in Azure SQL Database.

Initial + incremental loads staged from sample datasets.

Ingestion Layer (Azure Data Factory – Bronze Layer)

ADF pipelines extract data into Azure Data Lake (Bronze).

Data stored in Parquet format for efficiency.

Implemented incremental ingestion (only new/updated records).

Transformation Layer (Databricks – Silver Layer)

Data cleaned, validated, and structured into Facts & Dimensions.

Applied Star Schema design for analytics.

Managed Slowly Changing Dimensions (SCD Type 1) using upserts.

Serving Layer (Databricks + Delta Lake – Gold Layer)

Final data written to Delta format for:

ACID transactions

Time Travel

Schema evolution

Optimized for BI and downstream analytics.

Governance & Quality (Unity Catalog)

Centralized governance: RBAC, lineage tracking, auditing, and schema validation.

Visualization (Power BI)

Gold layer connected to Power BI.

Created dashboards for insights and KPIs.

⚙️ Tech Stack

Azure → Data Factory, Data Lake, SQL Database

Databricks → PySpark, Delta Lake, Unity Catalog

Modeling → Star Schema, Facts & Dimensions, SCD Type 1

File Formats → CSV → Parquet → Delta

Governance → Unity Catalog (lineage, auditing, RBAC)

BI → Power BI

📊 Scenarios Implemented

✅ Incremental Data Loading (CDC + Stored Procedures)
✅ Star Schema with Facts & Dimensions
✅ Slowly Changing Dimensions (SCD Type 1 – Upserts)
✅ Schema Evolution & Time Travel (Delta Lake)
✅ Data Governance with Unity Catalog
✅ Parameterized Pipelines for flexible deployments

📌 How to Run

Clone the repo and provision Azure resources.

Set up Resource Group → Data Lake → SQL Database → ADF → Databricks.

Load source data into Azure SQL Database.

Configure ADF pipelines for ingestion into Bronze.

Use Databricks notebooks to transform into Silver & Gold.

Connect Power BI to Gold for dashboarding.

✨ This project demonstrates the end-to-end design and implementation of a cloud-native data pipeline, covering ingestion, transformation, governance, and visualization.
