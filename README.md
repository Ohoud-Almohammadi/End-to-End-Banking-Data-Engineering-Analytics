# 🏦 End-to-End Banking Data Engineering & Analytics

![Azure](https://img.shields.io/badge/Azure-0078D4?style=for-the-badge\&logo=microsoftazure\&logoColor=white)
![Azure Data Factory](https://img.shields.io/badge/Azure%20Data%20Factory-0078D4?style=for-the-badge\&logo=microsoftazure\&logoColor=white)
![Azure Databricks](https://img.shields.io/badge/Azure%20Databricks-FF3621?style=for-the-badge\&logo=databricks\&logoColor=white)
![Delta Lake](https://img.shields.io/badge/Delta%20Lake-00ADD8?style=for-the-badge\&logo=delta\&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge\&logo=powerbi\&logoColor=black)

## 📌 Project Overview

This project demonstrates the design and implementation of an end-to-end data engineering and analytics solution for banking transaction data.

The solution follows a modern **Lakehouse Architecture**, transforming raw banking data into clean, structured, and analytics-ready datasets. The pipeline covers the complete data lifecycle, from data ingestion and transformation to dimensional modeling, aggregation, and interactive business intelligence reporting.

The project demonstrates practical implementation of cloud-based data engineering concepts, including data pipelines, Medallion Architecture, Delta Lake, dimensional modeling, data aggregation, and Power BI Composite Models.

---

## 🎯 Project Objectives

* Build an end-to-end data pipeline for banking transaction data.
* Implement a Medallion Architecture using Bronze, Silver, and Gold layers.
* Ingest raw CSV and JSON files using Azure Data Factory.
* Store and manage data using Azure Data Lake Storage Gen2.
* Transform and clean large-scale transaction data using Azure Databricks and PySpark.
* Implement dimensional data modeling using Fact and Dimension tables.
* Create an aggregation layer to improve analytical query performance.
* Build a Power BI Composite Model using Import, DirectQuery, and Aggregations.
* Develop interactive dashboards for transaction, customer, merchant, and geographic analytics.

---

## 🏗️ Solution Architecture

```text
Source Data
    │
    ▼
Azure Data Lake Storage Gen2
(Bulk / Raw Files)
    │
    ▼
Azure Data Factory
(Data Ingestion)
    │
    ▼
Bronze Layer
Raw Data
    │
    ▼
Silver Layer
Cleaned & Standardized Data
    │
    ▼
Gold Layer
Dimensional Model
    │
    ├── fact_transactions
    ├── dim_users
    ├── dim_cards
    ├── dim_date
    └── dim_mcc
    │
    ▼
Aggregation Layer
agg_transaction_daily
    │
    ▼
Power BI
Composite Model & Dashboards
```

---

## 🛠️ Technologies Used

| Technology                   | Purpose                                      |
| ---------------------------- | -------------------------------------------- |
| Azure Data Factory           | Data ingestion and pipeline orchestration    |
| Azure Data Lake Storage Gen2 | Cloud data lake storage                      |
| Azure Databricks             | Data processing and transformation           |
| PySpark                      | Large-scale data transformation              |
| Delta Lake                   | Reliable and optimized data storage          |
| Power BI                     | Data visualization and business intelligence |
| DAX                          | KPI and analytical measure development       |
| DAX Studio                   | Query performance and aggregation validation |

---

## 🗂️ Data Architecture

The project follows the **Medallion Architecture**.

### 🥉 Bronze Layer — Raw Data

The Bronze layer stores the original source data with minimal transformation.

Source files include:

* `transactions_data.csv`
* `cards_data.csv`
* `users_data.csv`
* `mcc_codes.json`

The objective of this layer is to preserve the original source data and provide a reliable foundation for downstream processing.

---

### 🥈 Silver Layer — Cleaned & Standardized Data

The Silver layer applies data cleaning, validation, and standardization.

Key transformations include:

* Handling invalid and inconsistent records.
* Standardizing transaction data types.
* Standardizing geographic information.
* Separating merchant geography into:

  * Merchant Country
  * Merchant State
  * Merchant City
* Handling online transactions where geographic information is unavailable.
* Preparing cleaned datasets for analytical modeling.

---

### 🥇 Gold Layer — Analytics-Ready Data

The Gold layer contains the dimensional model used for reporting and analytics.

### Fact Table

* `fact_transactions`

### Dimension Tables

* `dim_users`
* `dim_cards`
* `dim_date`
* `dim_mcc`

The model follows a dimensional approach optimized for analytical workloads.

---

## 📊 Aggregation Layer

An aggregation table was created to improve analytical query performance:

```text
agg_transaction_daily
```

The aggregation table includes:

* Date
* Merchant Category
* Merchant Country
* Transaction Type
* Total Transaction Amount
* Transaction Count

This layer reduces the need to query the detailed transaction fact table for common analytical queries.

---

## ⚡ Power BI Composite Model

The Power BI semantic model uses a combination of storage modes.

| Table                   | Storage Mode |
| ----------------------- | ------------ |
| `fact_transactions`     | DirectQuery  |
| `agg_transaction_daily` | Import       |
| `dim_date`              | Dual         |
| `dim_mcc`               | Dual         |
| `dim_users`             | Dual         | 
| `dim_cards`             | Dual         |

Aggregations were configured to allow Power BI to automatically query the imported aggregation table when the query grain was compatible.

The aggregation behavior was validated using **DAX Studio**.

---

## 🧪 Aggregation Testing

The Composite Model was tested to validate that Power BI queries were routed to the aggregation table instead of the detailed transaction fact table when applicable.

Successful tests included:

* Monthly Transaction Performance
* Merchant Category Performance

The tests confirmed that Power BI successfully used:

```text
agg_transaction_daily
```

instead of:

```text
fact_transactions
```

for compatible analytical queries.

---

## 📈 Dashboards

The Power BI report includes three main analytical dashboards.

### 1️⃣ Transaction Overview

Provides an executive overview of transaction performance.

Key areas include:

* Total transaction volume
* Total transaction value
* Average transaction amount
* Transaction trends
* Transaction activity analysis
* Key transaction performance indicators

---

### 2️⃣ Customer & Card Analytics

Focuses on customer behavior and card performance.

Key areas include:

* Customer transaction behavior
* Customer activity analysis
* Customer segmentation
* Credit score analysis
* Card performance
* Customer spending patterns

---

### 3️⃣ Merchant & Geographic Analytics

Analyzes merchant activity and geographic transaction performance.

Key areas include:

* Merchant activity
* Merchant category performance
* Geographic transaction analysis
* Country-level performance
* Online transaction activity
* Merchant activity trends

---

## 📊 Key KPIs

The project includes several analytical KPIs, including:

* Total Transactions
* Total Transaction Value
* Average Transaction Amount
* Active Customers
* Average Spending per Customer
* Customer Activity Rate
* Total Merchants
* Total Merchant Categories
* Total Countries
* Online Transaction Percentage

---

## 🚀 Performance Optimization

The following techniques were used to improve analytical performance:

* Medallion Architecture
* Delta Lake storage
* Dimensional data modeling
* Aggregation tables
* Power BI Composite Model
* Import and DirectQuery storage modes
* Dual storage mode for shared dimensions
* Query validation using DAX Studio

---

## 📁 Repository Structure

```text
banking-data-engineering-analytics/
│
├── notebooks/
│   ├── bronze/
│   ├── silver/
│   └── gold/
│
├── pipelines/
│   └── azure-data-factory/
│
├── powerbi/
│   └── banking-dashboard.pbix
│
├── images/
│   ├── architecture/
│   ├── data-model/
│   └── dashboards/
│
└── README.md
```

---

## 💡 Key Learnings

This project provided hands-on experience with:

* Building end-to-end cloud data pipelines
* Designing a Medallion Architecture
* Processing large-scale transaction data using PySpark
* Implementing dimensional data models
* Designing aggregation tables
* Optimizing analytical queries
* Building Power BI Composite Models
* Validating aggregation behavior using DAX Studio
* Developing business-focused analytical dashboards

---

## 🔮 Future Improvements

Potential future improvements include:

* Incremental data loading
* Automated data quality checks
* Pipeline monitoring and alerting
* CI/CD for Databricks notebooks and Azure Data Factory pipelines
* Row-Level Security in Power BI
* Advanced customer segmentation
* Predictive analytics
