### DATA CLEANING
This document records the data quality checks and preparation steps performed before analysis.

---
### Approach
I initially planned to review and prepare the data using Excel. However, while exploring the purchases and sales datasets, I found that the files exceeded Excel's row limit.
To continue reviewing and preparing the data, I used the SQLite database included in the dataset.

---
### Tables for Analysis
The primary tables selected for analysis are:
* purchases
* sales
* purchase_prices
* vendor_invoice
* begin_inventory
* end_inventory

---
### MISSING VALUES REVIEW
---
## purchases
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

## sales
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

## purchase_prices
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

## vendor_invoice

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

## begin_inventory
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

## end_inventory
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

---
### DUPLICATE RECORD REVIEWS

---
## purchases
To investigate potential duplicate records, I compared the total number of rows with the number of unique InventoryIds.

```sql
SELECT
    COUNT(*) AS TotalRows,
    COUNT(DISTINCT InventoryId) AS UniqueInventoryIds
FROM purchases;
```

### Results
| Metric              | Value     |
| ------------------- | --------- |
| Total Rows          | 2,372,474 |
| Unique InventoryIds | 245,907   |

### Observation
InventoryIds appear multiple times throughout the dataset. This is expected because the same inventory item can be purchased across different transactions, stores, and dates.

Further investigation was performed to determine whether exact duplicate records existed.

```sql
SELECT COUNT(*) AS DuplicateRows
FROM (
    SELECT *,
           COUNT(*) AS RecordCount
    FROM purchases
    GROUP BY
        InventoryId,
        Store,
        Brand,
        Description,
        Size,
        VendorNumber,
        VendorName,
        PONumber,
        PODate,
        ReceivingDate,
        InvoiceDate,
        PayDate,
        PurchasePrice,
        Quantity,
        Dollars,
        Classification
    HAVING COUNT(*) > 1
);
```

### Results
| Metric        | Value |
| ------------- | ----- |
| DuplicateRows | 0     |

### Observation
No exact duplicate records were identified in the purchases table.

## sales

To investigate potential duplicate records, I compared the total number of rows with the number of unique InventoryIds.

```sql
SELECT
    COUNT(*) AS TotalRows,
    COUNT(DISTINCT InventoryId) AS UniqueInventoryIds
FROM sales;
```

### Results
| Metric              | Value      |
| ------------------- | ---------- |
| Total Rows          | 12,825,363 |
| Unique InventoryIds | 267,552    |

### Observation
InventoryIds appear multiple times throughout the dataset. This is expected because the same inventory item can be sold across multiple transactions and dates.

Further investigation was performed to determine whether exact duplicate records existed.

```sql
SELECT COUNT(*) AS DuplicateRows
FROM (
    SELECT *,
           COUNT(*) AS RecordCount
    FROM sales
    GROUP BY
        InventoryId,
        Store,
        Brand,
        Description,
        Size,
        SalesQuantity,
        SalesDollars,
        SalesPrice,
        SalesDate,
        Volume,
        Classification,
        ExciseTax,
        VendorNo,
        VendorName
    HAVING COUNT(*) > 1
);
```

### Results
| Metric        | Value |
| ------------- | ----- |
| DuplicateRows | 0     |

### Observation
No exact duplicate records were identified in the sales table.

## purchase_prices
To investigate potential duplicate records, I compared the total number of rows with the number of unique Brands.

```sql
SELECT
    COUNT(*) AS TotalRows,
    COUNT(DISTINCT Brand) AS UniqueBrands
FROM purchase_prices;
```

### Results
| Metric        | Value  |
| ------------- | ------ |
| Total Rows    | 12,261 |
| Unique Brands | 12,261 |

### Observation
The number of unique Brands matches the total number of rows, indicating that each Brand appears only once in the table. This is consistent with the table's role as a product pricing reference table.

Further investigation was performed to determine whether exact duplicate records existed.

```sql
SELECT COUNT(*) AS DuplicateRows
FROM (
    SELECT *,
           COUNT(*) AS RecordCount
    FROM purchase_prices
    GROUP BY
        Brand,
        Description,
        Price,
        Size,
        Volume,
        Classification,
        PurchasePrice,
        VendorNumber,
        VendorName
    HAVING COUNT(*) > 1
);
```

### Results
| Metric        | Value |
| ------------- | ----- |
| DuplicateRows | 0     |

### Observation
No exact duplicate records were identified in the purchase_prices table.

## vendor_invoice
To investigate potential duplicate records, I compared the total number of rows with the number of unique purchase order numbers.

```sql
SELECT
    COUNT(*) AS TotalRows,
    COUNT(DISTINCT PONumber) AS UniquePONumbers
FROM vendor_invoice;
```

### Results
| Metric           | Value |
| ---------------- | ----- |
| Total Rows       | 5,543 |
| Unique PONumbers | 5,543 |

### Observation
The number of unique purchase order numbers matches the total number of rows, indicating that each purchase order appears only once in the table.

Further investigation was performed to determine whether exact duplicate records existed.

```sql
SELECT COUNT(*) AS DuplicateRows
FROM (
    SELECT *,
           COUNT(*) AS RecordCount
    FROM vendor_invoice
    GROUP BY
        VendorNumber,
        VendorName,
        InvoiceDate,
        PONumber,
        PODate,
        PayDate,
        Quantity,
        Dollars,
        Freight,
        Approval
    HAVING COUNT(*) > 1
);
```

### Results
| Metric        | Value |
| ------------- | ----- |
| DuplicateRows | 0     |

### Observation
No exact duplicate records were identified in the vendor_invoice table.

## begin_inventory
To investigate potential duplicate records, I compared the total number of rows with the number of unique InventoryIds.

```sql
SELECT
    COUNT(*) AS TotalRows,
    COUNT(DISTINCT InventoryId) AS UniqueInventoryIds
FROM begin_inventory;
```

### Results
| Metric              | Value   |
| ------------------- | ------- |
| Total Rows          | 206,529 |
| Unique InventoryIds | 206,529 |

### Observation
The number of unique InventoryIds matches the total number of rows, indicating that each inventory record appears only once in the table.
Further investigation was performed to determine whether exact duplicate records existed.

```sql
SELECT COUNT(*) AS DuplicateRows
FROM (
    SELECT *,
           COUNT(*) AS RecordCount
    FROM begin_inventory
    GROUP BY
        InventoryId,
        Store,
        City,
        Brand,
        Description,
        Size,
        onHand,
        Price,
        startDate
    HAVING COUNT(*) > 1
);
```

### Results
| Metric        | Value |
| ------------- | ----- |
| DuplicateRows | 0     |

### Observation
No exact duplicate records were identified in the begin_inventory table.

## end_inventory
To investigate potential duplicate records, I compared the total number of rows with the number of unique InventoryIds.

```sql
SELECT
    COUNT(*) AS TotalRows,
    COUNT(DISTINCT InventoryId) AS UniqueInventoryIds
FROM end_inventory;
```

### Results
| Metric              | Value   |
| ------------------- | ------- |
| Total Rows          | 224,489 |
| Unique InventoryIds | 224,489 |

### Observation
The number of unique InventoryIds matches the total number of rows, indicating that each inventory record appears only once in the table.

Further investigation was performed to determine whether exact duplicate records existed.

```sql
SELECT COUNT(*) AS DuplicateRows
FROM (
    SELECT *,
           COUNT(*) AS RecordCount
    FROM end_inventory
    GROUP BY
        InventoryId,
        Store,
        City,
        Brand,
        Description,
        Size,
        onHand,
        Price,
        endDate
    HAVING COUNT(*) > 1
);
```

### Results
| Metric        | Value |
| ------------- | ----- |
| DuplicateRows | 0     |

### Observation
No exact duplicate records were identified in the end_inventory table.

---
### DATA FORMAT REVIEW
---

## purchases
To review date formats in the purchases table, I checked the earliest and latest values for key date fields.

```sql
SELECT
    MIN(PODate) AS EarliestPODate,
    MAX(PODate) AS LatestPODate,
    MIN(InvoiceDate) AS EarliestInvoiceDate,
    MAX(InvoiceDate) AS LatestInvoiceDate
FROM purchases;
```
### Results
| Metric              | Value      |
| ------------------- | ---------- |
| Earliest PO Date    | 2023-12-20 |
| Latest PO Date      | 2024-12-23 |
| Earliest Invoice Date | 2024-01-04 |
| Latest Invoice Date | 2025-01-10 |

### Observation
The date fields reviewed are stored in a consistent YYYY-MM-DD format.
No formatting issues were identified, and the dates appear suitable for time-based analysis.

## sales
To review date formats in the sales table, I checked the earliest and latest values in the SalesDate field.

```sql
SELECT
    MIN(SalesDate) AS EarliestSalesDate,
    MAX(SalesDate) AS LatestSalesDate
FROM sales;
```

### Results
| Metric | Value |
| -------- | -------- |
| Earliest Sales Date | 2024-01-01 |
| Latest Sales Date | 2024-12-31 |

### Observation
The SalesDate field is stored in a consistent YYYY-MM-DD format.
The date range spans the full 2024 calendar year, and no obvious formatting issues were identified. The field appears suitable for trend and time-series analysis.

## purchase_prices
The purchase_prices table does not contain any date fields requiring format validation.

A review of the table structure showed that product, vendor, and pricing fields are stored consistently and no date format standardization was required.

## vendor_invoice
To review date formats in the vendor_invoice table, I checked the earliest and latest values for the purchase order, invoice, and payment dates.

```sql
SELECT
    MIN(PODate) AS EarliestPODate,
    MAX(PODate) AS LatestPODate,
    MIN(InvoiceDate) AS EarliestInvoiceDate,
    MAX(InvoiceDate) AS LatestInvoiceDate,
    MIN(PayDate) AS EarliestPayDate,
    MAX(PayDate) AS LatestPayDate
FROM vendor_invoice;
```

### Results
| Metric | Value |
| -------- | -------- |
| Earliest PO Date | 2023-12-20 |
| Latest PO Date | 2024-12-23 |
| Earliest Invoice Date | 2024-01-04 |
| Latest Invoice Date | 2025-01-10 |
| Earliest Pay Date | 2024-02-04 |
| Latest Pay Date | 2025-02-19 |

### Observation
The PODate, InvoiceDate, and PayDate fields are stored in a consistent YYYY-MM-DD format.
No formatting issues were identified, and the dates appear suitable for procurement and payment analysis.

## begin_inventory
To review date formats in the begin_inventory table, I checked the earliest and latest values in the startDate field.

```sql
SELECT
    MIN(startDate) AS EarliestStartDate,
    MAX(startDate) AS LatestStartDate
FROM begin_inventory;
```

### Results
| Metric | Value |
| -------- | -------- |
| Earliest Start Date | 2024-01-01 |
| Latest Start Date | 2024-01-01 |

### Observation
The startDate field is stored in a consistent YYYY-MM-DD format.
All records share the same start date, which is expected because the table represents beginning inventory balances at the start of the reporting period.

## end_inventory
To review date formats in the end_inventory table, I checked the earliest and latest values in the endDate field.

```sql
SELECT
    MIN(endDate) AS EarliestEndDate,
    MAX(endDate) AS LatestEndDate
FROM end_inventory;
```

### Results
| Metric | Value |
| -------- | -------- |
| Earliest End Date | 2024-12-31 |
| Latest End Date | 2024-12-31 |

### Observation
The endDate field is stored in a consistent YYYY-MM-DD format.
All records share the same end date, which is expected because the table represents ending inventory balances at the end of the reporting period.

---
### DATA VALIDATION
---

## purchases
To validate purchase values, I reviewed the minimum and maximum values for PurchasePrice and Dollars.

```sql
SELECT
    MIN(PurchasePrice) AS MinPurchasePrice,
    MAX(PurchasePrice) AS MaxPurchasePrice,
    MIN(Dollars) AS MinDollars,
    MAX(Dollars) AS MaxDollars
FROM purchases;
```

### Results
| Metric | Value |
| -------- | -------- |
| MinPurchasePrice | 0.00 |
| MaxPurchasePrice | 5,681.81 |
| MinDollars | 0.00 |
| MaxDollars | 50,175.70 |

### Observation
Zero values were identified in the PurchasePrice and Dollars fields.
To investigate further, I reviewed records with a PurchasePrice or Dollars value of 0.00.

```sql
SELECT *
FROM purchases
WHERE PurchasePrice = 0
   OR Dollars = 0;
```

The query returned 153 records.
Sample records were reviewed and appeared to represent legitimate business transactions involving specific products, vendors, and purchase orders distributed across multiple stores.

### Decision
The records were retained for analysis and documented as part of the data validation process.

## sales
To validate sales values, I reviewed the minimum and maximum values for SalesQuantity, SalesPrice, and SalesDollars.

```sql
SELECT
    MIN(SalesQuantity) AS MinSalesQuantity,
    MAX(SalesQuantity) AS MaxSalesQuantity,
    MIN(SalesPrice) AS MinSalesPrice,
    MAX(SalesPrice) AS MaxSalesPrice,
    MIN(SalesDollars) AS MinSalesDollars,
    MAX(SalesDollars) AS MaxSalesDollars
FROM sales;
```

### Results
| Metric | Value |
| -------- | -------- |
| MinSalesQuantity | 1 |
| MaxSalesQuantity | 1,231 |
| MinSalesPrice | 0.00 |
| MaxSalesPrice | 5,799.99 |
| MinSalesDollars | 0.00 |
| MaxSalesDollars | 26,061.14 |

### Observation
Zero values were identified in the SalesPrice and SalesDollars fields.

To investigate further, I reviewed records with a SalesPrice or SalesDollars value of 0.00.

```sql
SELECT *
FROM sales
WHERE SalesPrice = 0
   OR SalesDollars = 0;
```

The query returned 55 records.
Sample records were reviewed and appeared to represent legitimate sales transactions involving specific products, vendors, stores, and sales dates.

### Decision
The records were retained for analysis and documented as part of the data validation process.

## purchase_prices
To validate pricing values, I reviewed the minimum and maximum values for Price and PurchasePrice.

```sql
SELECT
    MIN(PurchasePrice) AS MinPurchasePrice,
    MAX(PurchasePrice) AS MaxPurchasePrice,
    MIN(Price) AS MinPrice,
    MAX(Price) AS MaxPrice
FROM purchase_prices;
```

### Results
| Metric | Value |
| -------- | -------- |
| MinPurchasePrice | 0.00 |
| MaxPurchasePrice | 11,111.03 |
| MinPrice | 0.00 |
| MaxPrice | 13,999.90 |

### Observation
Zero values were identified in the Price and PurchasePrice fields.
To investigate further, I reviewed records with a Price or PurchasePrice value of 0.00.

```sql
SELECT *
FROM purchase_prices
WHERE Price = 0
   OR PurchasePrice = 0;
```

The query returned 2 records.
One record was previously identified during the missing values review and contained missing Description, Size, and Volume fields. The second record contained valid product information but had a Price and PurchasePrice value of 0.00.

### Decision
The records were retained and documented. Due to the very small number of affected records, the impact on the overall analysis is expected to be minimal.

## vendor_invoice
To validate invoice values, I reviewed the minimum and maximum values for Quantity, Dollars, and Freight.

```sql
SELECT
    MIN(Quantity) AS MinQuantity,
    MAX(Quantity) AS MaxQuantity,
    MIN(Dollars) AS MinDollars,
    MAX(Dollars) AS MaxDollars,
    MIN(Freight) AS MinFreight,
    MAX(Freight) AS MaxFreight
FROM vendor_invoice;
```

### Results
| Metric | Value |
| -------- | -------- |
| MinQuantity | 1 |
| MaxQuantity | 141,660 |
| MinDollars | 4.14 |
| MaxDollars | 1,660,435.88 |
| MinFreight | 0.02 |
| MaxFreight | 8,468.22 |

### Observation
No zero or negative values were identified in the Quantity, Dollars, or Freight fields reviewed.
The values appear reasonable for vendor invoice transactions and no data quality concerns were identified.

### Decision
No corrective action was required.

## begin_inventory
To validate inventory values, I reviewed the minimum and maximum values for onHand and Price.

```sql
SELECT
    MIN(onHand) AS MinOnHand,
    MAX(onHand) AS MaxOnHand,
    MIN(Price) AS MinPrice,
    MAX(Price) AS MaxPrice
FROM begin_inventory;
```

### Results
| Metric | Value |
| -------- | -------- |
| MinOnHand | 0 |
| MaxOnHand | 1,251 |
| MinPrice | 0.00 |
| MaxPrice | 13,999.90 |

### Observation
Records with an onHand value of 0 and a Price value of 0.00 were identified.
To investigate further, I reviewed the number of affected records.

```sql
SELECT COUNT(*) AS ZeroOnHandRecords
FROM begin_inventory
WHERE onHand = 0;

SELECT COUNT(*) AS ZeroPriceRecords
FROM begin_inventory
WHERE Price = 0;
```

### Results
| Metric | Value |
| -------- | -------- |
| ZeroOnHandRecords | 6,044 |
| ZeroPriceRecords | 2 |

### Observation
Inventory records with an onHand value of 0 are expected in operational inventory data and may represent products that were temporarily out of stock or depleted.

Only 2 records contained a Price value of 0.00. The impact on inventory analysis is expected to be minimal.

### Decision
The records were retained and documented as part of the data validation process.

## end_inventory
To validate inventory values, I reviewed the minimum and maximum values for onHand and Price.

```sql
SELECT
    MIN(onHand) AS MinOnHand,
    MAX(onHand) AS MaxOnHand,
    MIN(Price) AS MinPrice,
    MAX(Price) AS MaxPrice
FROM end_inventory;
```

### Results
| Metric | Value |
| -------- | -------- |
| MinOnHand | 0 |
| MaxOnHand | 3,676 |
| MinPrice | 0.49 |
| MaxPrice | 13,999.90 |

### Observation
Records with an onHand value of 0 were identified.
To investigate further, I reviewed the number of affected records.

```sql
SELECT COUNT(*) AS ZeroOnHandRecords
FROM end_inventory
WHERE onHand = 0;

SELECT COUNT(*) AS ZeroPriceRecords
FROM end_inventory
WHERE Price = 0;
```

### Results
| Metric | Value |
| -------- | -------- |
| ZeroOnHandRecords | 7,230 |
| ZeroPriceRecords | 0 |

### Observation
Inventory records with an onHand value of 0 are expected in operational inventory data and may represent products that were temporarily out of stock or depleted.
No records contained a Price value of 0.00, indicating that inventory pricing data was complete for the fields reviewed.

### Decision
The records were retained and no corrective action was required.

## Data Validation Summary
- The key business fields in each table were reviewed to identify unusual values that could affect the analysis.
- Several records with zero values were found in the purchases, sales, and purchase_prices tables. These records were investigated and appeared to represent legitimate business transactions or isolated product records rather than data entry errors.
- The inventory tables contained records with an onHand value of 0, which is expected in inventory data and indicates products that were out of stock at the time of reporting.
- Overall, no major data quality issues were identified. The dataset was considered suitable for procurement, sales, vendor, and inventory analysis, and all records were retained for further analysis.
