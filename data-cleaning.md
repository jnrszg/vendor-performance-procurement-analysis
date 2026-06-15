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

### purchase_prices
To check for missing values in key fields, I ran the following SQL query:

```sql
SELECT
    COUNT(*) AS TotalRows,
    SUM(CASE WHEN VendorName IS NULL THEN 1 ELSE 0 END) AS MissingVendorName,
    SUM(CASE WHEN Description IS NULL THEN 1 ELSE 0 END) AS MissingDescription,
    SUM(CASE WHEN Price IS NULL THEN 1 ELSE 0 END) AS MissingPrice,
    SUM(CASE WHEN PurchasePrice IS NULL THEN 1 ELSE 0 END) AS MissingPurchasePrice
FROM purchase_prices;
```

### Results
| Metric                | Value  |
| --------------------- | ------ |
| Total Rows            | 12,261 |
| Missing VendorName    | 0      |
| Missing Description   | 1      |
| Missing Price         | 0      |
| Missing PurchasePrice | 0      |

### Observation
One record contains a missing product description. No missing values were found in the other key fields reviewed.

### Missing Description Investigation
A missing Description value was identified in the purchase_prices table.
Further review of the record showed that the same row also contains missing values in the Size and Volume fields. The Price field contains a value of 0.0.

The record belongs to Vendor 480 (BACARDI USA INC) and Brand 4202.

Decision:
The record will be retained and documented. Since only one record was affected, the impact on the overall analysis is expected to be minimal.

### vendor_invoice

To check for missing values in key fields, I ran the following SQL query:

```sql
SELECT
    COUNT(*) AS TotalRows,
    SUM(CASE WHEN VendorName IS NULL THEN 1 ELSE 0 END) AS MissingVendorName,
    SUM(CASE WHEN Quantity IS NULL THEN 1 ELSE 0 END) AS MissingQuantity,
    SUM(CASE WHEN Dollars IS NULL THEN 1 ELSE 0 END) AS MissingDollars,
    SUM(CASE WHEN InvoiceDate IS NULL THEN 1 ELSE 0 END) AS MissingInvoiceDate
FROM vendor_invoice;
```

### Results
| Metric             | Value |
| ------------------ | ----- |
| Total Rows         | 5,543 |
| Missing VendorName | 0     |
| Missing Quantity   | 0     |
| Missing Dollars    | 0     |
| Missing InvoiceDate| 0     |

### Observation
No missing values were found in the key fields reviewed. The vendor_invoice table appears suitable for vendor spending and payment analysis.

### begin_inventory
To check for missing values in key fields, I ran the following SQL query:

```sql
SELECT
    COUNT(*) AS TotalRows,
    SUM(CASE WHEN Description IS NULL THEN 1 ELSE 0 END) AS MissingDescription,
    SUM(CASE WHEN onHand IS NULL THEN 1 ELSE 0 END) AS MissingOnHand,
    SUM(CASE WHEN Price IS NULL THEN 1 ELSE 0 END) AS MissingPrice,
    SUM(CASE WHEN startDate IS NULL THEN 1 ELSE 0 END) AS MissingStartDate
FROM begin_inventory;
```

### Results
| Metric              | Value   |
| ------------------- | ------- |
| Total Rows          | 206,529 |
| Missing Description | 0       |
| Missing OnHand      | 0       |
| Missing Price       | 0       |
| Missing StartDate   | 0       |

### Observation
No missing values were found in the key fields reviewed. The begin_inventory table appears suitable for inventory analysis.

### end_inventory
To check for missing values in key fields, I ran the following SQL query:

```sql
SELECT
    COUNT(*) AS TotalRows,
    SUM(CASE WHEN Description IS NULL THEN 1 ELSE 0 END) AS MissingDescription,
    SUM(CASE WHEN onHand IS NULL THEN 1 ELSE 0 END) AS MissingOnHand,
    SUM(CASE WHEN Price IS NULL THEN 1 ELSE 0 END) AS MissingPrice,
    SUM(CASE WHEN endDate IS NULL THEN 1 ELSE 0 END) AS MissingEndDate
FROM end_inventory;
```

### Results
| Metric              | Value   |
| ------------------- | ------- |
| Total Rows          | 224,489 |
| Missing Description | 0       |
| Missing OnHand      | 0       |
| Missing Price       | 0       |
| Missing EndDate     | 0       |

### Observation
No missing values were found in the key fields reviewed. The end_inventory table appears suitable for inventory analysis.
