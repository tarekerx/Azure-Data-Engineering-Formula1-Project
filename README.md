# Azure Databricks & Apache Spark: End-to-End Formula 1 Data Engineering Project

## 📌 Project Overview
This project focuses on building a production-ready, end-to-end data engineering pipeline for Formula 1 racing data using the Azure Cloud ecosystem. The system ingests raw race metrics, processes them through a multi-tier lakehouse architecture (Medallion Architecture), and orchestrates automated pipelines to simulate real-world data processing workloads.

The project structure contains historical data ingestion layouts, schema definitions, baseline transformations, and a dedicated production pipeline designed to handle updates incrementally using Delta Lake.

---

## 🛠️ Tech Stack & Architecture
* **Cloud Platform:** Microsoft Azure
* **Processing Engine:** Apache Spark (PySpark & SparkSQL)
* **Compute Workspace:** Azure Databricks
* **Storage Layer:** Azure Data Lake Storage Gen2 (ADLS Gen2)
* **Storage Format:** Delta Lake (ACID transactions, Time Travel)
* **Orchestration:** Databricks Workflows (Pipeline Jobs)

### Data Pipeline Architecture (Medallion Pattern)
Raw data -> bronze layer -> silver layer -> gold layer -> analytics layer 

---

## ⚙️ Core Pipeline Features

### 1. Multi-Format Data Ingestion (Bronze Layer)
* Ingested multiple nested structures and formats including **JSON** (constructors, drivers, results) and **CSV** (circuits, races).
* Enforced strict, programming-defined schemas rather than relying on schema inference to ensure data quality and system stability.

### 2. High-Performance Transformations (Silver Layer)
* Handled data cleaning processes: renaming columns dynamically, dropping duplicates, adding ingestion timestamps, and flattening complex array structures.
* Implemented date-time formatting updates to standardize timezone metrics across global racing circuits.

### 3. Production Incremental Loading (Gold Layer)
* Leveraged **Delta Lake** functionalities to perform efficient `MERGE` (upsert) operations, ensuring that processing runs only capture new or updated race details without rewriting historical records.
* Created optimized analytical reporting tables detailing driver standings, constructor dominance, and historical track performance metrics.

### 4. Orchestration & Automation via Databricks Workflows
* Fully automated the notebooks utilizing **Databricks Jobs**.
* Built out a sequential Task Dependency graph to ensure data consistency (e.g., Ingestion must complete successfully before Transformations kick off).
* Maintained automated execution logic configurations for scheduled production processing.

---

## 📂 Repository Structure
The project is organized into the following components:

```bash
├── Pipeline jobs/                     # Exported pipeline job configurations
│   ├── Formula1/                      # Workflow details for baseline pipeline execution
│   └── job_formula1_incremental/      # Workflow configuration for incremental runs
├── formula1-project-incremental-load/ # Production incremental pipeline architecture
│   ├── formula1-projects-incremental-load/ # Delta Lake optimized merge and upsert logic notebooks
│   └── manifest.mf                    # Export manifest metadata
├── formula1-project/                  # Core baseline transformation layout
│   ├── formula1-projects/             # Notebooks handling raw data ingestion and transformations
│   └── manifest.mf                    # Export manifest metadata
└── README.md                          # Project documentation
