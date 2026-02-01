![Python](https://img.shields.io/badge/Python-3.x-blue)
![Azure](https://img.shields.io/badge/Azure-Cloud-blue)
![Databricks](https://img.shields.io/badge/Databricks-PySpark-red)
![Delta Lake](https://img.shields.io/badge/Delta-Lake-green)
![Power BI](https://img.shields.io/badge/PowerBI-Visualization-yellow)

# Amazon Prime Movies & TV Shows  
## End-to-End Azure Data Engineering Pipeline

---

## 📌 Project Overview

This project was built to **understand how real-world data engineering pipelines are designed, implemented, and operated on Azure**.

Instead of just processing data locally, I wanted to experience:
- How data is ingested from external sources
- How raw data is gradually refined into analytics-ready datasets
- How different Azure services work together in a production-style workflow

For this purpose, I used the **Amazon Prime Movies and TV Shows dataset**, which contains metadata about titles such as release year, genre, duration, ratings, and content type.

<img width="1303" height="685" alt="Architecture Overview" src="https://github.com/user-attachments/assets/0dfcef88-7cb8-406c-b42f-ba13bd3a8d71" />

---

## 🛠️ Tech Stack & Tools (What I Actually Used)

- **GitHub** – Hosted the source dataset and versioned transformation notebooks  
- **Azure Data Factory (ADF)** – Ingested data from GitHub and orchestrated the pipeline  
- **Azure Data Lake Storage Gen2 (ADLS)** – Stored data across Bronze, Silver, and Gold layers  
- **Azure Databricks (PySpark)** – Performed data cleaning, validation, and transformations  
- **Delta Lake & Parquet** – Used for efficient storage and analytics-ready tables  
- **Azure Synapse Analytics (Serverless SQL)** – Queried Gold-layer data directly from the lake  
- **Power BI** – Built exploratory dashboards by connecting to Databricks  

---

## 📂 Dataset

- **Source**: Kaggle  
- **Dataset**: Amazon Prime Movies and TV Shows  
- **Link**: https://www.kaggle.com/datasets/shivamb/amazon-prime-movies-and-tv-shows  

The dataset was stored in GitHub and fetched into Azure using **Azure Data Factory**, simulating a real external data source.

---

## 🏗️ Architecture & Design Choice

I followed the **Medallion Architecture** to clearly separate concerns and understand how data evolves across stages.

### 🥉 Bronze Layer – Raw Ingestion
- Raw CSV files copied from GitHub using **ADF Copy Activity**
- Stored exactly as received in the **Bronze container**
- No transformations applied at this stage  
- Purpose: **Preserve original data for traceability**

---

### 🥈 Silver Layer – Cleaning & Standardization
- Data read from Bronze into **Azure Databricks**
- Performed:
  - Schema validation
  - Handling missing and inconsistent values
  - Basic enrichment and formatting
- Output written back to ADLS in **Parquet format**
- PySpark notebooks are included in the repository for transparency

Purpose: **Create a reliable, clean dataset for downstream use**

---

### 🥇 Gold Layer – Analytics Ready
- Data reloaded from Silver layer
- Applied final transformations such as:
  - Consistent date formatting
  - Genre normalization
  - Creation of derived and helper columns
- Stored as **Delta tables** in the Gold container

<img width="1919" height="935" alt="Gold Layer Tables" src="https://github.com/user-attachments/assets/64bc6f4d-a297-4c57-8490-b2f183c9e609" />

Purpose: **Serve clean, query-optimized data for analytics and BI tools**

---

## 🔄 End-to-End Data Flow

1. **Ingestion**
   - Azure Data Factory pulls data from GitHub
   - Stores raw CSV files in Bronze

2. **Silver Transformations**
   - Databricks processes raw data
   - Applies cleaning and validation
   - Writes Parquet files to Silver

3. **Gold Transformations**
   - Final feature engineering
   - Writes Delta tables to Gold

4. **Analytics**
   - Azure Synapse serverless SQL queries data directly from ADLS

<img width="1608" height="981" alt="Synapse Query" src="https://github.com/user-attachments/assets/599f2ffe-931b-4041-b877-4586b489369f" />

---

## ⚙️ Real Challenge Faced (Databricks VM Availability)

While setting up Azure Databricks, I faced an issue where **clusters could not be created due to VM unavailability in certain regions**.

Instead of changing the project scope, I:
- Checked VM availability using **Azure CLI**
- Selected a **4-core, 16 GB RAM VM**
- Configured a **single-node Databricks cluster**
- Successfully ran PySpark workloads

<img width="1918" height="982" alt="Databricks Cluster" src="https://github.com/user-attachments/assets/a2acdd1d-4f72-44d8-ae3f-76ba065e347f" />

This helped me understand how **infrastructure constraints impact data engineering decisions**.

---

## 🔐 Security & Access Control

- Connected Databricks to ADLS using **Client Secrets**
- Avoided hardcoding credentials
- Followed Azure-recommended authentication practices

This reinforced the importance of **secure data access in cloud environments**.

---

## 📊 Analytics & Visualization

- Queried Gold-layer Delta tables using **Azure Synapse serverless SQL pools**
- Built Power BI visuals by connecting directly to Databricks
- Created views such as:
  - Content distribution by type
  - Content growth over time
  - Genre and country-level insights

<img width="1165" height="687" alt="Power BI Dashboard" src="https://github.com/user-attachments/assets/05555878-cd25-4d98-944d-def60b5572fa" />

---

## 📈 Future Improvements

- Build a full Power BI dashboard using Synapse queries
- Add incremental loading logic in ADF
- Implement data quality checks
- Schedule automated pipeline runs
- Add monitoring and alerting

---

## 🧠 Key Learnings

- How Azure services integrate in a real pipeline
- Why medallion architecture is important
- How storage formats affect analytics
- How to troubleshoot infrastructure issues
- How to design data for BI consumption

This project helped me move from **theory to hands-on understanding of cloud data engineering**.
