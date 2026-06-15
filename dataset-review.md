# Dataset Review
These are my notes while getting familiar with the dataset before starting the analysis.

## Files Included
* purchases.csv
* sales.csv
* purchase_prices.csv
* vendor_invoice.csv
* begin_inventory.csv
* end_inventory.csv
* vendor_sales_summary.csv
* inventory.db

---

## purchases.csv
### What I think this file is for
This file contains purchase records from vendors. It includes information about the products purchased, supplier details, dates, quantities, and costs.
### Key Fields
* InventoryId
* Brand
* Description
* VendorNumber
* VendorName
* PONumber
* PODate
* ReceivingDate
* InvoiceDate
* PayDate
* PurchasePrice
* Quantity
* Dollars
### Notes
* Looks like each row represents a purchase transaction.
* Contains vendor and product information in the same table.
* Several date fields are available for time-based analysis.
* Purchase quantity and purchase value may be useful for procurement analysis.

---

## sales.csv
### What I think this file is for
This file contains sales records for products sold.
### Key Fields
* InventoryId
* Brand
* Description
* SalesQuantity
* SalesDollars
* SalesPrice
* SalesDate
* VendorNo
* VendorName
### Notes
* Looks like each row represents a sale.
* Includes sales quantity and sales value.
* Contains vendor information that may be useful when comparing purchases and sales.
* Sales dates can be used for trend analysis.

---

## purchase_prices.csv
### What I think this file is for
This file appears to be a reference table containing product pricing and vendor information.
### Key Fields
* Brand
* Description
* Price
* Size
* Volume
* Classification
* PurchasePrice
* VendorNumber
* VendorName
### Notes
* Contains product and supplier details.
* Includes pricing information.
* May be useful as a lookup table rather than a transaction table.
* Could help when reviewing product costs across vendors.

---

## vendor_invoice.csv
### What I think this file is for
This file contains vendor invoice and payment information.
### Key Fields
* VendorNumber
* VendorName
* InvoiceDate
* PONumber
* PODate
* PayDate
* Quantity
* Dollars
* Freight
* Approval
### Notes
* Contains invoice and payment details.
* Includes purchase order information.
* May help analyze vendor spending and payment timing.

---

## begin_inventory.csv
### What I think this file is for
This file shows inventory levels at the beginning of the reporting period.
### Key Fields
* InventoryId
* Store
* City
* Brand
* Description
* Size
* onHand
* Price
* startDate
### Notes
* Shows quantity on hand at the start of the period.
* Includes product and store information.
* Can be used to calculate beginning inventory value.

---

## end_inventory.csv
### What I think this file is for
This file shows inventory levels at the end of the reporting period.
### Key Fields
* InventoryId
* Store
* City
* Brand
* Description
* Size
* onHand
* Price
* endDate
### Notes
* Shows quantity on hand at the end of the period.
* Can be compared with beginning inventory data.
* May help identify inventory movement over time.

---

## vendor_sales_summary.csv
### What I think this file is for
This file contains summarized vendor and product performance data.
### Key Fields
* VendorNumber
* VendorName
* Brand
* Description
* TotalPurchaseQuantity
* TotalPurchaseDollars
* TotalSalesQuantity
* TotalSalesDollars
* GrossProfit
* ProfitMargin
* StockTurnover
* SalestoPurchaseRatio
### Notes
* Contains pre-calculated metrics.
* Appears to be created from the other dataset files.
* Useful for checking results later.
### Decision
For this project, I plan to use the raw transaction tables for the analysis and use this file only as a reference.
