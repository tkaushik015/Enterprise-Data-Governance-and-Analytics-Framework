# 🚀 Azure End-to-End Data Engineering Pipeline (Job-Ready)

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
10. [📖 References](#references)  

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
