# Retail Sales Analysis SQL Project  
**Project Title:** Retail Sales Analysis  
**Database:** sql_project  
This project involves setting up a retail sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries. 
# Objectives
1.	**Set up a retail sales database:** Create and populate a retail sales database with the provided sales data.  
2.	**Data Cleaning:** Identify and remove any records with missing or null values.  
3.	**Exploratory Data Analysis (EDA):** Perform basic exploratory data analysis to understand the dataset.  
4.	**Business Analysis:** Use SQL to answer specific business questions and derive insights from the sales data.
**Project Structure**  
1. **Database Setup**  
•	**Database Creation:** The project starts by creating a database named sql_project.  
•	**Table Creation:** A table named retail_sales_analysis is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.  
```sql
CREATE DATABASE sql_project;

CREATE TABLE retail_sales_analysis
(
    transactions_id INT PRIMARY KEY,
    sale_date DATE,	
    sale_time TIME,
    customer_id INT,	
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,	
    cogs FLOAT,
    total_sale FLOAT
); 
```
2. **Data Exploration & Cleaning**  
•	**Record Count:** Determine the total number of records in the dataset.  
•	**Customer Count:** Find out how many unique customers are in the dataset.  
•	**Category Count:** Identify all unique product categories in the dataset.  
•	**Null Value Check:** Check for any null values in the dataset and delete records with missing data.  
```sql
SELECT * FROM retail_sales_analysis;
SELECT COUNT (DISTINCT customer_id) FROM retail_sales_analysis;
SELECT DISTINCT category FROM retail_sales_analysis;

SELECT * FROM retail_sales_analysiss;
WHERE
    transactions_id IS null or sale_date IS null or
    sale_time IS null or customer_id IS null or
    gender IS null or age IS null or category IS null or
    quantity IS null or price_per_unit IS null or
    cogs IS null or total_sale;
DELETE FROM retail_sales_analysis
WHERE
    transactions_id IS null or sale_date IS null or
    sale_time IS null or customer_id IS null or
    gender IS null or age IS null or category IS null or
    quantity IS null or price_per_unit IS null or
    cogs IS null or total_sale;
```
3. # Data Analysis & Findings
1.	**Write a SQL query to retrieve all columns for sales made on '2022-11-05:**  
```sql
SELECT * FROM retail_sales_analysis
WHERE sale_date = '2022-11-05';
```
2.	**Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than or equal to 4 in the month of Nov-2022:**  
```sql
SELECT * FROM retail_sales_analysis
WHERE
    sale_date like '2022-11%' and
    category = 'Clothing'and
    quantity >= 4;
```
3.	**Write a SQL query to calculate the total sales (total_sale) for each category.:**  
```sql
SELECT
category,
sum(total_sale) as net_sale,
count(*) as total_orders
from retail_sales_analysis
group by 1 
```
4.	**Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.:**  
```sql
SELECT category,
    ROUND(AVG(age),0)
    from  retail_sales_analysis
    WHERE category = 'Beauty';
```
5.	**Write a SQL query to find all transactions where the total_sale is greater than 1000.:**  
```sql
SELECT * FROM retail_sales_analysis
WHERE total_sale >1000;
```
6.	**Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.:**  
```sql
SELECT category,
gender,
count(transaction_id) as total_transactions
FROM retail_sales_analysis
group by 1,2;
```
7.	**Write a SQL query to calculate the average sale for each month. Find out best selling month in each year:**  
```sql
SELECT  year_, Month_,Avg_sales
    FROM (
        SELECT
            year_,
            Month_,
            Avg_sales,
            RANK() OVER(PARTITION BY year_ ORDER BY Avg_sales DESC) AS rank_
    FROM (
	    SELECT
            Year(sale_date) AS year_,
            Month(sale_date) AS Month_,
            AVG(total_sale) AS Avg_sales
    FROM retail_sales_analysis
        GROUP BY 1,2
    ) AS monthly_sales
    ) AS ranked_sales 
    WHERE rank_ =1;
```
8.	**Write a SQL query to find the top 5 customers based on the highest total sales:**
```sql
SELECT 
	customer_id,
	SUM(total_sale)
FROM retail_sales_analysis
GROUP BY customer_id
LIMIT 5;
```
9.	**Write a SQL query to find the number of unique customers who purchased items from each category.:**   
```sql
SELECT category,
       count(DISTINCT customer_id) AS UNIQUE_customers
From retail_sales_analysis
GROUP BY 1;
```
10.	**Write a SQL query to create each shift and number of orders (Example Morning <12, Afternoon Between 12 & 17, Evening >17):**  
```sql
with hourly_table as 
(
SELECT *,
CASE 
	WHEN HOUR(sale_time) < 12 THEN 'Morning'
    WHEN HOUR(sale_time) BETWEEN 12 AND 17 THEN 'AFTERNOON'
    ELSE 'EVENING'
    END AS shift
    FROM retail_sales_analysis
)
select  shift,
		count(*) as sales
	    From hourly_table
        GROUP BY shift
        order by sales desc
```
# Findings
•	**Customer Demographics:** The dataset includes customers from various age groups, with sales distributed across different categories such as Clothing and Beauty.      
•	**High-Value Transactions:** Several transactions had a total sale amount greater than 1000, indicating premium purchases.  
•	**Sales Trends:** Monthly analysis shows variations in sales, helping identify peak seasons.    
•	**Customer Insights:** The analysis identifies the top-spending customers and the most popular product categories.    
# Reports
•	**Sales Summary:** A detailed report summarizing total sales, customer demographics, and category performance.    
•	**Trend Analysis:** Insights into sales trends across different months and shifts.    
•	**Customer Insights:** Reports on top customers and unique customer counts per category.    
# Conclusion
This project serves as a comprehensive introduction to SQL for data analysts, covering database setup, data cleaning, exploratory data analysis, and business-driven SQL queries. The findings from this project can help drive business decisions by understanding sales patterns, customer behavior, and product performance.  

**Author** - Krishna Mohan  
This project is part of my portfolio, showcasing the SQL skills essential for data analyst roles. If you have any questions, feedback, or would like to collaborate, feel free to get in touch!  


