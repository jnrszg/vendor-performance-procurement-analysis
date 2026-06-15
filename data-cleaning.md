# Data Cleaning
This document records the data quality checks and preparation steps performed before analysis.

## Approach
I initially planned to review and prepare the data using Excel. However, while exploring the purchases and sales datasets, I found that the files exceeded Excel's row limit.
To continue reviewing and preparing the data, I used the SQLite database included in the dataset.

## Tables for Analysis
The primary tables selected for analysis are:
* purchases
* sales
* purchase_prices
* vendor_invoice
* begin_inventory
* end_inventory

## Missing Values Review

### purchases
To check for missing values in key fields, I ran the following SQL query:

```sql
SELECT
    COUNT(*) AS TotalRows,
    SUM(CASE WHEN VendorName IS NULL THEN 1 ELSE 0 END) AS MissingVendorName,
    SUM(CASE WHEN PurchasePrice IS NULL THEN 1 ELSE 0 END) AS MissingPurchasePrice,
    SUM(CASE WHEN Quantity IS NULL THEN 1 ELSE 0 END) AS MissingQuantity,
    SUM(CASE WHEN Dollars IS NULL THEN 1 ELSE 0 END) AS MissingDollars
FROM purchases;
```

### Results
| Metric                | Value     |
| --------------------- | --------- |
| Total Rows            | 2,372,474 |
| Missing VendorName    | 0         |
| Missing PurchasePrice | 0         |
| Missing Quantity      | 0         |
| Missing Dollars       | 0         |

### Observation
No missing values were found in the key fields reviewed. The purchases table appears suitable for procurement analysis.

### sales
To check for missing values in key fields, I ran the following SQL query:

```sql
SELECT
    COUNT(*) AS TotalRows,
    SUM(CASE WHEN VendorName IS NULL THEN 1 ELSE 0 END) AS MissingVendorName,
    SUM(CASE WHEN SalesQuantity IS NULL THEN 1 ELSE 0 END) AS MissingSalesQuantity,
    SUM(CASE WHEN SalesPrice IS NULL THEN 1 ELSE 0 END) AS MissingSalesPrice,
    SUM(CASE WHEN SalesDollars IS NULL THEN 1 ELSE 0 END) AS MissingSalesDollars
FROM sales;
```

### Results
| Metric                | Value      |
| --------------------- | ---------- |
| Total Rows            | 12,825,363 |
| Missing VendorName    | 0          |
| Missing SalesQuantity | 0          |
| Missing SalesPrice    | 0          |
| Missing SalesDollars  | 0          |

### Observation
No missing values were found in the key fields reviewed. The sales table appears suitable for sales analysis.

