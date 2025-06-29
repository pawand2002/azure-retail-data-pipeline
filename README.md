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

graph TD
    A[User / External System] -- Uploads sales.csv --> B(sales.csv File);

    subgraph Data Ingestion & Processing Azure Data Factory Orchestration
        direction LR
        B -- "1. Raw Ingestion (ADF Pipeline)" --> C(ADF Bronze Ingestion);
        C -- "Stores as-is" --> D[ADLS Gen2<br><b>Bronze Layer</b><br><i>(sales/)</i>];

        D -- "2. Clean & Transform (ADF Pipeline)" --> E(ADF Silver Transformation);
        E -- "Stores as Parquet" --> F[ADLS Gen2<br><b>Silver Layer</b><br><i>(sales_cleaned/)</i>];

        F -- "3. Aggregate Data (ADF Pipeline)" --> G(ADF Gold Aggregation);
        G -- "Stores as Parquet" --> H[ADLS Gen2<br><b>Gold Layer</b><br><i>(sales_summary/)</i>];
    end

    H -- "4. Consumption" --> I[Power BI<br><i>(Dashboard Layer)</i>];

    %% --- Styling for Professional Look ---
    classDef mainNode fill:#f9f,stroke:#333,stroke-width:2px;
    classDef component fill:#add8e6,stroke:#333,stroke-width:2px;
    classDef storageLayer fill:#fffacd,stroke:#333,stroke-width:2px;
    classDef outputLayer fill:#DA70D6,stroke:#333,stroke-width:2px;

    class A mainNode;
    class B mainNode;
    class C component;
    class D storageLayer;
    class E component;
    class F storageLayer;
    class G component;
    class H storageLayer;
    class I outputLayer;
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

