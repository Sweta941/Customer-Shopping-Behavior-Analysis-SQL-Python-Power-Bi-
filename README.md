# 🛍️ Customer Shopping Behaviour Analysis

An end-to-end data analysis project exploring customer shopping patterns through **Python** (data cleaning & feature engineering), **SQL** (business insights), and **Power BI** (interactive dashboard).

---

## 📁 Project Structure

```
Customer-Shopping-Behaviour-Analysis/
│
├── Customer_Shopping_Behaviour_Analysis.ipynb   # Python: data cleaning & MySQL export
├── SQL_script.sql                               # SQL: business questions & queries
├── Customer_Behavior_Dashboard.pbix             # Power BI: interactive dashboard
└── README.md
```

---

## 📊 Dataset

The dataset contains customer-level shopping records with the following attributes:

| Feature | Description |
|---|---|
| `customer_id` | Unique customer identifier |
| `age` | Customer age |
| `gender` | Male / Female |
| `item_purchased` | Product name |
| `category` | Product category |
| `purchase_amount` | Purchase value in USD |
| `review_rating` | Customer review score |
| `subscription_status` | Whether the customer is subscribed |
| `shipping_type` | Shipping method (Standard, Express, etc.) |
| `discount_applied` | Whether a discount was used |
| `frequency_of_purchases` | Purchase cadence (Weekly, Monthly, etc.) |
| `previous_purchases` | Count of past purchases |

---

## 🐍 Phase 1 — Python: Data Cleaning & Feature Engineering

**Notebook:** `Customer_Shopping_Behaviour_Analysis.ipynb`

### Steps Performed

**1. Exploratory Data Overview**
- Loaded the dataset using `pandas`
- Inspected shape, data types, and descriptive statistics with `.info()` and `.describe()`

**2. Handling Missing Values**
- Identified null values using `.isnull().sum()`
- Imputed missing `review_rating` values with the **median per category** using `groupby` + `transform`

**3. Column Standardisation**
- Converted all column names to lowercase with underscores for SQL compatibility
- Renamed `purchase_amount_(usd)` → `purchase_amount`

**4. Feature Engineering**
- **`age_group`** — Segmented customers into four quartile-based groups using `pd.qcut()`:
  - Young Adult · Adult · Middle-aged · Senior
- **`purchase_frequency_days`** — Mapped text-based purchase frequency to numeric values (e.g. `"Weekly"` → `7`, `"Monthly"` → `30`)

**5. Removing Redundant Columns**
- Verified that `discount_applied` and `promo_code_used` were identical columns (`100%` match)
- Dropped `promo_code_used` to eliminate redundancy

**6. Loading to MySQL**
- Connected to a local MySQL database (`customer_behavior_db`) using `SQLAlchemy` + `PyMySQL`
- Exported the cleaned DataFrame to a `customer` table for SQL analysis

---

## 🗄️ Phase 2 — SQL: Business Questions

**Script:** `SQL_script.sql`  
**Database:** MySQL (`customer_behavior_db`)

Ten business questions were answered using SQL queries:

| # | Business Question | Techniques Used |
|---|---|---|
| Q1 | Total revenue by gender | `GROUP BY`, `SUM` |
| Q2 | Discount users who spent above average | Subquery, `WHERE` filter |
| Q3 | Top 5 products by average review rating | `GROUP BY`, `ROUND`, `ORDER BY` |
| Q4 | Average purchase amount: Standard vs Express shipping | Conditional `WHERE`, `GROUP BY` |
| Q5 | Do subscribers spend more? | `COUNT`, `AVG`, `SUM`, `GROUP BY` |
| Q6 | Top 5 products with highest discount rate | `CASE WHEN`, percentage calculation |
| Q7 | Customer segmentation: New / Returning / Loyal | CTE, `CASE WHEN` |
| Q8 | Top 3 products per category | CTE, `ROW_NUMBER()` window function |
| Q9 | Are repeat buyers more likely to subscribe? | Filtered `GROUP BY` |
| Q10 | Revenue contribution by age group | `GROUP BY`, `SUM`, `ORDER BY` |

---

## 📈 Phase 3 — Power BI Dashboard

**File:** `Customer_Behavior_Dashboard.pbix`

An interactive dashboard was built in Power BI to visualise key findings, including revenue breakdowns by gender and age group, subscription impact on spending, product performance, and discount behaviour patterns.

![image alt](https://github.com/Sweta941/E-Commerce-Data-Analysis-Using-MySQL-/blob/31bf2074ee3ceed8b275cabe231753768ce41953/Screenshot%20(71).png)
---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| Python (pandas) | Data cleaning & feature engineering |
| SQLAlchemy / PyMySQL | Python → MySQL connection |
| MySQL | Data storage & business analysis |
| Power BI | Interactive dashboard |

---

## 🚀 Getting Started

### Prerequisites
```
Python 3.x
MySQL Server
Power BI Desktop
```

### Installation
```bash
pip install pandas sqlalchemy pymysql
```

### Steps to Reproduce

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/customer-shopping-behaviour-analysis.git
   cd customer-shopping-behaviour-analysis
   ```

2. **Run the Jupyter Notebook**  
   Open `Customer_Shopping_Behaviour_Analysis.ipynb` and update the MySQL credentials and dataset path, then run all cells to clean the data and load it into MySQL.

3. **Run SQL Queries**  
   Open `SQL_script.sql` in MySQL Workbench (or any MySQL client) and execute the queries against `customer_behavior_db`.

4. **Open the Dashboard**  
   Open `Customer_Behavior_Dashboard.pbix` in Power BI Desktop.

---

## 🔑 Key Insights

- **Subscribed customers** generate significantly higher total revenue despite similar average spend per transaction.
- Customers with **more than 5 previous purchases** are more likely to hold an active subscription.
- The **Middle-aged and Adult** segments contribute the most revenue across all age groups.
- Several top-selling products show high **discount dependency**, suggesting pricing strategy opportunities.
- **Standard and Express shipping** show comparable average purchase amounts, indicating shipping choice isn't strongly tied to spend level.

----

## 🙋 Author

**Sweta Mehta**

Data Analyst | Data Science Portfolio Project
