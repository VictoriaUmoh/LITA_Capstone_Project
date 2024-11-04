# LITA_Capstone_Project_1
This project reflects the knowledge I gained studying Data Analysis with the IncubatorHub- LITA on the tools we were taught, including Excel, SQL and Power BI. This is Project1

## Sales Analysis Report

### Overview
This analysis report summarizes the findings from a sales dataset sourced from Kaggle (sent by the LITA- The IncubatorHub resource instructor). The objective was to derive key insights from the data using Excel pivot tables, SQL and Power BI specifically focusing on total sales, average sales per product, and revenue across different regions and months.

### Methodology
Pivot tables in Excel were utilized to aggregate and organize the data by:
-	Product: Summing total sales and calculating the average sales per product to understand performance.
-	Region: Summing total sales by each region to identify regional trends.
-	Month: Breaking down sales by month to observe seasonal or monthly patterns in sales.
The above indicators were considered in order to write queries for the database and to create dashboard report with Power BI
#### Key Findings:
1.	Total Sales by Product:
- Each product's total sales were summarized, revealing which products performed best. Products with consistently high sales suggest strong demand and popularity.
2.	Average Sales Per Product:
- By calculating the average sales for each product, we identified the products with high sales potential on a per-transaction basis. This metric helps pinpoint high-value products.
3.	Revenue by Region:
-	Sales were grouped by region to uncover which areas generated the most revenue. This information can guide regional marketing and distribution strategies to optimize sales in high-performing regions.
4.	Monthly Sales Trends:
-	Sales data was summarized by month, allowing for the identification of seasonal trends or peak sales periods. This insight can aid in inventory planning and promotional scheduling.

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

### Charts Representation
![Sales Chart](https://github.com/VictoriaUmoh/LITA_Capstone_Project/blob/main/sales%20chart.png)   

![project 1 dashboard](https://github.com/user-attachments/assets/a0fbdb93-7d75-46c7-839a-d24cb83b74ec)

![sales report2](https://github.com/user-attachments/assets/eaff0169-aea3-4469-a520-8642fc90bdeb)

![sales_chart3](https://github.com/user-attachments/assets/af9e92f3-7c4c-4a88-bd22-eb6b33cc7816)


![project 1 dashboard](https://github.com/user-attachments/assets/9cf610ae-9a10-4a17-8601-32b852f17a8c)


