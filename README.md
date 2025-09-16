# 🚀 Azure End-to-End Data Engineering Pipeline  

![Azure](https://img.shields.io/badge/Azure-Data%20Engineering-blue)  
![Databricks](https://img.shields.io/badge/Databricks-Lakehouse-orange)  
![ETL](https://img.shields.io/badge/ETL-Pipeline-green)  
![PowerBI](https://img.shields.io/badge/PowerBI-Dashboard-yellow)  

---

## 📌 Project Overview  
This project demonstrates the design and implementation of a **real-world Azure Data Engineering pipeline**.  
It integrates **Azure SQL Database, Azure Data Factory (ADF), Azure Data Lake, Databricks, Delta Lake, Unity Catalog, and Power BI** under the **Medallion Architecture** (Bronze ➝ Silver ➝ Gold).  

---

## ✨ Key Highlights  
- ⚡ **Incremental data ingestion** using **Change Data Capture (CDC)**  
- 🗂️ **Star schema modeling** (Facts & Dimensions)  
- 🔄 **Slowly Changing Dimensions (SCD Type 1)** handling  
- 🔑 **Parameterized pipelines** for scalable deployment  
- 🔐 **Data governance, lineage, and schema enforcement** with Unity Catalog  
- 📊 **Power BI dashboards** for visualization  

---

## 🏗️ Architecture  

<p align="center">
  <img src="https://raw.githubusercontent.com/tkaushik015/Enterprise-Data-Governance-and-Analytics-Framework/main/architecture.png" width="800"/>
</p>  

The pipeline follows a **layered Medallion Architecture**:  

1. **Data Source** → Azure SQL Database  
   - Source tables hosted in Azure SQL DB  
   - Both **initial** and **incremental loads** staged  

2. **Ingestion Layer (Bronze)** → Azure Data Factory  
   - Data extracted into **Azure Data Lake (Bronze)**  
   - Stored in **Parquet format** for efficiency  
   - Incremental ingestion: only new/updated records  

3. **Transformation Layer (Silver)** → Azure Databricks  
   - Data cleaning, joins, and transformations with **PySpark**  
   - Creation of **dimension & fact tables**  
   - Implementation of **SCD Type 1**  

4. **Serving Layer (Gold)** → Delta Lake  
   - Modeled **star schema** for analytics  
   - Optimized storage for reporting  

5. **Governance & Security** → Unity Catalog  
   - Lineage tracking, schema enforcement, access control  

6. **Visualization** → Power BI  
   - Dashboards for KPIs, business insights, and reporting  

---

## 🔄 Data Flow  

📥 **Data Source**: Azure SQL DB  
⬇️  
📦 **Bronze**: Raw ingested data via ADF (Parquet)  
⬇️  
🧹 **Silver**: Cleaned, enriched data in Databricks (SCD, transformations)  
⬇️  
⭐ **Gold**: Business-ready data (Facts & Dimensions)  
⬇️  
📊 **Power BI**: Interactive dashboards  

---

## 🛠 Data Pipeline Flow  

📂 SQL DB
⬇️ Extracted via ADF → Bronze Layer (raw data, stored in Parquet)

⬇️ Cleaned & transformed in Databricks → Silver Layer (joins, deduplication, business rules)

⬇️ Modeled into Gold Layer (✅ Facts & Dimensions with Star Schema)

⬇️ Governed with Unity Catalog (🔐 schema enforcement, lineage, data governance)

⬇️ Visualized in Power BI Dashboards (📊 KPIs, trends, business insights)
