# Amazon Prime Movies & TV Shows  
## End-to-End Azure Data Engineering Pipeline

## 📌 Project Overview
This project demonstrates an **end-to-end, production-style data engineering pipeline** built on **Microsoft Azure**, using the Amazon Prime Movies and TV Shows dataset.

The objective is to ingest raw data, process and transform it using a **medallion architecture**, store it efficiently in a data lake, and make it analytics-ready for downstream reporting and visualization.

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

---

## ⚙️ Databricks Challenge & Solution
While setting up Azure Databricks, a key challenge encountered was **VM unavailability in certain regions**, which prevented cluster creation.

### ✅ Resolution
- Verified VM availability using **Azure CLI**
- Selected a **4-core, 16 GB RAM VM**
- Configured a **single-node Databricks cluster**
- Successfully executed PySpark workloads

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


