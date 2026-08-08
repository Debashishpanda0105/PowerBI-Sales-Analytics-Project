# 📋 Business Requirements Document

## Power BI Sales Analytics & Business Intelligence Project

---

## 1. Document Overview

### Project Name

**Power BI Sales Analytics & Business Intelligence Project**

### Purpose

The purpose of this project is to develop an interactive Power BI Business Intelligence solution using the curated Gold Layer of a SQL Server Data Warehouse.

The solution will transform transactional sales data into meaningful business insights through a professional data model, reusable analytical measures, interactive dashboards, and business-oriented reporting.

---

# 2. Business Problem

The organization has transactional sales data containing information about:

- Sales transactions
- Customers
- Products
- Product categories
- Customer demographics
- Geographic information
- Order dates
- Sales quantities
- Sales amounts

Although the data is available in the SQL Server Data Warehouse, business users need an interactive reporting solution to easily understand business performance.

The current analytical requirements include:

- Monitoring overall sales performance
- Understanding customer behavior
- Evaluating product performance
- Identifying high-value customers
- Identifying underperforming products
- Analyzing sales trends over time
- Comparing business performance across countries and categories
- Monitoring important business KPIs

Therefore, a centralized Power BI solution is required.

---

# 3. Business Objective

The primary objective is to build a dynamic Power BI reporting solution that enables business users to analyze sales, customers, and products from a single analytical environment.

The solution should allow users to:

- Monitor executive-level KPIs
- Analyze sales performance
- Analyze customer behavior
- Analyze product performance
- Identify business trends
- Compare performance across different dimensions
- Drill from summary information into detailed analysis
- Apply interactive filters
- Support data-driven decision-making

---

# 4. Target Users

The Power BI solution is designed for the following business users:

### Executive Management

Require a high-level overview of business performance.

### Sales Management

Require detailed sales and revenue performance analysis.

### Marketing / Customer Teams

Require customer behavior and customer contribution analysis.

### Product Management

Require product and category performance analysis.

### Business Analysts

Require interactive analytical capabilities for deeper investigation.

### Data Analysts

Require a reliable semantic model and reusable measures for business reporting.

---

# 5. Business Questions

The solution should answer the following key business questions.

## Sales Analysis

- What is the total revenue?
- How many orders have been placed?
- How many products have been sold?
- How is revenue changing over time?
- Which year generated the highest revenue?
- Which month generated the highest sales?
- Which country generates the highest revenue?
- Which product category generates the most revenue?
- How is sales performance changing year over year?

---

## Customer Analysis

- How many customers are present?
- How many customers have placed orders?
- Which customers generate the highest revenue?
- Which countries have the highest number of customers?
- Which customers are high-value customers?
- How frequently do customers purchase?
- Which customer segments contribute the most revenue?

---

## Product Analysis

- How many products are available?
- Which products generate the highest revenue?
- Which products sell the highest quantity?
- Which products are underperforming?
- Which categories perform best?
- Which categories contribute the most revenue?
- Which products should receive additional business attention?

---

# 6. Key Performance Indicators

The Executive Dashboard should provide the following KPIs.

| KPI | Business Purpose |
|---|---|
| Total Sales | Measure overall revenue |
| Total Orders | Measure transaction volume |
| Total Customers | Measure customer base |
| Total Products | Measure product portfolio |
| Total Quantity | Measure sales volume |
| Average Order Value | Measure average transaction value |
| Average Selling Price | Measure average selling price |
| Revenue per Customer | Measure customer contribution |

---

# 7. Dashboard Requirements

The Power BI solution will contain four primary analytical pages.

---

## 7.1 Executive Dashboard

The Executive Dashboard will serve as the main landing page.

### Required KPIs

- Total Sales
- Total Orders
- Total Customers
- Total Products
- Total Quantity
- Average Order Value

### Required Analysis

- Sales Trend
- Sales by Category
- Sales by Country
- Top Products
- Top Customers

### Navigation

Users should be able to navigate to:

- Sales Analysis
- Customer Analysis
- Product Analysis

---

# 8. Sales Dashboard Requirements

The Sales Dashboard will focus on overall sales performance.

### Required Analysis

- Revenue Trend
- Monthly Sales
- Yearly Sales
- Year-over-Year Performance
- Running Total
- Sales by Country
- Sales by Category
- Quantity Trends
- Top Performing Categories
- Bottom Performing Categories

### Filters

Users should be able to filter the analysis by:

- Date
- Year
- Country
- Category

---

# 9. Customer Dashboard Requirements

The Customer Dashboard will focus on customer behavior and contribution.

### Required KPIs

- Total Customers
- Active Customers
- Average Revenue per Customer
- Average Orders per Customer

### Required Analysis

- Revenue by Customer
- Top Customers
- Customers by Country
- Customer Revenue Distribution
- Customer Purchase Frequency
- Customer Segmentation

### Filters

- Date
- Country
- Gender
- Marital Status

---

# 10. Product Dashboard Requirements

The Product Dashboard will focus on product performance.

### Required KPIs

- Total Products
- Products Sold
- Total Quantity
- Average Product Revenue

### Required Analysis

- Revenue by Product
- Top 10 Products
- Bottom 10 Products
- Revenue by Category
- Quantity by Category
- Product Segmentation

### Filters

- Date
- Category
- Sub-Category
- Product

---

# 11. Data Model Requirements

The Power BI semantic model should follow a **Star Schema** architecture.

### Fact Table

```text
gold.fact_sales
