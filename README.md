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

                ┌────────────┐
                │  Raw File  │   (e.g., sales.csv upload)
                └────┬───────┘
                     │
             ┌───────▼────────────────┐
             │    ADF Ingestion       │
             │  (Trigger-based)       │
             └───────┬────────────────┘
                     │
            ▓▓▓▓ BRONZE LAYER ▓▓▓▓
         (Raw zone - as-is ingest via ADF)

                     ▼
        Stored in → ADLS Gen2 /bronze/sales/

                     │
             ┌───────▼────────────────────┐
             │   ADF Data Flow Transform  │
             │ - Null handling            │
             │ - Type casting             │
             │ - New columns (e.g., Profit)|
             └───────┬────────────────────┘
                     │
            ▓▓▓▓ SILVER LAYER ▓▓▓▓
      (Cleansed zone – conforming format)

                     ▼
       Stored in → ADLS Gen2 /silver/sales_cleaned/

                     │
             ┌───────▼────────────────────┐
             │     ADF Aggregation Flow   │
             │ - Region & Date grouping   │
             │ - Sales metrics            │
             └───────┬────────────────────┘
                     │
            ▓▓▓▓ GOLD LAYER ▓▓▓▓
    (Business zone – analytical data marts)

                     ▼
       Stored in → ADLS Gen2 /gold/sales_summary/

                     │
             ┌───────▼────────────────────┐
             │        Power BI            │
             │ - Dashboards (upcoming)    │
             │ - Row-Level Security (RLS)│
             └────────────────────────────┘

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

