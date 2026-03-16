# 🛒 **Retail Sales Analysis (SQL Project)**

## 📊 **Overview**
This project focuses on analyzing retail sales data using SQL to uncover insights into customer behavior, product performance, and sales patterns. It demonstrates how structured queries can be used for data cleaning, validation, and exploratory analysis within a relational database.

**Objectives**
- ✅ Create and manage a retail sales database.
- ✅ Load and validate transactional data.
- ✅ Identify null or missing values.
- ✅ Explore customer demographics and purchasing trends.
- ✅ Build a foundation for further business analysis (e.g., revenue forecasting, product performance).

## 🗄️ **Database Schema**

| **Database:** `sql_p1` | **Table:** `retail_sales` |
|------------------------|---------------------------|

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| `transactions_id` | `INT` | Unique transaction identifier |
| `sale_date` | `DATE` | Date of the sale |
| `sale_time` | `TIME` | Time of the sale |
| `customer_id` | `INT` | Unique customer identifier |
| `gender` | `VARCHAR(10)` | Gender of the customer |
| `age` | `INT` | Customer's age |
| `category` | `VARCHAR(15)` | Product category |
| `quantity` | `INT` | Quantity of items sold |
| `price_per_unit` | `FLOAT` | Price per item |
| `cogs` | `FLOAT` | Cost of goods sold |
| `total_sale` | `FLOAT` | Total sale amount |

## 🚀 **Steps Performed**
1. Created a new database `sql_p1`.
2. Created table `retail_sales` with transactional data columns.
3. Validated data integrity and null values.
4. Explored customer and category diversity.
5. Analyzed sales performance and trends using **10 analytical SQL queries**.

## 🔍 **Detailed Analysis Queries**

### **Q.1** Sales on '2022-11-05'
```sql
SELECT * FROM retail_sales WHERE sale_date = '2022-11-05';
```

### **Q.2** Clothing >4 quantity in Nov-2022
```sql
SELECT * FROM retail_sales WHERE category = 'Clothing' AND date_format(sale_date, '%Y-%m') = '2022-11' AND quantity >= 4;
```

### **Q.3** Total sales by category
```sql
SELECT category, SUM(total_sale) as net_sale, COUNT(*) as total_orders FROM retail_sales GROUP BY 1;
```

### **Q.4** Average age by category
```sql
SELECT category, ROUND(AVG(age), 2) as avg_age FROM retail_sales group by category;
```

### **Q.5** High-value transactions (>1000)
```sql
select category,quantity,total_sale from retail_sales where total_sale > 1000;
```

### **Q.6** Transactions by gender & category
```sql
SELECT category, gender, COUNT(*) as total_trans FROM retail_sales GROUP BY category, gender ORDER BY 1;
```

### **Q.7** Best selling month per year
```sql
SELECT year, month, avg_sale FROM (
    SELECT EXTRACT(YEAR FROM sale_date) AS year, 
           EXTRACT(MONTH FROM sale_date) AS month, 
           AVG(total_sale) AS avg_sale,
           RANK() OVER (PARTITION BY EXTRACT(YEAR FROM sale_date) ORDER BY AVG(total_sale) DESC) AS rnk
    FROM retail_sales GROUP BY 1, 2
) AS t WHERE rnk = 1 ORDER BY year, avg_sale DESC;
```

### **Q.8** Top 5 customers by sales
```sql
SELECT customer_id, SUM(total_sale) as total_sales FROM retail_sales GROUP BY 1 ORDER BY 2 DESC LIMIT 5;
```

### **Q.9** Unique customers per category
```sql
SELECT category, COUNT(DISTINCT customer_id) as cnt_unique_cs FROM retail_sales GROUP BY category;
```

### **Q.10** Sales by time shift
```sql
WITH hourly_sale AS (
    SELECT *, 
    CASE 
        WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
        WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening'
    END as shift 
    FROM retail_sales
)
SELECT shift, COUNT(*) as total_orders FROM hourly_sale GROUP BY shift;
```

## 🛠️ **Technologies Used**
<div align="center">





</div>

## 💡 **Key Insights**
- 🔥 **Top-selling categories** and **high-performing months** identified
- 👥 **Customer demographics** correlated with purchase preferences
- ⏰ **Category-wise** and **time-shift-based** demand distribution revealed
- 🏆 **Top customers** identified for loyalty programs

## 🏃‍♂️ **How to Run the Project**

```bash
git clone https://github.com/[username]/retail-sales-analysis.git
cd retail-sales-analysis
```

**Execute SQL:**
```sql
SOURCE retail_sales_analysis.sql;
```

Run each query sequentially to reproduce analysis results! 🚀

## 🚀 **Future Enhancements**
- 📈 Integrate **Python** (Matplotlib/Seaborn) for visualization
- 🔄 **ETL pipelines** for automated reporting
- 📊 **Power BI dashboard** for interactive analytics
- 📊 Additional KPIs: purchase frequency, customer lifetime value

***

<div align="center">
    
**👨‍💻 Author:** *Venkata Varma Vatsavayi*  
**🎯 Passionate about Data Analytics and SQL-based Insights**

[
[

</div>

