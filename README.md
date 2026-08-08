# 📊 Power BI Sales Analytics & Business Intelligence Project

An end-to-end **Power BI Sales Analytics and Business Intelligence project** built on top of a professionally designed SQL Server Data Warehouse.

This project transforms the curated **Gold Layer** of the Data Warehouse into a dynamic and interactive Power BI analytical solution using **Power Query, Star Schema Data Modeling, DAX, Time Intelligence, Row-Level Security, and Business Intelligence reporting**.

---

## 🚀 Project Overview

This project is the **Power BI analytics layer** of my end-to-end data analytics solution.

The project builds upon the previously developed:

1. **SQL Data Warehouse**
2. **SQL Exploratory Data Analysis & Business Insights**

The objective is to transform SQL-based analysis into a **dynamic Power BI reporting solution** that allows business users to interactively analyze:

- Sales Performance
- Customer Behavior
- Product Performance
- Revenue Trends
- Business KPIs

---

# 🔗 Project Ecosystem

This project is part of an end-to-end analytics workflow.

```text
SQL DATA WAREHOUSE
        │
        ▼
    GOLD LAYER
        │
        ▼
SQL EXPLORATORY DATA ANALYSIS
        │
        ▼
   BUSINESS INSIGHTS
        │
        ▼
     POWER BI
        │
        ▼
   DATA MODEL
        │
        ▼
      DAX
        │
        ▼
 DYNAMIC DASHBOARDS
        │
        ▼
 BUSINESS DECISIONS
```

---

# 🔗 Related Projects

### 🗄️ SQL Data Warehouse Project

The foundation of this project is the SQL Server Data Warehouse built using the **Bronze → Silver → Gold Medallion Architecture**.

### 🔎 SQL Exploratory Data Analysis Project

The Gold Layer was analyzed using SQL to perform:

- Database Exploration
- Dimension Exploration
- Date Exploration
- Measure Exploration
- Magnitude Analysis
- Ranking Analysis
- Change-Over-Time Analysis
- Cumulative Analysis
- Performance Analysis
- Part-to-Whole Analysis
- Data Segmentation
- Reporting

The Power BI project converts these analytical findings into an interactive BI solution.

---

# 🎯 Project Objectives

The main objectives are:

- Build a professional Power BI semantic model
- Use the SQL Data Warehouse Gold Layer as the data source
- Implement a clean Star Schema
- Create a dedicated Date Dimension
- Establish proper table relationships
- Develop reusable DAX measures
- Implement time intelligence
- Build dynamic dashboards
- Analyze sales performance
- Analyze customer behavior
- Analyze product performance
- Implement interactive filtering
- Implement drill-through analysis
- Implement Row-Level Security
- Validate Power BI results against SQL Server
- Generate actionable business insights

---

# 🗄️ Data Source

The project uses the curated **Gold Layer** from the SQL Server Data Warehouse.

### Fact Table

```text
gold.fact_sales
```

Contains transactional sales information.

### Dimension Tables

```text
gold.dim_customers
gold.dim_products
```

Contain descriptive customer and product information.

### Power BI Date Dimension

```text
dim_date
```

A dedicated Date Dimension is created in Power BI to support time-based analysis and time intelligence.

---

# ⭐ Data Model

The Power BI model follows a **Star Schema** architecture.

```text
                    DIM_CUSTOMERS
                         │
                         │ 1
                         │
                         ▼ *
                    FACT_SALES
                    ▲       ▲
                    │       │
                  * │       │ *
                    │       │
                    │       │
              DIM_DATE   DIM_PRODUCTS
                  1           1
```

### Model Components

### Fact

- `fact_sales`

### Dimensions

- `dim_customers`
- `dim_products`
- `dim_date`

---

# 📐 Data Modeling Standards

The following industry-oriented modeling principles are followed:

- ⭐ Star Schema
- 🔗 One-to-Many Relationships
- ➡️ Single-Direction Filtering
- 🔑 Integer/Surogate Keys
- 📅 Dedicated Date Dimension
- 🚫 Avoid unnecessary Many-to-Many relationships
- 🧹 Remove unnecessary columns
- 🏷️ Consistent naming conventions
- 📊 Prefer measures over unnecessary calculated columns
- ✅ Validate relationships
- ✅ Validate totals against SQL

---

# 🔄 Power Query

Power Query is used for data preparation, transformation, and validation.

### Activities

- Connect to SQL Server
- Load Gold Layer tables
- Validate data types
- Rename columns where required
- Remove unnecessary columns
- Check null values
- Check duplicate keys
- Validate relationships
- Create Date Dimension
- Prepare analytical-ready tables

---

# 📅 Date Dimension

A dedicated Date Dimension is created for time-based analysis.

### Date Attributes

- Date
- Year
- Quarter
- Month
- Month Number
- Month Name
- Year-Month
- Week
- Day

### Enables

- Yearly Analysis
- Quarterly Analysis
- Monthly Analysis
- YoY Analysis
- MoM Analysis
- Running Total
- Time Intelligence

---

# 📊 DAX Measures

Reusable DAX measures are created for dynamic business analysis.

## Sales Measures

- Total Sales
- Total Quantity
- Total Orders
- Average Order Value
- Average Selling Price

## Customer Measures

- Total Customers
- Active Customers
- Customers with Orders
- Average Revenue per Customer

## Product Measures

- Total Products
- Products Sold
- Product Revenue
- Top Product
- Bottom Product

## Time Intelligence

- Current Year Sales
- Previous Year Sales
- YoY Growth
- YoY Growth %
- Current Month Sales
- Previous Month Sales
- Running Total

---

# 📈 Dashboard Structure

The project contains **4 connected analytical pages**.

```text
                 🏠 EXECUTIVE
                    DASHBOARD
                       │
          ┌────────────┼────────────┐
          │            │            │
          ▼            ▼            ▼
       📈 SALES     👥 CUSTOMER   📦 PRODUCT
       ANALYSIS      ANALYSIS      ANALYSIS
          │            │            │
          └────────────┼────────────┘
                       │
                 🔍 DRILL-THROUGH
                       │
             ┌─────────┴─────────┐
             ▼                   ▼
       Customer Detail     Product Detail
```

---

# 🏠 1. Executive Dashboard

The Executive Dashboard acts as the main landing page.

## Key KPIs

- Total Revenue
- Total Orders
- Total Customers
- Total Products
- Total Quantity
- Average Order Value

## Analysis

- Revenue Trend
- Revenue by Category
- Revenue by Country
- Top 5 Products
- Top 5 Customers

## Navigation

Users can navigate to:

- Sales Analysis
- Customer Analysis
- Product Analysis

---

# 📈 2. Sales Dashboard

The Sales Dashboard focuses on overall sales performance.

### Analysis

- Monthly Sales
- Yearly Sales
- Revenue Trend
- YoY Growth
- Running Total
- Sales by Category
- Sales by Country
- Quantity Trend
- Top/Bottom Categories

### Filters

- Date
- Year
- Country
- Category

---

# 👥 3. Customer Dashboard

The Customer Dashboard analyzes customer behavior and contribution.

### KPIs

- Total Customers
- Active Customers
- Average Revenue per Customer
- Average Orders per Customer

### Analysis

- Revenue by Customer
- Top 10 Customers
- Customers by Country
- Customer Segmentation
- Customer Revenue Distribution
- Purchase Frequency

### Filters

- Country
- Gender
- Marital Status
- Date

---

# 📦 4. Product Dashboard

The Product Dashboard focuses on product performance.

### KPIs

- Total Products
- Products Sold
- Total Quantity
- Average Product Revenue

### Analysis

- Revenue by Product
- Top 10 Products
- Bottom 10 Products
- Revenue by Category
- Quantity by Category
- Product Segmentation

### Filters

- Category
- Sub-Category
- Product
- Date

---

# 🔄 Dynamic Dashboard Experience

The dashboards are designed as a connected analytical experience rather than independent reports.

### Common Filtering

Slicers can be synchronized across pages where appropriate.

Example:

```text
Year = 2023
Country = United States
Category = Bikes
```

The selected filters dynamically affect the relevant Sales, Customer, and Product analysis.

---

# 🔍 Drill-Through Analysis

Drill-through functionality is used to allow users to move from high-level analysis to detailed information.

### Example

```text
Sales Dashboard
       │
       ▼
Select Product
       │
       ▼
Product Detail
```

Similarly:

```text
Customer Dashboard
       │
       ▼
Select Customer
       │
       ▼
Customer Detail
```

---

# 🔐 Row-Level Security

Row-Level Security is implemented where required to control access to business data.

Conceptually:

```text
User
  │
  ▼
Security Mapping
  │
  ▼
Business Filter
  │
  ▼
Power BI Report
```

The objective is to ensure that users only see the data they are authorized to access.

---

# ✅ Data Validation

Power BI results are validated against SQL Server results.

### Validation Metrics

- Total Sales
- Total Orders
- Total Quantity
- Total Customers
- Total Products
- Revenue by Category
- Revenue by Country
- Revenue by Product

The validation principle is:

```text
SQL Server Result
       =
Power BI Result
```

This ensures data accuracy and model reliability.

---

# 💼 Business Questions

The Power BI solution helps answer important business questions.

### Sales

- How much revenue is being generated?
- How are sales changing over time?
- Which year generated the highest revenue?
- Which category contributes the most revenue?
- Which country generates the highest sales?

### Customers

- Who are the highest-value customers?
- Which customers contribute the most revenue?
- Which countries have the highest customer contribution?
- Which customer segments are most valuable?

### Products

- Which products generate the most revenue?
- Which products sell the highest quantity?
- Which products are underperforming?
- Which categories perform best?

---

# 🛠️ Technologies Used

- Microsoft Power BI
- Power Query
- DAX
- SQL Server
- SQL Server Management Studio
- Data Modeling
- Star Schema
- Time Intelligence
- Row-Level Security
- Git
- GitHub

---

# 📁 Project Structure

```text
PowerBI-Sales-Analytics-Project
│
├── PowerBI/
│   └── PowerBI_Sales_Analytics.pbix
│
├── Data_Model/
│   ├── data_model.png
│   ├── relationship_documentation.md
│   └── model_standards.md
│
├── Power_Query/
│   ├── transformation_steps.md
│   └── query_documentation.md
│
├── DAX/
│   ├── 01_base_measures.dax
│   ├── 02_sales_measures.dax
│   ├── 03_customer_measures.dax
│   ├── 04_product_measures.dax
│   └── 05_time_intelligence.dax
│
├── RLS/
│   └── rls_documentation.md
│
├── Documentation/
│   ├── Business_Requirements.md
│   ├── Data_Model_Documentation.md
│   ├── Dashboard_Design.md
│   ├── DAX_Documentation.md
│   └── Business_Insights.md
│
├── Screenshots/
│   ├── data_model.png
│   ├── executive_dashboard.png
│   ├── sales_dashboard.png
│   ├── customer_dashboard.png
│   └── product_dashboard.png
│
├── README.md
└── LICENSE
```

---

# 🔄 End-to-End Architecture

```text
                 SQL DATA WAREHOUSE
                         │
                         ▼
                    GOLD LAYER
                         │
             ┌───────────┼───────────┐
             │           │           │
             ▼           ▼           ▼
        FACT_SALES   CUSTOMERS   PRODUCTS
             │           │           │
             └───────────┼───────────┘
                         │
                         ▼
                   POWER QUERY
                         │
                         ▼
                 DATA VALIDATION
                         │
                         ▼
                   STAR SCHEMA
                         │
                         ▼
                    DIM_DATE
                         │
                         ▼
                    DAX LAYER
                         │
                         ▼
                       RLS
                         │
                         ▼
                 POWER BI REPORT
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
        SALES         CUSTOMER       PRODUCT
       ANALYSIS       ANALYSIS       ANALYSIS
          │              │              │
          └──────────────┼──────────────┘
                         ▼
                  BUSINESS INSIGHTS
```

---

# 📊 Project Development Phases

The project will be developed in the following order:

### Phase 1 — Data Connection

Connect Power BI to the SQL Server Gold Layer.

### Phase 2 — Power Query

Validate and prepare the data.

### Phase 3 — Data Modeling

Build the Star Schema and relationships.

### Phase 4 — Date Dimension

Create and configure the Date Dimension.

### Phase 5 — DAX

Create reusable business measures.

### Phase 6 — Dashboard Development

Build the four connected analytical pages.

### Phase 7 — Advanced Features

Implement:

- Drill-through
- Synchronized Slicers
- Tooltips
- RLS

### Phase 8 — Validation

Compare Power BI results with SQL Server.

### Phase 9 — Documentation

Document the model, measures, dashboards, and insights.

---

# 📚 Skills Demonstrated

- Power BI
- Power Query
- DAX
- SQL Server
- Data Modeling
- Star Schema
- Dimensional Modeling
- Time Intelligence
- KPI Development
- Business Intelligence
- Dashboard Development
- Data Validation
- Row-Level Security
- Analytical Thinking
- Business Reporting

---

# 🎯 Business Value

This project transforms SQL-based analytical work into a dynamic Business Intelligence solution.

It enables business users to:

- Monitor KPIs
- Analyze sales trends
- Compare performance
- Understand customer behavior
- Evaluate product performance
- Identify high-value customers
- Identify underperforming products
- Explore business trends interactively
- Support data-driven decision-making

---

# 🚀 Future Enhancements

- Power BI Service Deployment
- Scheduled Data Refresh
- Incremental Refresh
- Deployment Pipelines
- Microsoft Fabric Integration
- RFM Analysis
- Customer Lifetime Value
- Sales Forecasting
- Advanced Customer Segmentation

---

# 👨‍💻 Author

**Debashish Panda**

Data Analyst | SQL Developer | Business Intelligence Enthusiast

### Core Areas

- SQL
- Power BI
- Data Warehousing
- Business Intelligence
- Data Analytics

---

# 📄 License

This project is licensed under the MIT License.

---

## ⭐ If you found this project useful, consider giving it a Star!
