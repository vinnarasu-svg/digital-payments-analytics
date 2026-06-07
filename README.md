# 💳 Digital Payments Analytics Project

> End-to-end analytics project using **Snowflake SQL** and **Power BI** to uncover business insights from digital payment transactions.

---

## 📌 Project Overview

This project analyzes digital payment transaction data to generate actionable business insights across customers, merchants, banks, and cities. The goal is to simulate a real-world data analyst workflow — from raw data to interactive dashboards.

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| ❄️ Snowflake | Cloud SQL Database |
| 📊 Power BI | Interactive Dashboard |
| 🧠 SQL | Data Analysis & Querying |
| 📐 DAX | Calculated Measures in Power BI |

---

## 📁 Dataset

Four core tables used in this project:

| Table | Description |
|-------|-------------|
| `customer` | Customer demographics and location info |
| `merchant` | Merchant details and categories |
| `bank` | Bank information linked to customers |
| `transactions` | Payment records with amount, method, status |

---

## 🔍 SQL Analysis (30+ Questions)

### 💰 Revenue & Transaction Analysis
- Total revenue by merchant category
- Monthly revenue trend analysis
- Payment method-wise transaction breakdown

### 👤 Customer Analysis
- Top customers by total spending
- Customers with no successful transactions
- Customers using multiple payment methods
- Customer segmentation (High / Medium / Low spenders)

### 🏪 Merchant Analysis
- Top merchants by total revenue
- Top 2 merchants per category using Window Functions

### 🏙️ City & Bank Analysis
- Revenue breakdown by city
- Bank-wise customer revenue analysis

---

## 🧩 Key SQL Concepts Used

```sql
-- Joins, Aggregations, GROUP BY
-- CASE WHEN for segmentation
-- CTEs (WITH clause)
-- Subqueries
-- Window Functions: RANK(), ROW_NUMBER()
-- QUALIFY filter
-- Date functions for monthly trends
```

### 📌 Highlight Query — Top 2 Merchants per Category

```sql
WITH merchant_revenue AS (
    SELECT
        m.category,
        m.merchant_name,
        SUM(t.amount) AS total_revenue,
        RANK() OVER (PARTITION BY m.category ORDER BY SUM(t.amount) DESC) AS rnk
    FROM transactions t
    JOIN merchant m ON t.merchant_id = m.merchant_id
    WHERE t.status = 'Success'
    GROUP BY m.category, m.merchant_name
)
SELECT category, merchant_name, total_revenue
FROM merchant_revenue
WHERE rnk <= 2
ORDER BY category, rnk;
```

### 📌 Highlight Query — Customer Segmentation

```sql
WITH customer_spending AS (
    SELECT
        c.customer_id,
        c.customer_name,
        SUM(t.amount) AS total_spending
    FROM transactions t
    JOIN customer c ON t.customer_id = c.customer_id
    WHERE t.status = 'Success'
    GROUP BY c.customer_id, c.customer_name
)
SELECT
    customer_name,
    total_spending,
    CASE
        WHEN total_spending > 50000 THEN 'High Spender'
        WHEN total_spending BETWEEN 20000 AND 50000 THEN 'Medium Spender'
        ELSE 'Low Spender'
    END AS spending_segment
FROM customer_spending
ORDER BY total_spending DESC;
```

---

## 📊 Power BI Dashboard

### KPI Cards
- 💰 Total Revenue
- 👥 Total Customers
- 📈 Avg Transaction Value
- ✅ Success Transaction Count

### Visuals
- Revenue by Merchant Category *(Bar Chart)*
- Payment Method Distribution *(Pie/Donut Chart)*
- Monthly Revenue Trend *(Line Chart)*
- Top Customers by Spending *(Table/Bar)*

### Filters / Slicers
- 🏙️ City
- 🏪 Merchant Category
- 💳 Payment Method

---

## 💡 Business Insights

- Identified **top-performing merchant categories** driving majority of revenue
- Discovered **customer segments** to target for loyalty programs
- Tracked **monthly revenue trends** to spot growth and dips
- Analyzed **payment method preferences** across cities and demographics
- Flagged **customers with zero successful transactions** for re-engagement

---

## 📂 Project Structure

```
digital-payments-analytics/
│
├── sql/
│   ├── create_tables.sql        # Table creation scripts
│   ├── analysis_queries.sql     # 30+ analytical queries
│   └── advanced_queries.sql     # CTEs, Window Functions
│
├── powerbi/
│   └── digital_payments.pbix   # Power BI dashboard file
│
├── data/
│   ├── customer.csv
│   ├── merchant.csv
│   ├── bank.csv
│   └── transactions.csv
│
└── README.md
```

---

## 🚀 How to Run

1. **Snowflake Setup**
   - Create a free Snowflake trial account
   - Run `sql/create_tables.sql` to create tables
   - Load CSV data using Snowflake's data import tool
   - Run queries from `sql/analysis_queries.sql`

2. **Power BI Setup**
   - Open `powerbi/digital_payments.pbix` in Power BI Desktop
   - Connect to your Snowflake instance
   - Refresh data and explore the dashboard

---

## 🧠 Skills Demonstrated

`SQL` `Snowflake` `Power BI` `DAX` `Data Modeling` `Window Functions` `CTEs` `Customer Segmentation` `Revenue Analysis` `Trend Analysis` `Business Intelligence`

---

## 👨‍💻 Author

**[VINNARASU A]**  
Data Analyst | SQL • Power BI • Snowflake  
📧 [vinnarasutn49@gmail.com]  
🔗 [LinkedIn Profile:https://www.linkedin.com/in/vinnarasu-a-331434326?utm_source=share_via&utm_content=profile&utm_medium=member_android]  
🐙 [GitHub Profile:https://github.com/vinnarasu-svg]

---

markdown![Dashboard Preview](<img width="1125" height="636" alt="dashboard1 png" src="https://github.com/user-attachments/assets/28de2c97-7a6e-4a1e-9f57-ffcb07f4fa8c" />
)
markdown![Dashboard Preview](<img width="1903" height="906" alt="sql_quary png" src="https://github.com/user-attachments/assets/4233ea2e-a526-4a6b-9762-b4081830c7a8" />
)
