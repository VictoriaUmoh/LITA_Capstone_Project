# LITA_Capstone_Project_1
This project reflects the knowledge I gained studying Data Analysis with the IncubatorHub- LITA on the tools we were taught, including Excel, SQL and Power BI. This is Project1
---
## Sales Analysis Report
### Contents
[Methodology](#methodology)

[Project Overview](#project-overview)

[Key Findings](#key-findings)

[Conclusion](#conclusion)

[SQL Queries](#sql-queries)

### Project Overview
This analysis report summarizes the findings from a sales dataset sourced from Kaggle (sent by the LITA- The IncubatorHub resource instructor). The objective was to derive key insights from the data using Excel pivot tables, SQL and Power BI specifically focusing on total sales, average sales per product, and revenue across different regions and months.

### Methodology
Pivot tables in Excel were utilized to aggregate and organize the data by:
-	Product: Summing total sales and calculating the average sales per product to understand performance.
-	Region: Summing total sales by each region to identify regional trends.
-	Month: Breaking down sales by month to observe seasonal or monthly patterns in sales.
The above indicators were considered in order to write queries for the database and to create dashboard report with Power BI
---
#### Key Findings:
1.	Total Sales by Product:
- Each product's total sales were summarized, revealing which products performed best. Products with consistently high sales suggest strong demand and popularity.
2.	Average Sales Per Product:
- By calculating the average sales for each product, we identified the products with high sales potential on a per-transaction basis. This metric helps pinpoint high-value products.
3.	Revenue by Region:
-	Sales were grouped by region to uncover which areas generated the most revenue. This information can guide regional marketing and distribution strategies to optimize sales in high-performing regions.
4.	Monthly Sales Trends:
-	Sales data was summarized by month, allowing for the identification of seasonal trends or peak sales periods. This insight can aid in inventory planning and promotional scheduling.
---
### Conclusion
This analysis highlights crucial sales insights that can drive strategic decision-making for product offerings, regional focus, and marketing timing. The use of Excel pivot tables provided a streamlined approach for data summarization, enabling a clear view of trends and performance metrics.

### SQL Queries
```sql
SELECT * FROM project1;
```

```sql
---Retrieve the total sales for each product category---
SELECT Product, SUM(Quantity) AS TotalSales
FROM project1
GROUP BY Product
ORDER BY TotalSales DESC;
```

```sql
---Find the number of sales transactions in each region---
SELECT Region, COUNT(OrderID) AS TransactionCount
FROM project1
GROUP BY Region
ORDER BY TransactionCount DESC;
```

```sql
---Find the highest-selling product by total sales value---
SELECT TOP 1 Product, SUM(Quantity * UnitPrice) AS TotalSalesValue
FROM project1
GROUP BY Product
ORDER BY TotalSalesValue DESC;
```

```sql
---Calculate total revenue per product---
SELECT Product, SUM(Revenue) AS TotalRevenue
FROM project1
GROUP BY Product
ORDER BY TotalRevenue DESC;
```

```sql
---Calculate monthly sales totals for the current year---
SELECT 
    MONTH(OrderDate) AS Month,
    SUM(Quantity) AS MonthlySales
FROM project1
WHERE YEAR(OrderDate) = YEAR(2024)
GROUP BY Month
ORDER BY Month;
```

```sql
---Find the top 5 customers by total purchase amount---
SELECT TOP 5 Customer_Id, SUM(Revenue) AS TotalPurchaseAmount
FROM project1
GROUP BY Customer_Id
ORDER BY TotalPurchaseAmount DESC;
```

```sql
---Calculate the percentage of total sales contributed by each region---
SELECT 
    Region, 
    SUM(Revenue) AS RegionSales,
    (SUM(Revenue) / (SELECT SUM(Revenue) FROM project1) * 100) AS SalesPercentage
FROM project1
GROUP BY Region
ORDER BY SalesPercentage DESC;
```
---
### Charts Representation
#### Sales Dashboard [View Here](https://ibb.co/s90PKQN)

#### Pivot Sales Analysis [View Here](https://ibb.co/B6NPT1t)

#### Sales Chart [View Here](https://ibb.co/9VZ3Prx)



---
# LITA_Capstone_Project_2: Customer Data Analysis Report
This project focuses on custome Data
### Contents:
[Project Overview](#project-overview)

[Tools Used](#tools-used)

[Data Overview](#data-overview)

[Analysis Breakdown](#analysis-breakdown)

[Visualizations in Power BI](#visualizations-in-power-bi)

[Conclusion](#conclusion)

[Visualization Overview](#visualization-overview)

### Project Overview
---
This project analyzes a customer dataset sourced from Kaggle (given by The IncubatorHub Instructor) , focusing on insights around subscription types, customer demographics, and revenue. Using pivot tables in Excel, SQL queries, and Power BI, the analysis dives into various metrics such as customer distribution by region, subscription patterns, and revenue performance. This report details the methodology, tools, and findings from each stage of the analysis.

### Tools Used
1.	SQL: For data extraction and complex queries.
2.	Excel Pivot Tables: To quickly summarize data and identify trends.
3.	Power BI: For data visualization and creating an interactive dashboard.
---
### Data Overview
The dataset includes information about customers, their subscription types, start and end dates, revenue, and regional distribution. Key columns in the dataset are:
-	CustomerID: Unique identifier for each customer.
-	CustomerName: Name of the customer.
-	Region: Geographic region of the customer.
-	SubscriptionType: Type of subscription purchased.
-	SubscriptionStart and SubscriptionEnd: Subscription period.
-	Canceled: Whether the subscription was canceled (1 for canceled, 0 for active).
-	Revenue: Total revenue generated from each customer.
---

### Analysis Breakdown
1. Total Customers by Region
Using a pivot table, I summarized the total number of customers in each region to understand where our customer base is concentrated. SQL was also used to retrieve this information:

```sql
SELECT Region, COUNT(CustomerID) AS TotalCustomers
FROM customer_data
GROUP BY Region
ORDER BY TotalCustomers DESC;
```
#### Key Insight:
Regions with the highest customer counts provide opportunities for targeted marketing and retention strategies.

### Visualizations in Power BI
In Power BI, I created several visualizations to bring the analysis to life:
-	Regional Distribution of Customers: A map visualization showing customer density across regions.
-	Subscription Cancellations: A bar chart comparing cancellations by region.
-	Revenue by Subscription Type: A pie chart breaking down revenue contribution by subscription type.
---
These visualizations provide an interactive and visual overview, enabling stakeholders to easily interpret and explore the data.
### Dashboard Analysis [View Here](https://ibb.co/Wc0mPjP)

### Conclusion
The analysis offers actionable insights into customer demographics, subscription preferences, and revenue trends. By using a combination of SQL, pivot tables, and Power BI, I was able to generate a comprehensive view of the customer data, highlighting opportunities to increase revenue and improve retention.

### Visualization Overview:

```sql
---Query: Retrieve the total number of customers from each region---
SELECT Region, COUNT(CustomerID) AS TotalCustomers
FROM customer_data
GROUP BY Region
ORDER BY TotalCustomers DESC;
```

```sql
---Query: Find the most popular subscription type by the number of customers---
SELECT TOP 1 SubscriptionType, COUNT(CustomerID) AS CustomerCount
FROM customer_data
GROUP BY SubscriptionType
ORDER BY CustomerCount DESC;
```

```sql
 ---Query: Calculate total revenue by subscription type---
 SELECT subscriptionType, SUM(Revenue) As TotalRevenue
 FROM customer_data
 GROUP BY SubscriptionType
 ORDER BY TotalRevenue DESC;
```

```sql
---Query: Find the top 3 regions by subscription cancellations---
SELECT TOP 3 Region, COUNT(CustomerID) AS Cancellations
FROM customer_data
WHERE Canceled = 1
GROUP BY Region
ORDER BY Cancellations DESC;
```

```sql
---Query: Find the total number of active and canceled subscriptions---
SELECT 
    SUM(CASE WHEN Canceled = 0 THEN 1 ELSE 0 END) AS ActiveSubscriptions,
    SUM(CASE WHEN Canceled = 1 THEN 1 ELSE 0 END) AS CanceledSubscriptions
FROM customer_data;
```

### Pivot Table Analysis [View Here](https://ibb.co/PrDvRYr)

### Power BI Dashboard [View Here](https://ibb.co/Wc0mPjP)

