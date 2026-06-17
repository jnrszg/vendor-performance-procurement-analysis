## DASHBOARD DEVELOPMENT

---

## Objective
The goal of this phase is to create an interactive Power BI dashboard that presents procurement, sales, product, and inventory insights in a clear and meaningful way.

---

## Dashboard Requirements
### KPI Measures
The dashboard will include key performance indicators (KPIs) to provide a high-level overview of business performance.

Planned KPIs:
* Total Procurement Spend
* Total Sales Revenue
* Total Inventory Value
* Total Vendors

## Dashboard Progress

### KPI Measures Created

| KPI                     | Measure                                                           |
| ----------------------- | ----------------------------------------------------------------- |
| Total Procurement Spend | SUM(purchases[Dollars])                                           |
| Total Sales Revenue     | SUM(sales[SalesDollars])                                          |
| Total Vendors           | DISTINCTCOUNT(purchases[VendorName])                              |
| Total Inventory Value   | SUMX(end_inventory, end_inventory[onHand] * end_inventory[Price]) |

### KPI Results

| KPI                     |   Value |
| ----------------------- | ------: |
| Total Procurement Spend | 321.90M |
| Total Sales Revenue     | 452.06M |
| Total Vendors           |     128 |
| Total Inventory Value   |  79.70M |

Status: ✅ Completed

---

### Visualizations
The dashboard will include visualizations to support the business questions explored during the analysis.

Planned Visualizations:

#### Procurement Analysis
* Top Vendors by Procurement Spend
 > Key Finding: Procurement spending is concentrated among a small number of vendors. DIAGEO NORTH AMERICA INC is the largest supplier, with procurement spending significantly higher than the remaining vendors.
* Procurement Spending Trend
* Vendor Spend Concentration
      
#### Sales Analysis
* Top Vendors by Sales Revenue
* Sales Revenue Trend
* Procurement Spend vs Sales Revenue

#### Product & Inventory Analysis
* Top Products by Sales Revenue
* Top Products by Inventory Value
* Inventory Value vs Sales Activity

### Filters and Interactive Features
Planned Filters:
* Vendor
* Product
* Month

These filters will allow users to explore the data and interact with dashboard visuals.

## Dashboard Design
The dashboard will be designed as an executive summary view that highlights key metrics, trends, and performance indicators.

Planned Layout:
1. KPI Summary Section
2. Procurement Analysis Section
3. Sales Analysis Section
4. Product & Inventory Analysis Section

## Status

🚧 In Progress
