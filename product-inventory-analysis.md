## Product & Inventory Analysis

---

## Objective
The goal of this analysis is to evaluate product purchasing costs, sales performance, and inventory levels to identify high-value products and assess whether inventory investment supports sales activity.

---

## Business Questions
1. Identify products with the highest purchase cost.
2. Identify products generating the highest sales revenue.
3. Calculate inventory value.
4. Review inventory levels against sales activity.

---

## 1. Identify Products with the Highest Purchase Cost
To identify the most expensive products purchased by the business, I reviewed the highest recorded purchase price for each product and ranked them from highest to lowest.

```sql
SELECT
    Description,
    MAX(PurchasePrice) AS HighestPurchasePrice
FROM purchase_prices
GROUP BY Description
ORDER BY HighestPurchasePrice DESC
LIMIT 10;
```

### Results
| Product                      | Highest Purchase Price ($) |
| ---------------------------- | -------------------------: |
| Glen Grant 50 Yr Scotch      |                  11,111.03 |
| Patron En Lalique Tequila    |                   5,681.81 |
| Glenmorangie Pride           |                   4,264.70 |
| The Macallan M Decanter      |                   3,787.87 |
| Appleton Estate 50Yr Old Rum |                   3,649.63 |
| Hennessy Richard Cognac      |                   3,352.93 |
| Highland Park 1968           |                   3,149.60 |
| Armand De Brignac Brut       |                   2,816.43 |
| Glenfiddich 1978 Rare Collct |                   2,713.17 |
| Port Ellen 32 Yr Single Malt |                   2,661.86 |

### Observation
The highest purchase prices were associated with premium and luxury alcoholic beverages. Glen Grant 50 Yr Scotch recorded the highest purchase price at $11,111.03, which was significantly higher than the other products in the dataset.

### Insight
The results indicate that the business carries a selection of ultra-premium products that require substantial procurement investment. Although these products represent a higher purchasing cost, further analysis is required to determine whether they also generate significant sales revenue.

## 2. Identify Products Generating the Highest Sales Revenue
To identify the products generating the most sales revenue, I calculated total sales revenue for each product and ranked them from highest to lowest.

```sql id="n6mrwz"
SELECT
    Description,
    ROUND(SUM(SalesDollars), 2) AS TotalRevenue
FROM sales
GROUP BY Description
ORDER BY TotalRevenue DESC
LIMIT 10;
```

### Results
| Product                 | Total Revenue ($) |
| ----------------------- | ----------------: |
| Jack Daniels No 7 Black |      7,964,746.76 |
| Tito's Handmade Vodka   |      7,399,657.58 |
| Grey Goose Vodka        |      7,209,608.06 |
| Capt Morgan Spiced Rum  |      6,356,320.62 |
| Absolut 80 Proof        |      6,244,752.03 |
| Jameson Irish Whiskey   |      5,715,759.69 |
| Ketel One Vodka         |      5,070,083.56 |
| Baileys Irish Cream     |      4,150,122.07 |
| Kahlua                  |      3,604,858.66 |
| Tanqueray               |      3,456,697.90 |

### Observation
Jack Daniels No 7 Black generated the highest sales revenue at approximately $8.0 million, followed by Tito's Handmade Vodka and Grey Goose Vodka. Several vodka and whiskey products appeared among the top revenue-generating products.

### Insight
Unlike the products identified in the purchase cost analysis, the highest revenue-generating products were well-known, high-volume brands rather than ultra-premium products. This suggests that overall sales performance is driven by consistent customer demand for popular products.

## 6. Calculate Inventory Value
To identify products representing the largest inventory investment, I calculated inventory value by multiplying the quantity on hand by the unit price for each product and then ranked the products from highest to lowest inventory value.

```sql id="h7my4v"
SELECT
    Description,
    ROUND(SUM(onHand * Price), 2) AS InventoryValue
FROM end_inventory
GROUP BY Description
ORDER BY InventoryValue DESC
LIMIT 10;
```

### Results
| Product                    | Inventory Value ($) |
| -------------------------- | ------------------: |
| Jack Daniels No 7 Black    |          765,644.15 |
| Jameson Irish Whiskey      |          676,376.48 |
| Grey Goose Vodka           |          673,562.31 |
| Ketel One Vodka            |          654,236.05 |
| Johnnie Walker Black Label |          572,597.19 |
| Absolut 80 Proof           |          558,339.11 |
| Baileys Irish Cream        |          519,834.37 |
| Tito's Handmade Vodka      |          509,569.12 |
| Kahlua                     |          500,651.96 |
| Capt Morgan Spiced Rum     |          496,688.01 |

### Observation
Jack Daniels No 7 Black had the highest inventory value at approximately $765,644, followed by Jameson Irish Whiskey and Grey Goose Vodka. Several products appearing in the inventory value analysis were also identified among the highest revenue-generating products.

### Insight
The results suggest that the business maintains significant inventory investment in products that generate strong sales revenue. This alignment may help support product availability and meet customer demand for popular items.

## 4. Review Inventory Levels Against Sales Activity
To review inventory levels against sales activity, I compared inventory value and sales revenue for products to determine whether inventory investment aligns with product performance.

```sql
SELECT
    ei.Description,
    ROUND(SUM(ei.onHand * ei.Price), 2) AS InventoryValue,
    ROUND(COALESCE(s.TotalSalesRevenue, 0), 2) AS SalesRevenue
FROM end_inventory ei
LEFT JOIN
(
    SELECT
        Description,
        SUM(SalesDollars) AS TotalSalesRevenue
    FROM sales
    GROUP BY Description
) s
ON ei.Description = s.Description
GROUP BY ei.Description
ORDER BY InventoryValue DESC
LIMIT 10;
```

### Results
| Product                    | Inventory Value ($) | Sales Revenue ($) |
| -------------------------- | ------------------: | ----------------: |
| Jack Daniels No 7 Black    |          765,644.15 |      7,964,746.76 |
| Jameson Irish Whiskey      |          676,376.48 |      5,715,759.69 |
| Grey Goose Vodka           |          673,562.31 |      7,209,608.06 |
| Ketel One Vodka            |          654,236.05 |      5,070,083.56 |
| Johnnie Walker Black Label |          572,597.19 |      2,409,134.67 |
| Absolut 80 Proof           |          558,339.11 |      6,244,752.03 |
| Baileys Irish Cream        |          519,834.37 |      4,150,122.07 |
| Tito's Handmade Vodka      |          509,569.12 |      7,399,657.58 |
| Kahlua                     |          500,651.96 |      3,604,858.66 |
| Capt Morgan Spiced Rum     |          496,688.01 |      6,356,320.62 |

### Observation
Several products with the highest inventory values also generated strong sales revenue. Products such as Jack Daniels No 7 Black, Grey Goose Vodka, Tito's Handmade Vodka, Absolut 80 Proof, and Capt Morgan Spiced Rum appeared among both the highest inventory value products and the highest revenue-generating products.

### Insight
The results suggest that inventory investment is generally aligned with sales activity. Products receiving the largest inventory investment are also among the products generating the highest sales revenue, indicating that inventory levels are being maintained to support customer demand and product availability.

## Product & Inventory Analysis Summary
- The analysis showed that the products with the highest purchase costs were premium and luxury spirits, while the products generating the highest sales revenue were popular, high-demand brands.
- Products such as Jack Daniels No 7 Black, Jameson Irish Whiskey, and Grey Goose Vodka appeared among the top products for both inventory value and sales revenue.
- Overall, the results suggest that inventory levels are generally aligned with sales activity, helping ensure that high-demand products remain available to customers.
