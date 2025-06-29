# 🚀 End-to-End Azure Data Engineering Project – Retail Sales ETL Pipeline

This project demonstrates a complete Data Engineering workflow using Azure tools. It simulates ingesting sales data from a source CSV, transforming it through Bronze → Silver → Gold layers, and preparing it for reporting with Power BI.

---
## ✨ Features

* **Automated Data Ingestion:** Securely ingests raw sales data into a data lake.
* **Layered Data Architecture:** Implements a Medallion Architecture (Bronze, Silver, Gold) for data quality and reusability.
* **Data Transformation & Cleansing:** Handles data type conversions, null values, and derives new metrics.
* **Data Aggregation:** Prepares summarized data suitable for analytical reporting.
* **Cloud-Native & Scalable:** Built entirely on Azure, ensuring scalability and cost-effectiveness.
* **Version Controlled:** All pipeline definitions and code are managed via Git.

---

## 🧰 Tech Stack

- **Azure Data Factory** – Pipelines, Data Flows, Orchestration
- **Azure Data Lake Storage Gen2** – Bronze, Silver, Gold zone structure
- **Parquet Format** – Optimized columnar storage
- **Power BI** – Dashboard layer (to be added)
- **Git** – Source control
- **Python (optional)** – For local data inspection (not used here)

---

## 📊 Data Pipeline Overview

### 🔹 Bronze Layer
- Raw ingestion of uploaded `sales.csv` via ADF pipeline
- Stored as-is in ADLS Gen2 in `bronze/sales/`

### 🔸 Silver Layer
- Cleaned data with derived columns (e.g., `Profit = Sales - Cost`)
- Type conversions and null handling
- Saved as Parquet in `silver/sales_cleaned/`

### 🟡 Gold Layer
- Aggregated data by region and date
- Business-level metrics prepared for analytics
- Stored in `gold/sales_summary/`

---
### 🏅 Medallion Architecture Detail

This diagram illustrates the flow of data through the Bronze, Silver, and Gold layers within Azure Data Lake Storage Gen2, representing the progressive refinement of data.

```mermaid
graph TD
    subgraph "Azure Data Lake Storage Gen2"
        direction LR
        bronze_zone["**Bronze Zone**<br>_Raw, Immutable Data_<br>(e.g., `sales.csv` as-is)"]
        silver_zone["**Silver Zone**<br>_Cleaned, Conformed Data_<br>(Parquet Format)"]
        gold_zone["**Gold Zone**<br>_Aggregated, Business-Ready Data_<br>(Parquet Format)"]
    end

    bronze_zone -- "1. ETL (ADF Pipeline)<br>Cleansing & Transformation" --> silver_zone;
    silver_zone -- "2. ETL (ADF Pipeline)<br>Aggregation & Modeling" --> gold_zone;

    gold_zone -- "Consumed by BI & Analytics Tools" --> powerbi_consumer[Power BI / Analytics];

    %% --- Styling for Medallion Layers ---
    classDef medallionLayer fill:#FFFACD,stroke:#333,stroke-width:2px;
    classDef consumerNode fill:#DA70D6,stroke:#333,stroke-width:2px;

    class bronze_zone,silver_zone,gold_zone medallionLayer;
    class powerbi_consumer consumerNode;
```
---
## 🏗️ Architecture Diagram
```mermaid
graph TD
    subgraph Data Source
        A[Retail Sales Data Source]
    end

    subgraph Orchestration & Processing
        B[Azure Data Factory]
    end

    subgraph "Data Storage (Azure Data Lake Storage Gen2)"
        C("Bronze Zone<br><i>(Raw Data)</i>")
        D("Silver Zone<br><i>(Cleaned Data)</i>")
        E("Gold Zone<br><i>(Aggregated Data)</i>")
    end

    subgraph Business Intelligence
        F[Power BI]
    end

    subgraph Development & Version Control
        G[Git Repository]
    end

    A -- "Ingests Data" --> B;
    B -- "Orchestrates Storage into" --> C;
    C -- "Transforms Data via ADF" --> D;
    D -- "Aggregates Data via ADF" --> E;
    E -- "Consumes for Reporting" --> F;

    G -- "Manages ADF & Pipeline Code" --> B;

    %% --- Styling for Professional Look ---
    classDef source fill:#DDFFAA,stroke:#333,stroke-width:2px;
    classDef orchestrator fill:#ADD8E6,stroke:#333,stroke-width:2px;
    classDef storage fill:#FFFACD,stroke:#333,stroke-width:2px;
    classDef bi fill:#DA70D6,stroke:#333,stroke-width:2px;
    classDef devops fill:#C0C0C0,stroke:#333,stroke-width:2px;

    class A source;
    class B orchestrator;
    class C,D,E storage;
    class F bi;
    class G devops;
```
---

## 🔁 Pipeline Details

| Layer  | ADF Components        | Notes                           |
|--------|-----------------------|----------------------------------|
| Bronze | Copy activity         | Ingests CSV into ADLS            |
| Silver | Data Flow + Sink      | Data cleaning + derived columns  |
| Gold   | Data Flow + Sink      | Aggregation logic applied        |

---

## 📈 Power BI (Coming Soon)
- Planned dashboard connection to Gold layer via ADLS or Synapse
- KPIs: Total Sales, Profit by Region, Category Trends

---

## 📂 Folder Structure

azure-retail-sales-pipeline/
├── README.md
├── architecture.png
├── adf_pipeline_jsons/
├── screenshots/
└── data/

