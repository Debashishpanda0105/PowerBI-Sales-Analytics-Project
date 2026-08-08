# 📊 Dashboard Design Document

## Power BI Sales Analytics & Business Intelligence Project

---

# 1. Document Overview

This document defines the design, layout, navigation, visuals, interactions, and business purpose of the Power BI dashboards developed for the **Power BI Sales Analytics & Business Intelligence Project**.

The dashboard design is based on the SQL Server Data Warehouse Gold Layer and the analytical findings generated through the SQL Exploratory Data Analysis project.

The objective is to create a **dynamic, interactive, business-focused Power BI reporting solution** rather than a collection of disconnected charts.

---

# 2. Dashboard Objectives

The Power BI report is designed to help business users:

- Monitor overall business performance
- Analyze sales trends
- Understand customer behavior
- Evaluate product performance
- Identify high-value customers
- Identify underperforming products
- Compare performance across countries and categories
- Analyze historical trends
- Drill from summary-level information into detailed analysis
- Make data-driven business decisions

---

# 3. Dashboard Architecture

The report will contain four primary analytical pages.

```text
                    ┌──────────────────────┐
                    │   EXECUTIVE OVERVIEW  │
                    │       🏠 HOME         │
                    └──────────┬───────────┘
                               │
              ┌────────────────┼────────────────┐
              │                │                │
              ▼                ▼                ▼
       ┌─────────────┐  ┌─────────────┐  ┌─────────────┐
       │    SALES    │  │  CUSTOMER   │  │   PRODUCT   │
       │  ANALYSIS   │  │  ANALYSIS   │  │  ANALYSIS   │
       └─────────────┘  └─────────────┘  └─────────────┘
              │                │                │
              └────────────────┼────────────────┘
                               │
                               ▼
                       DRILL-THROUGH
                               │
                  ┌────────────┴────────────┐
                  ▼                         ▼
           CUSTOMER DETAIL           PRODUCT DETAIL

```
Users should be able to move between pages using Power BI Page Navigation buttons.
---

## 5. Global Design Principles

The report should follow these design principles:

- Clean layout
- Consistent spacing
- Consistent typography
- Limited visual clutter
- Business-focused KPIs
- Clear visual hierarchy
- Consistent number formatting
- Consistent navigation
- Interactive filtering
- Meaningful use of color
- Minimal unnecessary decoration

The report should prioritize clarity and usability over excessive visual effects.

---

## 6. Executive Dashboard

Page Purpose

The Executive Dashboard is the main landing page of the report.

It provides management with a quick overview of overall business performance.

## 6.1 KPI Section

The top section should contain key business KPIs.

-KPI Cards

```text
┌──────────────┐ ┌──────────────┐ ┌──────────────┐
│ Total Sales  │ │ Total Orders │ │  Customers   │
│              │ │              │ │              │
└──────────────┘ └──────────────┘ └──────────────┘

┌──────────────┐ ┌──────────────┐ ┌──────────────┐
│  Products    │ │ Total Qty    │ │ Avg Order    │
│              │ │              │ │    Value     │
└──────────────┘ └──────────────┘ └──────────────┘

```
Required KPIs
- Total Sales
- Total Orders
- Total Customers
- Total Products
- Total Quantity
- Average Order Value

---

## 7. Executive Dashboard — Visuals

# Visual 1 — Sales Trend

Chart: Line Chart

Axis:

```Date / Month```

Value:
```
Total Sales
```
Purpose:

Identify overall revenue trends over time.

# Visual 2 — Sales by Category

Chart: Bar Chart

```Category → Total Sales```

Purpose:

Identify the categories contributing the most revenue.

# Visual 3 — Sales by Country

Chart: Bar / Map where appropriate

``` Country → Total Sales```

Purpose:

Understand geographic sales performance.

## Visual 4 — Top 5 Products

Chart: Horizontal Bar Chart

```Product → Total Sales```

- Filter:

Top 5

Purpose:

Identify the highest revenue-generating products.

## Visual 5 — Top 5 Customers

Chart: Horizontal Bar Chart

```Customer → Total Sales```

Filter:

```Top 5```

Purpose:

Identify customers contributing the most revenue.


---

## 8. KPI Design

KPIs should communicate:

- Current value
- Business context
- Trend where useful
Example:
```
┌───────────────────────────┐
│       TOTAL SALES        │
│                           │
│       $XX.XXM             │
│                           │
│       ▲ 12.4% YoY         │
└───────────────────────────┘
```
here valid, KPI cards should include comparison metrics such as:

- YoY %
- MoM %
- Previous Period
- Target Variance

----

## 9. Visual Hierarchy

Each page should follow a consistent structure.
```
┌─────────────────────────────────────────────┐
│              PAGE TITLE / NAVIGATION        │
├─────────────────────────────────────────────┤
│ KPI │ KPI │ KPI │ KPI │ KPI │ KPI           │
├─────────────────────────────────────────────┤
│                                             │
│              PRIMARY ANALYSIS               │
│                                             │
├──────────────────────┬──────────────────────┤
│                      │                      │
│   SECONDARY VISUAL   │   SECONDARY VISUAL   │
│                      │                      │
├──────────────────────┴──────────────────────┤
│             SUPPORTING ANALYSIS              │
└─────────────────────────────────────────────┘
```

---

## 10. Executive User Journey

The intended user journey is:
```
OPEN REPORT
     │
     ▼
EXECUTIVE OVERVIEW
     │
     ├──────────────┐
     ▼              ▼
SALES ANALYSIS   CUSTOMER ANALYSIS
     │              │
     │              ▼
     │       CUSTOMER DETAILS
     │
     ▼
PRODUCT ANALYSIS
     │
     ▼
PRODUCT DETAILS
     │
     ▼
BUSINESS INSIGHTS
```

----

## 11. Dashboard-to-Business Mapping

```
| Dashboard       | Primary Business Need            |
| --------------- | -------------------------------- |
| Executive       | Overall business health          |
| Sales           | Revenue and sales performance    |
| Customer        | Customer behavior and value      |
| Product         | Product and category performance |
| Customer Detail | Individual customer analysis     |
| Product Detail  | Individual product analysis      |
```
---

## 12. Final Dashboard Layout
```
                  POWER BI SALES ANALYTICS

                         🏠 EXECUTIVE
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼
    📈 SALES              👥 CUSTOMER           📦 PRODUCT
        │                     │                     │
        │                     │                     │
        └─────────────────────┼─────────────────────┘
                              │
                              ▼
                       🔍 DRILL-THROUGH
                              │
                    ┌─────────┴─────────┐
                    ▼                   ▼
              CUSTOMER DETAIL     PRODUCT DETAIL

```

---
## 13. Development Order

The dashboards should be developed in the following sequence:

```
1. Data Model
       ↓
2. Power Query Validation
       ↓
3. Date Dimension
       ↓
4. Base DAX Measures
       ↓
5. Sales Measures
       ↓
6. Customer Measures
       ↓
7. Product Measures
       ↓
8. Executive Dashboard
       ↓
9. Sales Dashboard
       ↓
10. Customer Dashboard
       ↓
11. Product Dashboard
       ↓
12. Drill-Through
       ↓
13. Tooltips
       ↓
14. Navigation
       ↓
15. RLS
       ↓
16. Validation
       ↓
17. Final Documentation

```

---

## 14. Final Dashboard Objective

The objective of the dashboard design is to create a single, connected, dynamic Business Intelligence 
solution rather than multiple disconnected dashboards.

The final experience should allow users to move from:

```
HIGH-LEVEL BUSINESS PERFORMANCE
              ↓
       SALES ANALYSIS
              ↓
      CUSTOMER ANALYSIS
              ↓
       PRODUCT ANALYSIS
              ↓
       DETAILED ANALYSIS
              ↓
      BUSINESS INSIGHTS
```

## What is happening?

Understand current business performance.

## Why is it happening?

Analyze customers, products, categories, geography, and time.

## What should the business focus on?

Identify high-value opportunities, risks, trends, and underperforming areas.

---

## 15. Final Design Principle

```The dashboard is not the product. The business insight is the product.```

Power BI visuals, DAX measures, navigation, and interactions should all work together to make business 
decision-making faster, clearer, and more reliable.

---
