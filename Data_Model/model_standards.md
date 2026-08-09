# Data Model Standards

## 1. Purpose

This document defines the modeling standards used in the Power BI Sales Analytics project.

The objective is to maintain a clean, scalable, understandable, and performance-oriented Power BI semantic model.

---

## 2. Modeling Architecture

The project follows a **Star Schema**.

### Central Fact

`gold fact_sales`

### Dimensions

- `gold dim_products`
- `gold dim_customers`
- `dim_date`

### Supporting Table

- `dim_measures` — disconnected measure table

The fact table remains at the center while dimensions provide descriptive filtering and slicing.

---

## 3. Table Naming Standards

The existing Gold-layer source table names are preserved as the project source of truth:

- `gold fact_sales`
- `gold dim_products`
- `gold dim_customers`

The Power BI-created supporting tables use:

- `dim_date`
- `dim_measures`

**Important:** Existing SQL source table names and source column names must not be changed without first documenting and explaining the reason.

---

## 4. Column Naming Standards

Source column names are preserved.

### Fact Table

`gold fact_sales`

```text
order_name
product_key
customer_key
order_date
shipping_date
due_date
sales_amount
quantity
price
```

### Product Dimension

`gold dim_products`

```text
product_key
product_id
product_number
product_name
category_id
category
sub_category
maintenance
cost
product_line
start_date
```

### Customer Dimension

`gold dim_customers`

```text
customer_key
customer_id
customer_number
first_name
last_name
country
marital_status
gender
birthdate
create_date
```

---

## 5. Key Standards

### Primary / Dimension Keys

- `gold dim_products[product_key]`
- `gold dim_customers[customer_key]`

### Fact Foreign Keys

- `gold fact_sales[product_key]`
- `gold fact_sales[customer_key]`

The key names are intentionally consistent between dimensions and fact table to make relationship management clear.

---

## 6. Fact Table Standards

`gold fact_sales` represents sales transaction-level data.

### Measures / Numeric Fields

- `sales_amount`
- `quantity`
- `price`

### Transaction / Date Fields

- `order_name`
- `order_date`
- `shipping_date`
- `due_date`

The fact table should remain focused on measurable business events and their related keys.

---

## 7. Dimension Standards

### Product Dimension

`gold dim_products` provides product-level descriptive attributes.

Examples:

- `product_name`
- `product_number`
- `category`
- `sub_category`
- `product_line`
- `maintenance`

### Customer Dimension

`gold dim_customers` provides customer-level descriptive attributes.

Examples:

- `first_name`
- `last_name`
- `country`
- `gender`
- `marital_status`
- `birthdate`

### Date Dimension

`dim_date` is the centralized date table used for time intelligence.

It contains date attributes used for:

- Year analysis
- Quarter analysis
- Month analysis
- Month sorting
- Time-based filtering

---

## 8. Measure Management Standard

All reusable business measures are centralized in:

`dim_measures`

Examples include:

- Total Sales
- Total Orders
- Total Customers
- Total Products
- Total Quantity
- Average Order Value
- Average Quantity per Order
- Average Selling Price
- Current Year Sales
- Sales YTD
- Sales QTD
- Sales MTD
- Sales Previous Year
- Sales YoY Growth %
- Customer Sales %
- Customer Sales Rank
- Product Sales %
- Product Sales Rank
- Revenue per Customer

### Rule

When a new reusable business calculation is required, create it in `dim_measures` unless there is a specific modeling reason to place it elsewhere.

---

## 9. Relationship Standards

The project follows these relationship rules:

- Dimension → Fact
- 1-to-many cardinality
- Single-direction filtering
- No unnecessary bidirectional relationships
- No unnecessary many-to-many relationships
- No fact-to-fact relationships

The main relationships are:

```text
gold dim_products[product_key]
        1
        |
        *
gold fact_sales[product_key]


gold dim_customers[customer_key]
        1
        |
        *
gold fact_sales[customer_key]


dim_date[Date]
        1
        |
        *
gold fact_sales[order_date]
```

Shipping Date and Due Date are secondary date roles and are handled through the date model/DAX when required.

---

## 10. Date Modeling Standards

`dim_date` is the dedicated Date Dimension.

The model should not depend on automatically generated hidden date tables for core time intelligence.

`order_date` is the primary reporting date.

`shipping_date` and `due_date` are secondary business dates.

Time-intelligence measures such as:

- Current Year Sales
- Sales YTD
- Sales QTD
- Sales MTD
- Sales Previous Year
- Sales YoY Growth %

are built using the centralized date model.

---

## 11. DAX Standards

### General Rules

- Prefer measures for dynamic calculations.
- Avoid unnecessary calculated columns.
- Reuse existing measures inside new measures.
- Keep measure names business-friendly.
- Use explicit table and column references.
- Keep calculations centralized in `dim_measures`.
- Use time-intelligence functions with `dim_date`.

### Example

```DAX
Total Sales =
SUM('gold fact_sales'[sales_amount])
```

A derived measure should reuse the base measure where appropriate rather than repeating the same aggregation logic.

---

## 12. Performance Standards

To keep the model efficient:

- Keep the Star Schema simple.
- Avoid unnecessary columns.
- Avoid unnecessary calculated columns.
- Prefer measures over calculated columns for report calculations.
- Avoid unnecessary bidirectional filtering.
- Avoid unnecessary many-to-many relationships.
- Keep dimensions descriptive and facts transactional.
- Use the Gold-layer tables as the analytical source.

---

## 13. Formatting Standards

### Measures

Business measures should use readable names:

```text
Total Sales
Total Orders
Current Year Sales
Sales YoY Growth %
Average Order Value
```

### Numeric Formatting

Recommended formatting:

- Sales / Revenue → Currency or appropriate financial format
- Quantity → Whole number
- Orders / Customers / Products → Whole number
- Percentages → Percentage
- Average Selling Price → Currency
- Average Order Value → Currency

---

## 14. Hidden / Supporting Objects

`dim_measures` is a supporting table and is intentionally disconnected.

The helper column/table structure should not be used for report filtering.

Measures should be the primary objects consumed by report visuals.

---

## 15. Change Control

The following are considered model-breaking changes and should not be made casually:

- Renaming source tables
- Renaming source columns
- Changing relationship keys
- Changing relationship direction
- Changing the primary date relationship
- Introducing unnecessary bidirectional filtering
- Replacing the Star Schema with a different architecture

If a change becomes necessary, document:

1. What is changing
2. Why it is required
3. Business impact
4. Modeling impact
5. Performance impact
6. Documentation updates required

---

## 16. Final Model Principle

> **Keep the model simple, dimensional, reusable, and business-friendly.**

The Power BI model should allow Sales, Customer, Product, and Time analysis to work dynamically from the same semantic model while keeping business logic centralized and maintainable.
