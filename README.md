# 🛍️ Customer Shopping Behavior Analysis

## 📌 Project Overview

This project analyzes customer shopping behavior using transactional data from **3,900 purchases** across multiple product categories. The goal is to uncover insights into spending patterns, customer segments, product preferences, and subscription behavior to guide strategic business decisions such as targeted discounting, retention campaigns, and inventory planning.

**Tech stack:** Python (Pandas) → SQL Server → Power BI

---

## 🗂️ Dataset Summary

| Attribute | Details |
|---|---|
| Rows | 3,900 |
| Columns | 18 |
| Missing Data | 37 values in `Review Rating` |

**Key features:**
- **Customer demographics:** Age, Gender, Location, Subscription Status
- **Purchase details:** Item Purchased, Category, Purchase Amount, Season, Size, Color
- **Shopping behavior:** Discount Applied, Promo Code Used, Previous Purchases, Frequency of Purchases, Review Rating, Shipping Type

---

## 🧹 1. Data Cleaning & Preparation (Python)

Performed using Pandas in a Jupyter notebook.

- **Data Loading:** Imported the dataset with Pandas
- **Initial Exploration:** Used `df.info()` and `df.describe()` to check structure and summary statistics
- **Missing Data Handling:** Imputed missing `Review Rating` values using the median rating per product category
- **Column Standardization:** Renamed all columns to `snake_case` for readability and consistency
- **Feature Engineering:**
  - Created `age_group` by binning customer ages
  - Created `purchase_frequency_days` from purchase frequency data
- **Data Consistency Check:** Verified redundancy between `discount_applied` and `promo_code_used`; dropped `promo_code_used`
- **Database Integration:** Loaded the cleaned DataFrame into PostgreSQL/SQL Server for downstream SQL analysis

<!-- Add a screenshot of df.info() / df.describe() output or notebook cell here -->

---

## 🗃️ 2. SQL Analysis (SQL Server)

Structured queries answering key business questions.
| # | Business Question | Key Finding |
|---|---|---|
| 1 | Revenue by gender | Male: $157,890 · Female: $75,191 |
| 2 | High-spending discount users | Customers using discounts who still spent above the average purchase amount |
| 3 | Top 5 products by review rating | Gloves (3.86), Sandals (3.84), Boots (3.82), Hat (3.8), Skirt (3.79) |
| 4 | Shipping type comparison | Standard: $58 avg · Express: $60 avg |
| 5 | Subscribers vs. non-subscribers | Subscribers: 1,053 customers, $62,645 total · Non-subscribers: 2,847 customers, $170,436 total |
| 6 | Discount-dependent products | Hat (50%), Coat (49%), Sneakers (49%), Sweater (48%), Pants (47%) |
| 7 | Customer segmentation | Loyal: 3,116 · Returning: 701 · New: 83 |
| 8 | Top 3 products per category | e.g., Jewelry (171), Blouse (171), Sandals (160) |
| 9 | Repeat buyers & subscription | 958 repeat buyers are subscribers vs. 2,518 are not |
| 10 | Revenue by age group | Young Adult ($62,143) leads, followed by Middle-aged, Adult, Senior |

<!-- Add a screenshot of a key SQL query + result table here -->

---

## 📊 3. Power BI Dashboard

An interactive dashboard was built to visualize customer and sales insights for stakeholders.

<img width="1299" height="735" alt="Screenshot 2026-09-04 190318" src="https://github.com/user-attachments/assets/c28f888b-c5ec-47c6-931b-d2c4166436fc" />

<!-- Add the full dashboard screenshot here (the one from the report) -->

**Dashboard highlights:**
- **3.9K** total customers · **$59.76** average purchase amount · **3.75** average review rating
- **27%** of customers are active subscribers
- Revenue and sales breakdown by **category** and **age group**
- Interactive filters: Subscription Status, Gender, Category, Shipping Type

---

## 💡 4. Key Insights

- Male customers generated significantly higher total revenue than female customers, suggesting a potential gender-skewed marketing opportunity.
- Non-subscribers contribute far more total revenue (~$170K) than subscribers (~$62K) despite subscribers having a comparable average spend — indicating subscription growth is an untapped lever.
- **Loyal customers** dominate the base (3,116 of 3,900), signaling strong retention but limited new-customer acquisition (only 83 new customers).
- Hats, coats, and sneakers are the most discount-dependent products, which may indicate price sensitivity in those categories.
- Young Adults are the highest revenue-contributing age group, closely followed by Middle-aged customers.

---

## 🛠️ Tools & Technologies

`Python` · `Pandas` · `PostgreSQL / SQL Server` · `Power BI` · `DAX`

---

## 📁 Repository Structure

```
customer-shopping-behavior-analysis/
├── data/
│   └── customer_shopping_data.csv
├── notebooks/
│   └── data_cleaning.ipynb
├── sql/
│   └── analysis_queries.sql
├── powerbi/
│   └── customer_behavior_dashboard.pbix
├── images/
│   ├── dashboard_banner.png
│   ├── data_cleaning.png
│   ├── sql_results.png
│   └── powerbi_dashboard.png
└── README.md
```

---

## 🚀 How to Reproduce

1. Clone this repository
2. Run the Python notebook in `notebooks/` to clean and prepare the data
3. Load the cleaned data into SQL Server and run the queries in `sql/analysis_queries.sql`
4. Open `powerbi/customer_behavior_dashboard.pbix` in Power BI Desktop to explore the dashboard

---

## 👤 Author

**Bimal**
_Final-year, Department of Materials Science and Engineering, IIT Kanpur_

