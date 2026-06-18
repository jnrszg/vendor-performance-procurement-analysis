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
#### Top Vendors by Procurement Spend
- A bar chart was created to identify vendors with the highest procurement spending. The analysis showed that DIAGEO NORTH AMERICA INC had the highest procurement spend, followed by MARTIGNETTI COMPANIES and JIM BEAM BRANDS COMPANY.
> Key Finding: Procurement spending is concentrated among a small number of vendors, with DIAGEO NORTH AMERICA INC representing the largest procurement spend.

#### Procurement Spending Trend
- A line chart was created to analyze procurement spending patterns over time. Procurement spending increased steadily during the first half of the year, peaking in July before fluctuating throughout the remaining months.
> Key Finding: Procurement activity remained strong throughout the year, with spending consistently exceeding $26 million during the second half of the year.

#### Vendor Spend Concentration
- A treemap was used to visualize the distribution of procurement spending across vendors. The chart highlighted that a relatively small group of suppliers accounted for a significant portion of total procurement spend.
> Key Finding: Procurement spending is moderately concentrated among key suppliers, emphasizing the importance of managing strategic vendor relationships and supplier dependency risks.
      
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
