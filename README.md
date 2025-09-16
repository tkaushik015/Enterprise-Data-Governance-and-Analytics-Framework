# 🚀 Azure End-to-End Data Engineering Pipeline 

🔗 **GitHub Repository:** https://github.com/yourusername/azure-data-engineering-bootcamp

---

## 📚 Table of Contents
1. [Project Overview](#project-overview)  
2. [🏗️ Architecture](#architecture)  
3. [💾 Data Sources](#data-sources)  
4. [⚙️ Key Features & Concepts](#key-features--concepts)  
5. [🔧 Technology Stack](#technology-stack)  
6. [🚀 Getting Started](#getting-started)  
   - 🛠️ [Prerequisites](#prerequisites)  
   - 📥 [Clone the Repo](#clone-the-repo)  
   - ☁️ [Azure Provisioning](#azure-provisioning)  
   - ⚙️ [Configuration](#configuration)  
   - ▶️ [Run the Pipeline](#run-the-pipeline)  
7. [📂 Folder Structure](#folder-structure)  
8. [🧠 Key Learnings & Challenges](#key-learnings--challenges)  
9. [🔮 Future Improvements](#future-improvements)  


---

## Project Overview
An **end-to-end** Azure Data Engineering pipeline built in a production-ready, job-focused bootcamp:

- **Source Prep:** Pull CSV sales data from a GitHub repo into Azure SQL DB.  
- **Bronze Layer:** Incrementally load only new records into ADLS Gen2 as Parquet.  
- **Silver Layer:** Conform to a star schema in Databricks, split combined sales data into facts & dimensions, generate surrogate keys, and apply **SCD Type 1 (upsert)**.  
- **Gold Layer:** Build optimized Delta tables for business consumption.  
- **Governance:** Secure access with Unity Catalog and Managed Identities.  
- **Consumption:** Serve final datasets to Power BI for quick analytics.

---

## 🏗️ Architecture
```text
 GitHub CSV  →  Azure SQL DB  →  ADLS Gen2 (Bronze)
                                             │
                                             ▼
                                   Azure Databricks (Silver)
                                             │
                                             ▼
                                   Azure Databricks (Gold)
                                             │
                                             ▼
                                    Power BI / Analytics
💾 Data Sources
Sales Data (CSV)

Combined “facts + dimensions” table with columns:
branch_id, dealer_id, model_id, date_id, revenue, units

Config JSON

Defines initial vs. incremental loads, file patterns & table mappings

⚙️ Key Features & Concepts
Medallion Architecture
Bronze → Silver → Gold logical layers to separate raw ingestion from curated models

Incremental CDC Processing

Pipeline identifies only new rows each run, avoiding full re-loads

Dynamic, Parameterized ADF Pipelines

Lookup activity reads JSON config

ForEach iterates tables/months with parameters (sourcePath, targetPath, watermarkCol)

Parquet & Delta Lake

Bronze writes Parquet for efficiency

Silver & Gold use Delta for ACID, time travel & versioning

Star Schema & SCD Type 1

Split raw data into FactSales and dimension tables (DimBranch, DimDealer, DimModel, DimDate)

Upsert logic in Silver to overwrite changed dimension attributes

Unity Catalog Governance
Unified metastore for catalogs, schemas and fine-grained access control

Secure Secret Management

Azure Key Vault for all service credentials

Managed Identities for ADF & Databricks

Power BI Integration

Live connector to Gold Delta tables for sub-hourly dashboard refreshes

🔧 Technology Stack
Layer	Tools & Services
Orchestration	Azure Data Factory
Storage	Azure Data Lake Storage Gen2
Compute	Azure Databricks (PySpark, Delta Lake)
Database	Azure SQL Database
Governance	Unity Catalog, Azure Key Vault
Visualization	Power BI
Source Control	Git & GitHub

🚀 Getting Started
🛠️ Prerequisites
Azure subscription with:

Data Factory, Storage Account, Databricks workspace, SQL Database, Key Vault

Local: Azure CLI, Databricks CLI, Git

📥 Clone the Repo
bash
Copy
Edit
git clone https://github.com/yourusername/azure-data-engineering-bootcamp.git
cd azure-data-engineering-bootcamp/project2
☁️ Azure Provisioning
Create Resource Group

bash
Copy
Edit
az group create -n rg-azure-de-eng -l eastus
Create Storage Account & Containers

bash
Copy
Edit
az storage account create -n stazuredeeng \
  --resource-group rg-azure-de-eng --hierarchical-namespace true
az storage container create -n bronze --account-name stazuredeeng
az storage container create -n silver --account-name stazuredeeng
az storage container create -n gold   --account-name stazuredeeng
Provision Key Vault & Secrets

bash
Copy
Edit
az keyvault create -n kv-azure-de-eng -g rg-azure-de-eng
az keyvault secret set -n "SQLConn"      --vault-name kv-azure-de-eng --value "<conn-string>"
az keyvault secret set -n "StorageKey"   --vault-name kv-azure-de-eng --value "<storage-key>"
az keyvault secret set -n "DatabricksPAT"--vault-name kv-azure-de-eng --value "<pat>"
⚙️ Configuration
Upload GitHub CSVs to your Azure SQL DB source tables.

Place config/project2_config.json in the lookup/ container of your storage account.

Ensure JSON includes keys: tableName, isIncremental, sourceQuery, watermarkColumn.

▶️ Run the Pipeline
Import ADF JSON definitions into your Data Factory.

Link your Linked Services (SQL DB, ADLS, Key Vault).

Trigger the master pipeline (pipeline_project2_master).

Monitor runs in ADF Monitor → verify Parquet files in Bronze.

Check Silver & Gold Delta tables in Databricks SQL:

sql
Copy
Edit
SELECT COUNT(*) FROM bronze.raw_sales;
SELECT COUNT(*) FROM silver.fact_sales;
SELECT COUNT(*) FROM gold.fact_sales;
Connect Power BI to your Databricks workspace, select Gold schema for live reports.

📂 Folder Structure
pgsql
Copy
Edit
project2/
├── configs/
│   └── project2_config.json
├── lookup/
│   └── raw_sales.csv
├── pipelines/
│   └── ADF_definitions/
├── notebooks/
│   ├── 01_load_bronze.py
│   ├── 02_transform_silver.py
│   └── 03_build_gold.py
└── README.md
🧠 Key Learnings & Challenges
Designing CDC-based incremental loads to avoid reprocessing.

Implementing dynamic pipelines with Lookup & ForEach for maintainability.

Mastering Delta Lake upserts for SCD Type 1.

Securing assets with Unity Catalog & Managed Identities.

🔮 Future Improvements
Add SCD Type 2 to track full dimension history.

Integrate Event Hubs + Stream Analytics for real-time ingest.

Automate CI/CD for ADF & notebooks via GitHub Actions.

Incorporate data quality checks with Great Expectations or Deequ.
