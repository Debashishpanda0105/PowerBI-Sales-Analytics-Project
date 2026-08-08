# 📐 DAX Documentation

## Power BI Sales Analytics & Business Intelligence Project

---

# 1. Document Overview

This document defines the DAX calculation framework used in the Power BI Sales Analytics & Business Intelligence Project.

The DAX layer converts the business logic identified during the SQL Exploratory Data Analysis phase into reusable Power BI measures.

The objective is to create a scalable, maintainable, and business-oriented semantic layer rather than creating calculations directly inside individual visuals.

---

# 2. DAX Objectives

The DAX layer is designed to:

- Create reusable business measures
- Standardize KPI calculations
- Implement time intelligence
- Support dynamic dashboard filtering
- Calculate customer and product performance
- Implement ranking analysis
- Implement contribution analysis
- Support customer and product segmentation
- Calculate growth metrics
- Support drill-through analysis
- Maintain a clean semantic model
- Reduce duplicated calculations

---

# 3. DAX Development Principles

The following principles will be followed:

- Prefer measures over calculated columns for aggregations
- Reuse existing measures whenever possible
- Avoid repeating business logic
- Use descriptive measure names
- Organize measures into logical display folders
- Use variables for complex calculations
- Keep filter context in mind
- Use the Date Dimension for time intelligence
- Avoid unnecessary calculated tables
- Validate important measures against SQL results

---

# 4. DAX Measure Architecture

The DAX layer will follow the following structure:

```text
                    DAX MEASURE LAYER
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
        ▼                  ▼                  ▼
   Base Measures      Time Intelligence   Analytical Measures
        │                  │                  │
        ▼                  ▼                  ▼
    Sales KPIs       YoY / MoM / YTD    Ranking / Contribution
        │                  │                  │
        └──────────────────┼──────────────────┘
                           │
                           ▼
                  Business Segmentation
                           │
                           ▼
                    Dashboard KPIs

```

---
## 5. Measure Naming Convention

Measures should follow a consistent naming standard.

Recommended Format
```[Business Area] [Metric]```

Examples:
```
Sales Total
Sales LY
Sales YoY
Sales YoY %
Orders Total
Customers Total
Products Total
Quantity Total
AOV
```
For more complex measures:
```
Customer Revenue
Customer Revenue %
Product Revenue
Product Revenue %
Category Revenue
Category Revenue %
```

---

## 6. Measure Display Folders

Measures should be organized into logical display folders.

-Recommended structure:
```
Measures
│
├── 01 Base KPIs
│
├── 02 Sales Metrics
│
├── 03 Customer Metrics
│
├── 04 Product Metrics
│
├── 05 Time Intelligence
│
├── 06 Growth Analysis
│
├── 07 Ranking
│
├── 08 Contribution Analysis
│
├── 09 Segmentation
│
└── 10 Dynamic Measures

```
---

## 7. Base KPI Measures
Total Sales

```
Sales Total =
SUM ( fact_sales[sales_amount] )
```
Purpose:

Calculates total business revenue.

Like that all calculate

---

## 8. Sales Metrics

```
-Average Selling Price

Average Selling Price =
AVERAGE ( fact_sales[price] )
Average Quantity per Order
Average Quantity per Order =
DIVIDE (
    [Quantity Total],
    [Orders Total]
)

-Average Order Value

AOV =
DIVIDE (
    [Sales Total],
    [Orders Total]
)

AOV = Average Order Value.

- Average Revenue per Customer

Revenue per Customer =
DIVIDE (
    [Sales Total],
    [Customers Active]
)
```
---

## 9. Minimum and Maximum Analysis

- Minimum Sales Amount
```
Sales Minimum =
MIN ( fact_sales[sales_amount] )
```
-Maximum Sales Amount
```
Sales Maximum =
MAX ( fact_sales[sales_amount] )
```
---

## 10. Time Intelligence

Time intelligence measures should use the dedicated Date Dimension.

The Date Dimension should have:

- Date
- Year
- Quarter
- Month
- Month Number
- Year-Month

The Date table should be marked as the official Date Table in Power BI.

---

## 11. Measure Dependency Architecture

Measures should be built in layers.

```
FACT COLUMNS
     │
     ▼
BASE MEASURES
     │
     ├──────────────┐
     ▼              ▼
SALES KPIs     CUSTOMER KPIs
     │
     ▼
TIME INTELLIGENCE
     │
     ▼
GROWTH ANALYSIS
     │
     ▼
RANKING / CONTRIBUTION
     │
     ▼
SEGMENTATION
     │
     ▼
DASHBOARD KPIs

```

This prevents unnecessary duplication of business logic.

---

## 12. DAX Performance Guidelines

The following practices should be followed:

- Prefer measures over unnecessary calculated columns
- Reuse existing measures
- Avoid excessive iterator functions
- Use variables for complex expressions
- Avoid unnecessary FILTER() operations
- Avoid using ALL() when ALLSELECTED() is more appropriate
- Keep the data model optimized
- Use a proper Star Schema
- Remove unused columns
- Avoid unnecessary calculated tables

---

## 13. Final DAX Architecture

The final DAX layer should follow:
```

                DATA MODEL
                    │
                    ▼
             BASE MEASURES
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
      SALES     CUSTOMERS    PRODUCTS
        │           │           │
        └───────────┼───────────┘
                    ▼
           TIME INTELLIGENCE
                    │
                    ▼
             GROWTH ANALYSIS
                    │
                    ▼
        ┌───────────┼───────────┐
        ▼           ▼           ▼
     RANKING   CONTRIBUTION  SEGMENTATION
        │           │           │
        └───────────┼───────────┘
                    ▼
             DYNAMIC KPIs
                    │
                    ▼
             POWER BI REPORT
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
      SALES      CUSTOMER     PRODUCT
      DASHBOARD  DASHBOARD    DASHBOARD

```
---

## 52. Final Objective

The purpose of the DAX layer is not simply to create calculations.

The objective is to build a reusable semantic layer that allows Power BI users to interact with the business 
data dynamically while maintaining consistent business definitions.

The final solution should allow users to:

- Analyze sales
- Analyze customers
- Analyze products
- Compare periods
- Identify trends
- Rank entities
- Measure contribution
- Segment business entities
- Drill into details
- Interactively filter the report
- Generate actionable business insights

---
