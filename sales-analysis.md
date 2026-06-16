### SALES ANALYSIS

---

### Objective
The goal of this analysis is to evaluate sales performance, identify vendors generating the highest sales value, analyze sales trends over time, and compare procurement spending with sales revenue.

---

### Business Questions
1. Which vendors generate the highest sales value?
2. What are the sales trends over time?
3. How does procurement spending compare with sales revenue?

---

## 1. Vendors Generating the Highest Sales Value
To identify the vendors that generated the highest sales value, I calculated total sales revenue for each vendor and ranked them from highest to lowest.

```sql
SELECT
    VendorName,
    ROUND(SUM(SalesDollars), 2) AS TotalSales
FROM sales
GROUP BY VendorName
ORDER BY TotalSales DESC
LIMIT 10;
```

### Results
| Vendor Name | Total Sales ($) |
|------------|----------------:|
| DIAGEO NORTH AMERICA INC | 68,742,416.99 |
| MARTIGNETTI COMPANIES | 40,992,395.93 |
| PERNOD RICARD USA | 32,281,247.95 |
| JIM BEAM BRANDS COMPANY | 31,906,320.54 |
| BACARDI USA INC | 25,014,556.89 |
| CONSTELLATION BRANDS INC | 24,469,172.93 |
| E & J GALLO WINERY | 18,556,085.61 |
| BROWN-FORMAN CORP | 18,478,557.47 |
| ULTRA BEVERAGE COMPANY LLP | 17,822,938.45 |
| M S WALKER INC | 15,465,247.75 |

### Observation
DIAGEO NORTH AMERICA INC generated the highest sales value, with more than $68.7 million in sales revenue. MARTIGNETTI COMPANIES ranked second with approximately $41.0 million in sales.
Several vendors that ranked highest in procurement spending also ranked highest in sales value, suggesting that the company's largest suppliers contribute significantly to overall revenue generation.

### Insight
The results indicate that sales revenue is concentrated among a relatively small group of major vendors. Monitoring the performance of these vendors is important because they have a substantial impact on overall business revenue.

## 2. Sales Trends Over Time
To understand how sales performance changed over time, I calculated total sales revenue by month.

```sql
SELECT
    strftime('%Y-%m', SalesDate) AS Month,
    ROUND(SUM(SalesDollars), 2) AS TotalSales
FROM sales
GROUP BY strftime('%Y-%m', SalesDate)
ORDER BY Month;
```

### Results
| Month | Total Sales ($) |
|---------|----------------:|
| 2024-01 | 29,854,027.92 |
| 2024-02 | 28,876,607.23 |
| 2024-03 | 28,988,411.94 |
| 2024-04 | 30,723,734.63 |
| 2024-05 | 36,041,210.52 |
| 2024-06 | 39,290,701.46 |
| 2024-07 | 49,696,466.85 |
| 2024-08 | 39,056,166.03 |
| 2024-09 | 38,477,538.83 |
| 2024-10 | 36,433,141.73 |
| 2024-11 | 42,312,696.86 |
| 2024-12 | 52,312,248.02 |

### Observation
Sales revenue remained relatively stable during the first quarter of 2024, averaging approximately $29 million per month.
Revenue increased steadily from April through July, reaching nearly $49.7 million in July. After a temporary decline between August and October, sales increased again and reached their highest level in December at approximately $52.3 million.

### Insight
The business experienced stronger sales performance during the second half of the year, particularly in July and December. This pattern may indicate seasonal demand, promotional activity, or inventory planning that supports increased sales during peak periods.

## 3. Compare Procurement Spending with Sales Revenue
To compare purchasing activity with sales performance, I calculated monthly procurement spending, monthly sales revenue, and the sales-to-spend ratio.

```sql
SELECT
    p.Month,
    p.ProcurementSpend,
    s.SalesRevenue,
    ROUND(s.SalesRevenue / p.ProcurementSpend, 2) AS SalesToSpendRatio
FROM
(
    SELECT
        strftime('%Y-%m', PODate) AS Month,
        SUM(Dollars) AS ProcurementSpend
    FROM purchases
    GROUP BY strftime('%Y-%m', PODate)
) p
JOIN
(
    SELECT
        strftime('%Y-%m', SalesDate) AS Month,
        SUM(SalesDollars) AS SalesRevenue
    FROM sales
    GROUP BY strftime('%Y-%m', SalesDate)
) s
ON p.Month = s.Month
ORDER BY p.Month;
```

### Results
| Month | Procurement Spend ($) | Sales Revenue ($) | Sales-to-Spend Ratio |
|---------|---------------------:|------------------:|---------------------:|
| 2024-01 | 19,138,815.42 | 29,854,027.92 | 1.56 |
| 2024-02 | 20,147,364.53 | 28,876,607.23 | 1.43 |
| 2024-03 | 20,252,968.80 | 28,988,411.94 | 1.43 |
| 2024-04 | 21,798,729.53 | 30,723,734.63 | 1.41 |
| 2024-05 | 28,693,060.33 | 36,041,210.52 | 1.26 |
| 2024-06 | 29,699,192.07 | 39,290,701.46 | 1.32 |
| 2024-07 | 32,193,842.50 | 49,696,466.85 | 1.54 |
| 2024-08 | 30,747,883.70 | 39,056,166.03 | 1.27 |
| 2024-09 | 26,840,919.81 | 38,477,538.83 | 1.43 |
| 2024-10 | 31,836,531.74 | 36,433,141.73 | 1.14 |
| 2024-11 | 27,252,267.02 | 42,312,696.86 | 1.55 |
| 2024-12 | 26,349,072.86 | 52,312,248.02 | 1.99 |

### Observation
Sales revenue exceeded procurement spending in every month reviewed. The sales-to-spend ratio ranged from 1.14 in October to 1.99 in December.
December recorded the highest sales revenue and the highest sales-to-spend ratio, indicating that nearly two dollars of sales revenue were generated for every dollar spent on procurement during that month.

### Insight
The business consistently generated more sales revenue than procurement spending throughout the year. The strong sales-to-spend ratios observed in November and December may indicate increased demand during the holiday season or improved inventory utilization during the final months of the year.

## Sales Analysis Summary
- The analysis showed that sales revenue was concentrated among a small group of major vendors, with DIAGEO NORTH AMERICA INC generating the highest sales value.
- Sales performance strengthened during the second half of 2024, with revenue peaking in December at over $52 million.
- Comparing procurement spending with sales revenue showed that sales consistently exceeded procurement costs throughout the year. The strongest performance occurred in November and December, when the sales-to-spend ratio reached its highest levels.
- These findings suggest that procurement activity generally supported sales growth and that the business achieved particularly strong revenue generation during the final months of the year.
