# Relationship Documentation

## 1. Overview

The Power BI Sales Analytics model follows a **Star Schema** design.

The model contains:

- `gold fact_sales` — central fact table
- `gold dim_products` — product dimension
- `gold dim_customers` — customer dimension
- `dim_date` — dedicated date dimension
- `dim_measures` — disconnected centralized measure table

The model is designed for dynamic Sales, Customer, Product, and Time analysis.

---

## 2. Core Relationships

### 2.1 Product → Sales

| From Table | From Column | To Table | To Column | Cardinality | Cross Filter |
|---|---|---|---|---|---|
| `gold dim_products` | `product_key` | `gold fact_sales` | `product_key` | 1 : * | Single |

**Purpose:**  
Allows product attributes such as product name, category, sub-category, product line, and product number to filter sales transactions.

---

### 2.2 Customer → Sales

| From Table | From Column | To Table | To Column | Cardinality | Cross Filter |
|---|---|---|---|---|---|
| `gold dim_customers` | `customer_key` | `gold fact_sales` | `customer_key` | 1 : * | Single |

**Purpose:**  
Allows customer attributes such as customer name, country, gender, and marital status to filter sales transactions.

---

## 3. Date Relationships

`dim_date` is the dedicated Date Dimension and is used for time-based analysis.

The fact table contains three business date columns:

- `order_date`
- `shipping_date`
- `due_date`

The intended model uses `dim_date[Date]` with these fact-table date columns.

### Date Role

| Date Dimension | Fact Table | Relationship Role |
|---|---|---|
| `dim_date[Date]` | `gold fact_sales[order_date]` | Active / Primary Date |
| `dim_date[Date]` | `gold fact_sales[shipping_date]` | Inactive / Secondary Date |
| `dim_date[Date]` | `gold fact_sales[due_date]` | Inactive / Secondary Date |

**Primary reporting date:** `order_date`

The inactive relationships can be activated inside DAX when analysis specifically requires Shipping Date or Due Date.

---

## 4. Measures Table

### `dim_measures`

`dim_measures` is a **disconnected table**.

It intentionally has **no relationships** with:

- `gold fact_sales`
- `gold dim_products`
- `gold dim_customers`
- `dim_date`

All centralized measures are stored in this table so that report authors can find and manage business calculations from one location.

Current measure categories include:

- Sales
- Orders
- Customers
- Products
- Quantity
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

Additional measures can be added to `dim_measures` later when required by the dashboards.

---

## 5. Relationship Design Rules

1. Dimension tables filter the fact table.
2. Relationships use surrogate/business model keys already present in the Gold layer.
3. The model avoids unnecessary fact-to-fact relationships.
4. The model avoids unnecessary many-to-many relationships.
5. `dim_date` is the centralized time dimension.
6. `dim_measures` remains disconnected.
7. Single-direction filtering is preferred for the Star Schema.
8. DAX measures should be used for business calculations instead of unnecessary calculated columns.

---

## 6. Model Structure

```text
                  gold dim_products
                         |
                    1 : *
                         |
                         v
gold dim_customers --> gold fact_sales <-- dim_date
       1 : *                 ^              |
                             |              |
                         Measures       Date Roles
                             |
                       dim_measures
                    (Disconnected)
```

---

## 7. Validation Checklist

Before moving to dashboard development, verify:

- [x] Product relationship uses `product_key`
- [x] Customer relationship uses `customer_key`
- [x] `dim_date` is used as the dedicated date dimension
- [x] `order_date` is the primary reporting date
- [x] Shipping and Due Date relationships are secondary/inactive
- [x] `dim_measures` has no relationship
- [x] Fact table remains the center of the Star Schema
- [x] No unnecessary relationship has been introduced

---

## 8. Source Columns

### `gold fact_sales`

- `order_name`
- `product_key`
- `customer_key`
- `order_date`
- `shipping_date`
- `due_date`
- `sales_amount`
- `quantity`
- `price`

### `gold dim_products`

- `product_key`
- `product_id`
- `product_number`
- `product_name`
- `category_id`
- `category`
- `sub_category`
- `maintenance`
- `cost`
- `product_line`
- `start_date`

### `gold dim_customers`

- `customer_key`
- `customer_id`
- `customer_number`
- `first_name`
- `last_name`
- `country`
- `marital_status`
- `gender`
- `birthdate`
- `create_date`
