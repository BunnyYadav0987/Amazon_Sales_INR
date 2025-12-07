# Amazon_Sales_INR
Amazon Sales 2025 analytics built in Databricks. Includes ingestion, cleaning, feature engineering, PySpark notebook analysis, SQL insights, Delta tables, and an interactive dashboard showing revenue by category/state, payment method distribution, KPIs, and customer rating trends.

 Perfect — now that all files for **Venu’s Amazon Sales Project** are uploaded and the dashboard JSON metadata is fully parsed (including all SQL queries, KPIs, and filters), I can generate:

1️⃣ **A GitHub repo description (<350 characters)**
2️⃣ **A complete professional README.md**
— matching your style
— matching your professor’s structure (4.1 → 4.6)
— matching the fact that **all files are stored directly in the main branch**
— referencing the exact SQL queries extracted from the dashboard JSON (with citations as required).

Here it is:

---

# ✅ **1. Repo Description (<350 characters)**

**Amazon Sales 2025 analytics built in Databricks. Includes ingestion, cleaning, feature engineering, PySpark notebook analysis, SQL insights, Delta tables, and an interactive dashboard showing revenue by category/state, payment method distribution, KPIs, and customer rating trends.**



# 📘 **Amazon Sales 2025 – INR Analytics Project (Venu)**

This repository contains a complete Databricks-based **Amazon Sales Analysis** project for the module **Unlocking the Power of Big Data (MADSC102)**.
It includes **data ingestion, transformation, PySpark analysis, SQL analytics, Delta Lake storage, and a fully interactive dashboard**.

---

# 📁 **Repository Contents (All Files in Main Branch)**

| File                                              | Description                                                               |
| ------------------------------------------------- | ------------------------------------------------------------------------- |
| **amazon_sales_2025_INR.csv**                     | Original sales dataset used for ingestion                                 |
| **Amazon_sales_Notebook.ipynb**                   | PySpark notebook for cleaning, feature engineering, and notebook analysis |
| **SQL_Quries_NOTEBOOK.ipynb**                     | SQL analysis used for dashboard visuals                                   |
| **Amazon Sales 2025 – INR Dashboard.lvdash.json** | Dashboard export including visuals, KPIs, layout, and filters             |
| **README.md**                                     | Documentation for the full project                                        |

---

# 📊 **Dataset Description**

The dataset includes transactional Amazon order information such as:

* Product Category
* State
* Quantity
* Unit Price
* Total Sales (INR)
* Payment Method
* Review Rating
* Order ID
* Order Date

This supports analysis of **revenue trends**, **customer spending patterns**, **regional performance**, **payment preferences**, and **ratings-based insights**.

---

# 🧵 **1. Data Ingestion (Requirement 4.1)**

The CSV file was uploaded into Databricks via:

**Create Table → Upload File → Add to Catalog (workspace.amazon_project)**

Accessed in PySpark using:

```python
spark.sql("USE CATALOG workspace")
spark.sql("USE SCHEMA amazon_project")
df_raw = spark.table("amazon_sales_raw")
```

---

# 🧼 **2. Data Cleaning & Feature Engineering (4.2)**

Performed inside **Amazon_sales_Notebook.ipynb**.

### ✔ Cleaning steps:

* Converted data types (dates, numbers, categories)
* Corrected `Total_Sales_INR` for missing or zero values
* Removed unusable rows
* Standardized categorical fields

### ✔ Engineered fields:

* **Order_Month** (YYYY-MM formatted)
* **Total_Sales_INR recalculated** (Quantity × Unit Price if needed)
* **Rating Band** (High / Medium / Low)
* **Revenue_Per_Unit**
* **Region-level grouping**

These fields support SQL analytics and dashboards.

---

# 💾 **3. Delta Table Storage (4.3)**

The final cleaned dataset was written as a Delta table:

```python
df_clean.write.format("delta")
  .mode("overwrite")
  .saveAsTable("workspace.amazon_project.amazon_sales_clean")
```

This ensures high performance, ACID transactions, and optimized dashboard querying.

---

# 📘 **4. Notebook Analysis (4.5)**

Inside **Amazon_sales_Notebook.ipynb**, your analysis included:

* Summary statistics
* Revenue distribution
* Category-level insights
* **Notebook visualization:** Monthly Revenue Trend chart (Order Month vs Total Sales)

This satisfies the notebook analysis requirement.

---

# 🧮 **5. SQL Analysis (4.4)**

All SQL queries are inside **SQL_Quries_NOTEBOOK.ipynb**, and the dashboard export confirms which were used.

Below are the **actual SQL queries extracted from the dashboard JSON**:

---

### ⭐ Revenue by Product Category



```sql
SELECT
  Product_Category,
  ROUND(SUM(Total_Sales_INR), 2) AS total_revenue,
  COUNT(DISTINCT Order_ID) AS num_orders
FROM amazon_sales_clean
GROUP BY Product_Category
ORDER BY total_revenue DESC;
```

---

### ⭐ Revenue by State



```sql
SELECT
  State,
  ROUND(SUM(Total_Sales_INR), 2) AS total_revenue,
  COUNT(DISTINCT Order_ID) AS num_orders
FROM amazon_sales_clean
GROUP BY State
ORDER BY total_revenue DESC;
```

---

### ⭐ Payment Method Distribution (Pie Chart)



```sql
SELECT
  Payment_Method,
  ROUND(SUM(Total_Sales_INR), 2) AS total_revenue,
  COUNT(DISTINCT Order_ID) AS num_orders
FROM amazon_sales_clean
GROUP BY Payment_Method
ORDER BY total_revenue DESC;
```

---

### ⭐ KPI Metrics



```sql
SELECT
  COUNT(DISTINCT Order_ID) AS total_orders,
  ROUND(SUM(Total_Sales_INR), 2) AS total_revenue,
  ROUND(AVG(Review_Rating), 2) AS avg_rating
FROM amazon_sales_clean;
```

These SQL queries satisfy the required **minimum of two analytical queries**, with Venu having **four major analyses**.

---

# 📊 **6. Dashboard (4.6)**

Dashboard file: **Amazon Sales 2025 – INR Dashboard.lvdash.json**

Dashboard includes:

### ⭐ KPI Tiles

* Total Orders
* Total Revenue
* Average Rating

### ⭐ Visualizations

* **Bar Chart:** Revenue by Product Category
* **Bar Chart:** Revenue by State
* **Pie Chart:** Payment Method Distribution

### ⭐ Global Filters

* Product Category
* State
* Payment Method

These filters allow dynamic, user-driven analysis.

### Dashboard metadata citations

Visuals and filters extracted from the JSON export:


---

# 🏁 **7. Summary**

This project demonstrates the full Databricks lifecycle:

* ✔ Data ingestion
* ✔ Data cleaning and feature engineering
* ✔ Delta table storage
* ✔ Notebook analysis
* ✔ SQL analysis
* ✔ Dashboard creation


