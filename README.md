# 🍽️ Restaurant Order Analysis – The World Cafe

![Restaurant Banner](images/banner.png)  
*Visualize customer orders, menu popularity, and revenue trends.*

---

# 📌 Project Overview
This project analyzes **order and menu data from The World Cafe** using **MySQL** to provide actionable insights for restaurant management.  

The analysis helps answer key business questions:

- Which menu items are the most and least popular?  
- Which types of cuisine generate the most revenue?  
- How do order volumes vary by time and category?  

**Outcome:** Recommendations to optimize menu offerings, boost revenue, and enhance customer satisfaction.

---

# 🖼️ Highlights / Key Insights

| Insight | Description |
|---------|-------------|
| **Most expensive item** | Shrimp Scampi (Italian) |
| **Least expensive item** | Edamame (Asian) |
| **Most ordered item** | American Hamburger |
| **Least ordered item** | Mexican Chicken Tacos |
| **Top orders by revenue** | Premium dishes from multiple categories |
| **Popular cuisine** | Italian dishes dominate menu orders |

![Top 5 Orders Chart](images/top_orders.png)  
*Example visualization of top 5 highest spending orders.*

---

# 📂 Table of Contents

- [Project Overview](#project-overview)  
- [Data Sources](#data-sources)  
- [Tools Used](#tools-used)  
- [Data Cleaning / Preparation](#data-cleaning--preparation)  
- [Exploratory Data Analysis](#exploratory-data-analysis)  
- [SQL Queries](#sql-queries)  
- [Results / Findings](#results--findings)  
- [Future Improvements](#future-improvements)  
- [References](#references)  

---
# 🗄️ Data Sources

1. **Menu Items Data** – `menu_items` file: Details about each menu item, including price, category, and cuisine type.  
2. **Order Details Data** – `order_details` file: Details of each order placed, including item IDs, order ID, and order date.

---

# 🛠️ Tools Used

- **MySQL** – ETL, data cleaning, and exploratory data analysis  
- **GitHub** – Version control and project hosting  

---

# 🧹 Data Cleaning / Preparation

1. Loaded the datasets into MySQL.  
2. Checked for missing values and duplicates.  
3. Standardized column types and formats.  
4. Prepared combined table for detailed analysis (`order_details` + `menu_items`).  

---

# 🔍 Exploratory Data Analysis (EDA)

EDA answered business-critical questions:

- How many items are on the menu?  
- Least and most expensive items (overall and by cuisine)  
- Number of dishes per category and average price  
- Total orders and total items ordered  
- Orders with the most items (e.g., >12 items)  
- Most and least ordered items  
- Top 5 orders by revenue and their item/category breakdown  

![Menu Analysis Chart](images/menu_analysis.png)  
*Example: Distribution of dishes per category.*

---

# 💻 SQL Queries (Examples)

# Menu Analysis
```sql
-- Count items on the menu
SELECT COUNT(*) FROM menu_items;

-- Least and most expensive items
SELECT * FROM menu_items ORDER BY price;
SELECT * FROM menu_items ORDER BY price DESC;


# Orders Analysis

-- Total orders and items
SELECT COUNT(DISTINCT order_id) FROM order_details;
SELECT COUNT(*) FROM order_details;

-- Orders with most items
SELECT order_id, COUNT(item_id) AS num_items
FROM order_details
GROUP BY order_id
ORDER BY num_items DESC;

-- Orders with more than 12 items
SELECT COUNT(*) FROM (
    SELECT order_id, COUNT(item_id) AS num_items
    FROM order_details
    GROUP BY order_id
    HAVING num_items > 12
) AS large_orders;
-- Italian dishes count
SELECT COUNT(*) FROM menu_items WHERE category='italian';
