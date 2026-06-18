# DASHBOARD DEVELOPMENT

---

## Objective

The goal of this phase is to create interactive Power BI dashboards that transform procurement, sales, and inventory data into actionable business insights. The dashboards were designed to support decision-making through KPI monitoring, trend analysis, vendor evaluation, product performance tracking, inventory management, and store-level analysis.

---

# KPI Measures

## Procurement Dashboard

| KPI                      | DAX Measure                                                               |
| ------------------------ | ------------------------------------------------------------------------- |
| Total Procurement Spend  | `SUM(purchases[Dollars])`                                                 |
| Total Purchase Quantity  | `SUM(purchases[Quantity])`                                                |
| Active Vendors           | `DISTINCTCOUNT(purchases[VendorName])`                                    |
| Largest Vendor Spend     | `MAXX(VALUES(purchases[VendorName]), CALCULATE(SUM(purchases[Dollars])))` |
| Average Spend per Vendor | `DIVIDE([Total Procurement Spend],[Active Vendors])`                      |

### KPI Results

| KPI                      | Value    |
| ------------------------ | -------- |
| Total Procurement Spend  | $321.90M |
| Total Purchase Quantity  | 34M      |
| Active Vendors           | 128      |
| Largest Vendor Spend     | $50.96M  |
| Average Spend per Vendor | $2.51M   |

---

## Sales Dashboard

| KPI                   | DAX Measure                                                             |
| --------------------- | ----------------------------------------------------------------------- |
| Total Sales Revenue   | `SUM(sales[SalesDollars])`                                              |
| Units Sold            | `SUM(sales[SalesQuantity])`                                             |
| Products Sold         | `DISTINCTCOUNT(sales[Description])`                                     |
| Average Selling Price | `DIVIDE(SUM(sales[SalesDollars]), SUM(sales[SalesQuantity]))`           |
| Top Product Revenue   | `MAXX(VALUES(sales[Description]), CALCULATE(SUM(sales[SalesDollars])))` |

### KPI Results

| KPI                   | Value    |
| --------------------- | -------- |
| Total Sales Revenue   | $452.06M |
| Units Sold            | 33M      |
| Products Sold         | 10K      |
| Average Selling Price | $13.73   |
| Top Product Revenue   | $7.96M   |

---

## Inventory Dashboard

| KPI                                 | DAX Measure                                                         |
| ----------------------------------- | ------------------------------------------------------------------- |
| Total Inventory Value               | `SUMX(end_inventory, end_inventory[onHand] * end_inventory[Price])` |
| Total Inventory Units               | `SUM(end_inventory[onHand])`                                        |
| Active Products                     | `DISTINCTCOUNT(end_inventory[Description])`                         |
| Active Stores                       | `DISTINCTCOUNT(end_inventory[Store])`                               |
| Average Inventory Value per Product | `DIVIDE([Total Inventory Value],[Active Products])`                 |

### KPI Results

| KPI                                 | Value   |
| ----------------------------------- | ------- |
| Total Inventory Value               | $79.70M |
| Total Inventory Units               | 5M      |
| Active Products                     | 9K      |
| Active Stores                       | 80      |
| Average Inventory Value per Product | $9.13K  |

---

# POWER BI VISUALIZATIONS

## Procurement Analysis

### Top Vendors by Procurement Spend

**Chart Type:** Horizontal Bar Chart

**Fields Used:**

* VendorName
* Dollars

> **Key Finding:**
> DIAGEO NORTH AMERICA INC recorded the highest procurement spend at approximately $50.96M, followed by MARTIGNETTI COMPANIES and JIM BEAM BRANDS COMPANY.

---

### Top Products by Procurement Spend

**Chart Type:** Horizontal Bar Chart

**Fields Used:**

* Description
* Dollars

> **Key Finding:**
> Jack Daniels No. 7 Black Label, Tito's Handmade Vodka, and Grey Goose Vodka accounted for a significant portion of procurement expenditure, indicating concentrated investment in premium beverage products.

---

### Monthly Procurement Spending Trend

**Chart Type:** Line Chart

**Fields Used:**

* PODate (Month)
* Dollars

> **Key Finding:**
> Procurement spending increased steadily throughout the year, rising from approximately $19.1M in January to a peak of approximately $33.3M in December.

---

### Vendor Spend Concentration

**Chart Type:** Treemap

**Fields Used:**

* VendorName
* Dollars

> **Key Finding:**
> Procurement spending was concentrated among a relatively small group of suppliers, highlighting the importance of managing strategic vendor relationships and supplier dependency risks.

---

## Sales Analysis

### Top Vendors by Sales Revenue

**Chart Type:** Horizontal Bar Chart

**Fields Used:**

* VendorName
* SalesDollars

> **Key Finding:**
> DIAGEO NORTH AMERICA INC generated the highest sales revenue, followed by MARTIGNETTI COMPANIES and PERNOD RICARD USA.

---

### Top Products by Sales Revenue

**Chart Type:** Horizontal Bar Chart

**Fields Used:**

* Description
* SalesDollars

> **Key Finding:**
> Jack Daniels No. 7 Black Label generated the highest sales revenue at approximately $7.96M, followed by Tito's Handmade Vodka and Grey Goose Vodka.

---

### Monthly Sales Revenue Trend

**Chart Type:** Line Chart

**Fields Used:**

* SalesDate (Month)
* SalesDollars

> **Key Finding:**
> Sales revenue strengthened throughout the year, increasing from approximately $30M in January to a peak of approximately $52M in December.

---

### Revenue Share by Store

**Chart Type:** Donut Chart

**Fields Used:**

* Store
* SalesDollars

> **Key Finding:**
> Revenue generation was distributed across multiple stores, with the highest-performing store contributing approximately 14.6% of total sales revenue.

---

## Inventory Analysis

### Top Products by Inventory Value

**Chart Type:** Horizontal Bar Chart

**Fields Used:**

* Description
* Inventory Value

> **Key Finding:**
> Jack Daniels No. 7 Black Label represented the highest inventory value at approximately $0.77M, followed by Jameson Irish Whiskey and Grey Goose Vodka.

---

### Top Products by Units on Hand

**Chart Type:** Horizontal Bar Chart

**Fields Used:**

* Description
* onHand

> **Key Finding:**
> Jameson Irish Whiskey held the highest inventory quantity at approximately 18.4K units, followed by Ketel One Vodka and Captain Morgan Spiced Rum.

---

### Inventory Value by Store

**Chart Type:** Donut Chart

**Fields Used:**

* Store
* Inventory Value

> **Key Finding:**
> Store 50 held the highest inventory value at approximately $4.89M, representing the largest inventory share among all store locations.

---

### Inventory Distribution by Store

**Chart Type:** Treemap

**Fields Used:**

* Store
* Inventory Value

> **Key Finding:**
> Inventory value was distributed across multiple stores, reducing reliance on a single location and supporting balanced inventory management.

---

# Filters and Interactive Features

### Implemented Features

* Cross-filtering between visuals
* Dynamic KPI calculations
* Interactive visual highlighting
* Date-based analysis using DateTable
* Dashboard page navigation
* Drill-down capabilities

### Available Filters

* Month
* Vendor
* Product
* Store

---

# Dashboard Design

The dashboards were designed using executive reporting principles to provide a clear and concise overview of business performance.

## Procurement Dashboard

* KPI Summary Section
* Vendor Analysis
* Product Analysis
* Procurement Trend Analysis
* Supplier Concentration Analysis

## Sales Dashboard

* KPI Summary Section
* Vendor Revenue Analysis
* Product Revenue Analysis
* Revenue Trend Analysis
* Store Performance Analysis

## Inventory Dashboard

* KPI Summary Section
* Inventory Value Analysis
* Inventory Quantity Analysis
* Store Inventory Analysis
* Inventory Distribution Analysis

---

# Overall Key Findings

* Total Procurement Spend reached **$321.90M** across **128 active vendors**.
* DIAGEO NORTH AMERICA INC represented the largest procurement supplier with approximately **$50.96M** in procurement spend.
* Total Sales Revenue reached **$452.06M** from approximately **33 million units sold**.
* Sales performance strengthened throughout the year, peaking at approximately **$52M** in December.
* Jack Daniels No. 7 Black Label emerged as the highest-performing product across procurement, sales revenue, and inventory value metrics.
* Total Inventory Value reached **$79.70M** across approximately **5 million inventory units**.
* Inventory was distributed across **80 active stores**, with Store 50 holding the highest inventory value at approximately **$4.89M**.
* Products with the highest inventory value were not always the products with the highest stock quantities, highlighting the difference between inventory investment and inventory volume.
* Procurement, sales, and inventory analyses collectively indicate strong performance among premium beverage products and key supplier relationships.

---

# Status

✅ Procurement Dashboard Completed

✅ Sales Dashboard Completed

✅ Inventory Dashboard Completed

✅ Dashboard Design Completed

✅ Interactive Features Implemented


