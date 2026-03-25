# Databricks Lakehouse Project

Welcome to the **Databricks Lakehouse Project** repository! 🚀  
This project demonstrates an end-to-end modern data engineering workflow using **Databricks**, **PySpark**, **Delta Lake**, and the **Medallion Architecture** (**Bronze**, **Silver**, and **Gold** layers).

The goal of this project is to ingest raw data from **CRM** and **ERP** CSV source files, transform it into clean analytical datasets, and model it into a **Sales Data Mart** using a **Star Schema** for reporting and analytics.

---

## 🏗️ Data Architecture

The data architecture for this project follows the **Medallion Architecture** using **Bronze**, **Silver**, and **Gold** layers:

![Lakehouse Architecture](docs/diagram1.png)

1. **Bronze Layer**  
   Stores raw data as-is from the source systems with minimal transformation.  
   CSV files from **CRM** and **ERP** are ingested into **Bronze Delta tables**.

2. **Silver Layer**  
   Applies data cleansing, standardization, null handling, date formatting, column renaming, and duplicate checks.  
   This layer prepares clean and trusted data for downstream modeling.

3. **Gold Layer**  
   Builds business-ready analytical tables in the form of:
   - `gold.dim_customers`
   - `gold.dim_products`
   - `gold.fact_sales`

   These tables are optimized for reporting, analytics, and dashboarding.

---

## 📖 Project Overview

This project includes:

1. **Lakehouse Design**  
   Building a modern Lakehouse solution in Databricks using **Bronze**, **Silver**, and **Gold** layers.

2. **Batch Ingestion**  
   Loading CRM and ERP **CSV source files** into the Bronze layer using **Databricks notebooks** and **PySpark**.

3. **Data Cleaning & Transformation**  
   Cleaning and standardizing source data in the Silver layer through dedicated transformation notebooks.

4. **Data Modeling**  
   Creating a **Sales Data Mart** in the Gold layer using a **Star Schema** with fact and dimension tables.

5. **Orchestration**  
   Running Bronze, Silver, and Gold workflows through orchestration notebooks using:
   - `dbutils.notebook.run(...)`

6. **Analytics & Reporting**  
   Preparing the final Gold tables for analytics and visualization tools such as **Power BI**.

🎯 This repository is a strong portfolio project for showcasing skills in:

- Databricks
- PySpark
- Delta Lake
- Data Engineering
- ETL / ELT Pipelines
- Data Modeling
- Lakehouse Architecture
- Orchestration
- Business Analytics

---

## 🛠️ Tools & Technologies

This project uses:

- **Databricks**
- **PySpark**
- **Delta Lake**
- **Unity Catalog**
- **SQL**
- **Power BI**
- **GitHub**
- **Excalidraw / Draw.io** for architecture and schema diagrams

---

## 🚀 Project Requirements

### Objective

Develop a modern Lakehouse pipeline that consolidates data from multiple source systems and transforms it into analytics-ready business tables.

### Specifications

- **Data Sources**: Import data from two source systems:
  - **CRM**
  - **ERP**
- **File Format**: CSV files
- **Ingestion Method**: Batch ingestion using Databricks notebooks and PySpark
- **Data Quality**: Clean and resolve issues such as:
  - null values
  - invalid dates
  - inconsistent keys
  - duplicate records
- **Integration**: Combine CRM and ERP data into a unified analytical model
- **Modeling**: Build a Star Schema for sales analytics
- **Documentation**: Provide architecture, orchestration, and schema documentation

---

## 📂 Source Datasets

### CRM Source Files
- `cust_info.csv`
- `prd_info.csv`
- `sales_details.csv`

### ERP Source Files
- `CUST_AZ12.csv`
- `LOC_A101.csv`
- `PX_CAT_G1V2.csv`

---

## 🥉 Bronze Layer

The Bronze layer stores the raw ingested data from the source files without applying major transformations.

### Bronze Tables
- `workspace.bronze.crm_cust_info`
- `workspace.bronze.crm_prd_info`
- `workspace.bronze.crm_sales_details`
- `workspace.bronze.erp_cust_az12`
- `workspace.bronze.erp_loc_a101`
- `workspace.bronze.erp_px_cat_g1v2`

---

## 🥈 Silver Layer

The Silver layer applies cleaning and transformation logic to each dataset.

### Silver Transformations Include
- Trimming string columns
- Cleaning and converting date columns
- Standardizing IDs and join keys
- Handling null values
- Replacing invalid values
- Fixing inconsistent business values
- Deduplication checks
- Renaming columns to business-friendly names
- Saving cleaned data as Delta tables

### Silver Tables
- `workspace.silver.crm_customers`
- `workspace.silver.crm_products`
- `workspace.silver.crm_sales`
- `workspace.silver.erp_customers`
- `workspace.silver.erp_customer_location`
- `workspace.silver.erp_product_category`

---

## 🥇 Gold Layer

The Gold layer contains business-ready analytical tables.

### Gold Tables
- `workspace.gold.dim_customers`
- `workspace.gold.dim_products`
- `workspace.gold.fact_sales`

### Gold Data Model
- **`dim_customers`** combines customer details from CRM and ERP
- **`dim_products`** combines product and category details
- **`fact_sales`** stores the core sales transactions and measurable business values

---

## ⭐ Sales Data Mart (Star Schema)

The final analytical model is built as a **Star Schema**:

![Sales Star Schema](docs/sales_star_schema.png)

### Fact Table
- **`gold.fact_sales`**
  - `order_number`
  - `product_key`
  - `customer_key`
  - `order_date`
  - `ship_date`
  - `due_date`
  - `sales_amount`
  - `quantity`
  - `price`

### Dimension Tables
- **`gold.dim_customers`**
- **`gold.dim_products`**

This schema supports business analysis such as:
- sales by customer
- sales by product
- sales by category
- sales trends over time

---

## 🔄 Orchestration Flow

The project includes orchestration notebooks to execute each layer in sequence:

![Orchestration Flow](docs/orchestration.png)

### Orchestration Notebooks
- `bronze_layer`
- `silver_orchestration`
- `gold_orchestration`

These notebooks use `dbutils.notebook.run(...)` to execute the pipeline in order.

---

## 📂 Repository Structure

```text
databricks_datalakehouse_project/
│
├── data_sets/
│   ├── source_crm/
│   │   ├── cust_info.csv
│   │   ├── prd_info.csv
│   │   └── sales_details.csv
│   │
│   └── source_erp/
│       ├── CUST_AZ12.csv
│       ├── LOC_A101.csv
│       └── PX_CAT_G1V2.csv
│
├── docs/
│   ├── lakehouse_architecture.png
│   ├── star_schema.png
│   └── orchestration_flow.png
│
├── scripts/
│   ├── bronze_layer/
│   │   └── bronze_layer.ipynb
│   │
│   ├── silver_layer/
│   │   ├── silver_crm_cust_info.ipynb
│   │   ├── silver_crm_prd_info.ipynb
│   │   ├── silver_crm_sales_details.ipynb
│   │   ├── silver_erp_cust_az12.ipynb
│   │   ├── silver_erp_loc_a101.ipynb
│   │   ├── silver_erp_px_cat_g1v2.ipynb
│   │   └── silver_orchestration.ipynb
│   │
│   └── gold_layer/
│       ├── gold_dim_customers.ipynb
│       ├── gold_dim_products.ipynb
│       ├── gold_fact_sales.ipynb
│       └── gold_orchestration.ipynb
│       
│
└── README.md

```

---
## 🌟 About Me

Hi there! I'm **Gehad Hany Elsayed**, a Computer and Data Science graduate from Alexandria University.  
I’m passionate about **Data Engineering**, **ETL pipelines**, and **modern data solutions**.  
I enjoy designing data architectures, building scalable pipelines, and transforming raw data into actionable insights.  

Let’s connect and share ideas!  

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/gehad-hani-36602a261)  

