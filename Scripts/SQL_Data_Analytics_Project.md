# SQL Data Analytics Project — Retail Sales Analysis

**Dataset:** Superstore Sales (retail orders, 2009–2012) — 8,399 order line items, 5,496 orders, 795 customers, 1,263 products, across 8 Canadian regions.
**Tools:** SQL (SQLite), applying the full EDA → Advanced Analytics framework.

This project runs the complete framework end-to-end on a real transactional dataset: Exploratory Data Analysis (database, dimension, data, and measure exploration; magnitude; ranking) followed by Advanced Analytics (time trends, cumulative analysis, performance analysis, part-to-whole, segmentation, and reporting).

---

## Part 1: Exploratory Data Analysis (EDA)

### 1. Database Exploration
```sql
SELECT COUNT(*) AS total_rows, COUNT(DISTINCT order_id) AS total_orders,
       COUNT(DISTINCT customer_name) AS total_customers,
       COUNT(DISTINCT product_name) AS total_products,
       MIN(order_date) AS first_order, MAX(order_date) AS last_order
FROM sales;
```
| total_rows | total_orders | total_customers | total_products | first_order | last_order |
|---|---|---|---|---|---|
| 8,399 | 5,496 | 795 | 1,263 | 2009-01-01 | 2012-12-30 |

### 2. Dimension Exploration
```sql
SELECT product_category, COUNT(DISTINCT product_subcategory) AS subcats,
       COUNT(DISTINCT product_name) AS products
FROM sales GROUP BY product_category;
```
| Category | Sub-categories | Products |
|---|---|---|
| Furniture | 4 | 257 |
| Office Supplies | 9 | 715 |
| Technology | 4 | 291 |

### 3. Data Exploration (region × segment)
Top combination: **Prairie / Corporate** — 690 orders, $1.29M in sales — narrowly ahead of West/Corporate ($1.22M).

### 4. Measure Exploration (the big numbers)
```sql
SELECT ROUND(SUM(sales),2) AS total_sales, ROUND(SUM(profit),2) AS total_profit,
       ROUND(AVG(sales),2) AS avg_order_value,
       ROUND(SUM(profit)*100.0/SUM(sales),2) AS profit_margin_pct
FROM sales;
```
| Total Sales | Total Profit | Avg Order Value | Profit Margin |
|---|---|---|---|
| $14.92M | $1.52M | $1,775.88 | **10.2%** |

### 5. Magnitude (by category)
| Category | Sales | Profit |
|---|---|---|
| Technology | $5.98M | $886K |
| Furniture | $5.18M | **$117K** |
| Office Supplies | $3.75M | $518K |

**🔑 Key finding:** Furniture generates the 2nd-highest sales but the *lowest* profit by a wide margin — its margin is only ~2.3% vs Technology's ~14.8%.

### 6. Ranking — Top-N / Bottom-N
- **Top product by sales:** Global Troy™ Executive Leather Low-Back Tilter — $275,942
- **Biggest loss-maker:** Okidata Pacemark 4410N Dot Matrix Printer — **–$43,949** profit

---

## Part 2: Advanced Analytics

### 7. Change-Over-Time Trends
| Year | Sales | Profit |
|---|---|---|
| 2009 | $4.21M | $434.5K |
| 2010 | $3.55M | $363.9K |
| 2011 | $3.44M | $381.5K |
| 2012 | $3.72M | $341.9K |

**🔑 Key finding:** Sales *declined* every year after a strong 2009, only recovering slightly in 2012 — but 2012 profit was the *lowest* of the four years despite higher sales, meaning profitability is eroding even where revenue holds up.

### 8. Cumulative Analysis
```sql
WITH yearly AS (SELECT substr(order_date,1,4) AS yr, SUM(sales) AS yr_sales FROM sales GROUP BY yr)
SELECT yr, ROUND(yr_sales,2), ROUND(SUM(yr_sales) OVER (ORDER BY yr),2) AS cumulative_sales
FROM yearly ORDER BY yr;
```
Cumulative sales reached **$14.92M by end of 2012**, using a SQL window function (`SUM() OVER`).

### 9. Performance Analysis
Technology outperforms the category average by **+$1.01M**; Office Supplies underperforms it by **–$1.22M** — despite Office Supplies having 9 sub-categories and 715 distinct products (far more SKUs than either other category).

### 10. Part-to-Whole
| Region | % of Total Sales |
|---|---|
| West | 24.1% |
| Ontario | 20.5% |
| Prairie | 19.0% |
| Atlantic | 13.5% |
| Quebec | 10.1% |
| Yukon | 6.5% |
| Northwest Territories | 5.4% |
| Nunavut | 0.8% |

**🔑 Key finding:** The top 3 regions (West, Ontario, Prairie) drive **63.7%** of all sales.

### 11. Data Segmentation
| Order Value Bucket | # Orders | Total Sales | Avg Profit/Order |
|---|---|---|---|
| Under $100 | 1,450 | $76.6K | **–$22.61** |
| $100–$500 | 2,920 | $709.1K | **–$48.79** |
| $500–$2,000 | 2,157 | $2.32M | $26.44 |
| $2,000+ | 1,872 | $11.81M | $876.06 |

**🔑 Key finding:** Orders under $500 are *net unprofitable on average* — every low-value order actively loses money, likely from shipping cost and discounting eating the margin.

### 12. Reporting
Executive summary table combining category × segment shows **Technology–Corporate** as the top revenue driver ($2.29M, 16.3% margin), while **Furniture–Corporate** brings in similar sales ($1.86M) at a razor-thin **1.18% margin**.

---

## Headline Insights (usable for resume/interviews)
1. Furniture is the least profitable category despite being the #2 revenue driver — margin is ~1–4% vs. ~13–16% for Technology.
2. Orders under $500 lose money on average; profitability only turns positive above the $500 order-value threshold.
3. Sales declined for 3 straight years (2009→2011) before a partial 2012 recovery, but profit kept falling even as sales ticked up.
4. Just 3 of 8 regions account for nearly two-thirds of total sales.

---

## Resume Bullets (with real numbers)

- Built a SQL analytics pipeline on an 8,400-row retail dataset ($14.9M in sales), applying EDA and advanced analytics (ranking, cumulative trends via window functions, segmentation) to identify that **Furniture carried a ~2% profit margin vs. ~15% for Technology** despite comparable revenue.
- Used SQL segmentation analysis to find that **orders under $500 were net unprofitable on average**, informing a data-backed recommendation to revisit minimum order thresholds or shipping cost allocation.
- Applied window functions and time-trend analysis in SQL to track a 3-year sales decline (2009–2011) and flag a profit-margin drop in 2012 despite a sales recovery — a signal missed by top-line revenue tracking alone.
