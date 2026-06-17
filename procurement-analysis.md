## PROCUREMENT ANALYSIS

---

### Objective
The goal of this analysis is to understand procurement spending patterns, identify key suppliers, and evaluate whether procurement spending is concentrated among a small number of vendors.

---

### Business Questions
1. Which vendors account for the highest procurement spending?
2. How does procurement spending change over time?
3. Is procurement spending concentrated among a small number of vendors?

---

## 1. Vendors with the Highest Procurement Spending
To identify the vendors that received the most procurement spending, I calculated the total purchase dollars for each vendor and ranked them from highest to lowest.

```sql
SELECT
    VendorName,
    ROUND(SUM(Dollars), 2) AS TotalSpend
FROM purchases
GROUP BY VendorName
ORDER BY TotalSpend DESC
LIMIT 10;
```

### Results
| Vendor Name | Total Spend ($) |
|------------|----------------:|
| DIAGEO NORTH AMERICA INC | 50,959,796.85 |
| MARTIGNETTI COMPANIES | 27,821,473.91 |
| JIM BEAM BRANDS COMPANY | 24,203,151.05 |
| PERNOD RICARD USA | 24,124,091.56 |
| BACARDI USA INC | 17,624,378.72 |
| CONSTELLATION BRANDS INC | 15,573,917.90 |
| BROWN-FORMAN CORP | 13,529,433.08 |
| ULTRA BEVERAGE COMPANY LLP | 13,210,613.93 |
| E & J GALLO WINERY | 12,289,608.09 |
| M S WALKER INC | 10,935,817.30 |

### Observation
DIAGEO NORTH AMERICA INC had the highest procurement spending, with total purchases of more than $50 million.
The results also show that a few vendors account for a large portion of the company's procurement spending. The top 10 vendors all had purchase totals above $10 million.

### Insight
Based on the results, procurement spending is not evenly distributed across vendors. A small number of vendors account for a large share of total purchases, with DIAGEO NORTH AMERICA INC being the largest supplier.

## 2. Procurement Spending Trends Over Time
To understand how procurement spending changed over time, I calculated total purchase spending by month.

```sql
SELECT
    strftime('%Y-%m', PODate) AS Month,
    ROUND(SUM(Dollars), 2) AS TotalSpend
FROM purchases
GROUP BY strftime('%Y-%m', PODate)
ORDER BY Month;
```

### Results
| Month | Total Spend ($) |
|---------|----------------:|
| 2023-12 | 6,950,117.22 |
| 2024-01 | 19,138,815.42 |
| 2024-02 | 20,147,364.53 |
| 2024-03 | 20,252,968.80 |
| 2024-04 | 21,798,729.53 |
| 2024-05 | 28,693,060.33 |
| 2024-06 | 29,699,192.07 |
| 2024-07 | 32,193,842.50 |
| 2024-08 | 30,747,883.70 |
| 2024-09 | 26,840,919.81 |
| 2024-10 | 31,836,531.74 |
| 2024-11 | 27,252,267.02 |
| 2024-12 | 26,349,072.86 |

### Observation
Procurement spending increased steadily during the first half of 2024, rising from approximately $19.1 million in January to $32.2 million in July.
Spending peaked in July 2024 before declining slightly during the remaining months of the year. Despite the decline, monthly procurement spending remained above $26 million from May through December.

### Insight
The business appears to increase purchasing activity during the middle of the year, potentially to support higher inventory demand. Procurement spending remained relatively strong throughout 2024, indicating consistent purchasing activity across the period analyzed.

## 3. Vendor Concentration Analysis
To determine whether procurement spending was concentrated among a small number of vendors, I calculated each vendor's percentage share of total procurement spending.

```sql
SELECT
    VendorName,
    ROUND(SUM(Dollars), 2) AS TotalSpend,
    ROUND(
        SUM(Dollars) * 100.0 /
        (SELECT SUM(Dollars) FROM purchases),
        2
    ) AS SpendPercent
FROM purchases
GROUP BY VendorName
ORDER BY TotalSpend DESC
LIMIT 10;
```

### Results
| Vendor Name | Total Spend ($) | Spend Share (%) |
|------------|----------------:|----------------:|
| DIAGEO NORTH AMERICA INC | 50,959,796.85 | 15.83 |
| MARTIGNETTI COMPANIES | 27,821,473.91 | 8.64 |
| JIM BEAM BRANDS COMPANY | 24,203,151.05 | 7.52 |
| PERNOD RICARD USA | 24,124,091.56 | 7.49 |
| BACARDI USA INC | 17,624,378.72 | 5.48 |
| CONSTELLATION BRANDS INC | 15,573,917.90 | 4.84 |
| BROWN-FORMAN CORP | 13,529,433.08 | 4.20 |
| ULTRA BEVERAGE COMPANY LLP | 13,210,613.93 | 4.10 |
| E & J GALLO WINERY | 12,289,608.09 | 3.82 |
| M S WALKER INC | 10,935,817.30 | 3.40 |

### Observation
DIAGEO NORTH AMERICA INC accounted for approximately 15.8% of total procurement spending, making it the company's largest supplier by a significant margin.
The top 10 vendors collectively accounted for approximately 65% of total procurement spending, indicating that a large portion of purchasing activity was concentrated among a relatively small group of suppliers.

### Insight
Procurement spending is moderately concentrated among a small number of key vendors. While these suppliers likely provide important products and purchasing efficiencies, the business may face increased supply chain risk if it becomes overly dependent on a limited number of vendors.

## Procurement Analysis Summary
- The analysis showed that procurement spending is concentrated among a small number of vendors, with DIAGEO NORTH AMERICA INC being the largest supplier. Procurement spending increased during 2024 and remained consistently high throughout the year.
- Overall, the findings suggest that the business relies on key suppliers to support its purchasing and inventory requirements.
