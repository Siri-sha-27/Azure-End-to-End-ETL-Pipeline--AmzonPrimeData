![Python](https://img.shields.io/badge/Python-3.x-blue)
![Azure](https://img.shields.io/badge/Azure-Cloud-blue)
![Databricks](https://img.shields.io/badge/Databricks-PySpark-red)
![Delta Lake](https://img.shields.io/badge/Delta-Lake-green)
![Power BI](https://img.shields.io/badge/PowerBI-Visualization-yellow)

# Amazon Prime Movies & TV Shows  
## End-to-End Azure Data Engineering Pipeline

## 📌 Project Overview
This project demonstrates an **end-to-end, production-style data engineering pipeline** built on **Microsoft Azure**, using the Amazon Prime Movies and TV Shows dataset.

The objective is to ingest raw data, process and transform it using a **medallion architecture**, store it efficiently in a data lake, and make it analytics-ready for downstream reporting and visualization.
<img width="1303" height="685" alt="Screenshot 2026-01-31 235736" src="https://github.com/user-attachments/assets/0dfcef88-7cb8-406c-b42f-ba13bd3a8d71" />


The dataset contains metadata such as:
- Title name  
- Release year  
- Genre  
- Duration  
- Ratings  
- Content type (Movie / TV Show)

---

## 🛠️ Tech Stack & Tools
- **GitHub** – Source data storage and version control  
- **Azure Data Factory (ADF)** – Data ingestion and orchestration  
- **Azure Data Lake Storage Gen2 (ADLS)** – Centralized data lake  
- **Azure Databricks (PySpark)** – Data processing and transformations  
- **Azure Synapse Analytics (Serverless SQL Pool)** – Analytics and querying  
- **Power BI** *(Planned)* – Dashboards and visualization  

---

## 📂 Dataset
- **Source**: Kaggle  
- **Dataset**: Amazon Prime Movies and TV Shows  
- **Link**: https://www.kaggle.com/datasets/shivamb/amazon-prime-movies-and-tv-shows  

The dataset is stored in GitHub and ingested into Azure using Azure Data Factory.

---

## 🏗️ Architecture Overview
The pipeline follows the **Medallion Architecture** pattern:

### 🥉 Bronze Layer (Raw Data)
- Raw CSV files ingested from GitHub using **Azure Data Factory Copy Activity**
- Stored in the **ADLS Bronze container**
- No transformations applied

### 🥈 Silver Layer (Cleaned & Enriched)
- Data read from the Bronze layer using **Azure Databricks**
- Data cleaning, validation, and schema standardization performed using **PySpark**
- Exploratory Data Analysis (EDA) and enrichment applied
- Output written to **ADLS Silver container** in **Parquet format**
- PySpark notebooks available in the repository under:

### 🥇 Gold Layer (Analytics-Ready)
- Data read from the Silver layer
- Final preprocessing and feature engineering applied:
- Standardized date formats  
- Creation of derived columns (e.g., normalized genres)  
- Business-ready aggregations  
- Output written to **ADLS Gold container** in **Delta format**
- Optimized for analytics and BI consumption
<img width="1919" height="935" alt="Screenshot 2026-01-31 235121" src="https://github.com/user-attachments/assets/64bc6f4d-a297-4c57-8490-b2f183c9e609" />

---

## 🔄 Data Pipeline Flow
1. **Ingestion**
 - Azure Data Factory fetches CSV files from GitHub
 - Stores raw data in the Bronze container

2. **Transformation (Silver Layer)**
 - Azure Databricks reads raw data from ADLS
 - Cleans, validates, and enriches data
 - Writes processed data in Parquet format

3. **Transformation (Gold Layer)**
 - Applies final transformations and feature engineering
 - Writes analytics-ready Delta tables

4. **Analytics**
 - Azure Synapse queries Gold layer data directly from ADLS
 - Uses serverless SQL pools (no dedicated warehouse required)
   <img width="1608" height="981" alt="Screenshot 2026-01-31 235055" src="https://github.com/user-attachments/assets/599f2ffe-931b-4041-b877-4586b489369f" />


---

## ⚙️ Databricks Challenge & Solution
While setting up Azure Databricks, a key challenge encountered was **VM unavailability in certain regions**, which prevented cluster creation.

### ✅ Resolution
- Verified VM availability using **Azure CLI**
- Selected a **4-core, 16 GB RAM VM**
- Configured a **single-node Databricks cluster**
- Successfully executed PySpark workloads
<img width="1918" height="982" alt="Screenshot 2026-01-31 235013" src="https://github.com/user-attachments/assets/a2acdd1d-4f72-44d8-ae3f-76ba065e347f" />
This reflects a real-world production constraint and its resolution.


---

## 🔐 Security & Access
- Azure Databricks connected to ADLS using **Client Secrets**
- Secure authentication without hardcoding credentials
- Follows Azure best practices for secure data access

---


## 📊 Analytics with Azure Synapse
- Gold layer Delta tables queried using **Azure Synapse Analytics**
- Configured with **built-in serverless SQL pools**
- Enables on-demand analytics directly on data lake storage

---

## 📈 Future Enhancements
- Integrate **Power BI** dashboards using Synapse queries
- Implement incremental data loading
- Add data quality checks and monitoring
- Schedule automated pipeline runs using ADF triggers
<img width="1165" height="687" alt="image" src="https://github.com/user-attachments/assets/05555878-cd25-4d98-944d-def60b5572fa" />



