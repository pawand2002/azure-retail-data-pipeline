# 🚀 End-to-End Azure Data Engineering Project – Retail Sales ETL Pipeline

This project demonstrates a complete Data Engineering workflow using Azure tools. It simulates ingesting sales data from a source CSV, transforming it through Bronze → Silver → Gold layers, and preparing it for reporting with Power BI.

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

## 🏗️ Architecture Diagram
```mermaid
graph TD
    subgraph Data Source
        A[Retail Sales Data Source]
    end

    subgraph Orchestration & Processing
        B[Azure Data Factory]
    end

    subgraph Data Storage (Azure Data Lake Storage Gen2)
        C(Bronze Zone<br><i>(Raw Data)</i>)
        D(Silver Zone<br><i>(Cleaned Data)</i>)
        E(Gold Zone<br><i>(Aggregated Data)</i>)
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

