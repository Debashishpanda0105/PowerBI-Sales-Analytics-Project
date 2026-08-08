# 📐 Data Model Documentation

## Power BI Sales Analytics & Business Intelligence Project

---

# 1. Document Overview

This document describes the data model used in the **Power BI Sales Analytics & Business Intelligence Project**.

The Power BI semantic model is built on top of the curated **Gold Layer** of the SQL Server Data Warehouse.

The model follows a **Star Schema** architecture to provide:

- Simple relationships
- Efficient filtering
- Reusable DAX measures
- Better report performance
- Consistent business logic
- Easy analytical navigation

---

# 2. Data Model Objective

The primary objective of the data model is to create a clean and reliable analytical layer that connects sales transactions with descriptive customer, product, and date information.

The model should allow business users to analyze:

- Sales
- Orders
- Customers
- Products
- Categories
- Geography
- Time
- Quantity
- Revenue

without requiring users to understand the underlying transactional structure.

---

# 3. Data Sources

The Power BI model uses the following sources.

### SQL Server Gold Layer

```text
gold.fact_sales
gold.dim_customers
gold.dim_products
```

---

## Power BI

The Date Dimension is created in Power BI to support time intelligence and standardized date analysis.

----

## 4. Star Schema Architecture

The final model follows a Star Schema.

```text
                       ┌───────────────────┐
                       │   DIM_CUSTOMERS   │
                       │───────────────────│
                       │ PK customer_key   │
                       │ first_name        │
                       │ last_name         │
                       │ gender            │
                       │ country           │
                       │ marital_status    │
                       │ birthdate         │
                       │ create_date       │
                       └─────────┬─────────┘
                                 │
                                 │ 1 : *
                                 │
                                 ▼
                       ┌───────────────────┐
                       │    FACT_SALES     │
                       │───────────────────│
                       │ PK/FK order data  │
                       │ customer_key      │
                       │ product_key       │
                       │ order_date        │
                       │ sales_amount      │
                       │ quantity          │
                       │ price             │
                       └─────────┬─────────┘
                                 │
                 ┌───────────────┴───────────────┐
                 │                               │
                 │ * : 1                         │ * : 1
                 │                               │
                 ▼                               ▼
       ┌───────────────────┐          ┌───────────────────┐
       │   DIM_PRODUCTS    │          │     DIM_DATE      │
       │───────────────────│          │───────────────────│
       │ PK product_key    │          │ PK date           │
       │ product_name      │          │ year              │
       │ category          │          │ quarter           │
       │ sub_category      │          │ month             │
       │ cost              │          │ month_name        │
       │ product_line      │          │ month_number      │
       └───────────────────┘          │ year_month        │
                                      │ week              │
                                      └───────────────────┘

```

## 5. Tables in the Model

The model contains:

```
| Table           | Type      | Source          | Purpose                      |
| --------------- | --------- | --------------- | ---------------------------- |
| `fact_sales`    | Fact      | SQL Server Gold | Stores sales transactions    |
| `dim_customers` | Dimension | SQL Server Gold | Stores customer attributes   |
| `dim_products`  | Dimension | SQL Server Gold | Stores product attributes    |
| `dim_date`      | Dimension | Power BI        | Supports time-based analysis |

```

## 6. Relationships

The model uses one-to-many relationships.

- Customer Relationship
```
dim_customers[customer_key]
          1
          │
          │
          *
fact_sales[customer_key]
```

- Product Relationship
```
dim_products[product_key]
          1
          │
          │
          *
fact_sales[product_key]
```

- Date Relationship
```
dim_date[date]
      1
      │
      │
      *
fact_sales[order_date]
```

---

## 7. Why Star Schema?

A Star Schema was selected because it provides a clean separation between:

- Facts
Business events and numerical measurements.
```fact_sales```

- Dimensions
Descriptive business context.
```
dim_customers
dim_products
dim_date
```
This structure makes the model easier to understand and maintain.

---

## 8. Date Table Configuration

The dim_date table should be configured as the official Date Table in Power BI.


-Requirements
- Date column must contain unique dates
- Date column must not contain blanks
- Date column should cover the required reporting period
- Mark the table as a Date Table
- Use the Date column for time intelligence

---

## 9. Model Naming Standards

The following naming conventions are followed.

- Tables
Use clear business names:
- fact_sales
- dim_customers
- dim_products
- dim_date

- Columns
- Use: snake_case

- Measures
Use readable business names:
```
Total Sales
Total Orders
Total Customers
Average Order Value
YoY Growth %

```
---

## 10. Semantic Layer

The Power BI model acts as the semantic layer between the data warehouse and business users.

```
SQL DATA WAREHOUSE
        │
        ▼
     GOLD LAYER
        │
        ▼
 POWER BI SEMANTIC MODEL
        │
 ┌──────┼──────┐
 ▼      ▼      ▼
Sales Customer Product
Measures Measures Measures
        │
        ▼
    DASHBOARDS

```

Business users interact with the semantic model rather than directly querying the underlying database.

---

## 11. Final Model Architecture

```text
                    POWER BI SEMANTIC MODEL

                         DIM_CUSTOMERS
                              │
                              │ 1
                              ▼
                              *
                         FACT_SALES
                        /          \
                       /            \
                      /              \
                     ▼                ▼
              DIM_PRODUCTS         DIM_DATE
                   1                   1
                   │                   │
                   └─────────┬─────────┘
                             │
                             ▼
                         DAX MEASURES
                             │
                             ▼
                    POWER BI REPORT
                             │
            ┌────────────────┼────────────────┐
            ▼                ▼                ▼
        SALES PAGE      CUSTOMER PAGE    PRODUCT PAGE
            │                │                │
            └────────────────┼────────────────┘
                             ▼
                     EXECUTIVE DASHBOARD
```
----

## 12. Final Design Principles

The final Power BI model follows these principles:

- ⭐ Star Schema
- 🔑 Proper keys
- 🔗 One-to-many relationships
- ➡️ Single-direction filtering
- 📅 Dedicated Date Dimension
- 📊 Reusable DAX Measures
- 🧹 Clean semantic model
- 🚫 Avoid unnecessary many-to-many relationships
- 🚫 Avoid unnecessary calculated columns
- ✅ Data validation against SQL Server
- ⚡ Performance-oriented modeling
- 👨‍💼 Business-friendly naming
- 🔐 Security-ready architecture

---

## 13. Model Validation Checklist

Before moving to dashboard development, verify:

 - Gold Layer tables connected successfully
 - fact_sales loaded correctly
 - dim_customers loaded correctly
 - dim_products loaded correctly
 - dim_date created
 - Date table marked correctly
 - Customer relationship validated
 - Product relationship validated
 - Date relationship validated
 - No ambiguous relationships
 - No unnecessary bidirectional relationships
 - Keys validated
 - Data types validated
 - SQL totals match Power BI totals
 - Model performance checked
 - Technical columns hidden where appropriate

 ---

 ## 14. Final Objective

 The objective of this data model is to provide a clean, scalable, reliable, and business-friendly semantic layer 
 that supports dynamic Sales, Customer, Product, and Executive reporting.

 The model will serve as the foundation for the next stages of the project:
 
```text
DATA MODEL
    ↓
DAX MEASURES
    ↓
DYNAMIC REPORTING
    ↓
BUSINESS INSIGHTS
  
```
A well-designed model is the foundation of a reliable Power BI solution.
---

