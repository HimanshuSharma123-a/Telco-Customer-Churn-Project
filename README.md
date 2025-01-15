
[**Download Dataset**](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
# Telco Customer Churn Analysis
SQL PROJECT
This project aims to analyze and predict customer churn for a telecom company using a dataset from Kaggle. The analysis is performed using SQL queries, exploring various aspects of customer behavior and identifying patterns that may lead to churn. The goal is to uncover insights that can help reduce churn and improve customer retention.

## Project Overview

The dataset contains information about customers, including demographic data, account information, services used, and customer status. By analyzing this data, we can understand the factors contributing to customer churn and suggest improvements based on the findings.

### Key Objectives:
- Identify patterns in customer behavior related to churn.
- Provide insights into potential improvements for reducing churn.
- Solve SQL-based problems to analyze and manipulate data effectively.
  
## Technologies Used
- **SQL**: For querying and analyzing data.
- **Kaggle**: Dataset source.
- **GitHub**: For version control and project sharing.

## Problem Statements & Insights
- Solved 10-15 SQL queries related to customer demographics, account information, service usage, and churn.
- Provided percentage-based insights on improvements, such as how different factors (e.g., customer tenure, service usage) impact the likelihood of churn.

## Results
The analysis provided actionable insights into improving customer retention, including:
- Key demographic features contributing to churn.
- Insights into service usage patterns and their effect on customer loyalty.
- Recommendations for retention strategies based on the analysis.

## Future Improvements
- Implement machine learning models to predict churn more accurately.
- Explore more advanced SQL queries for deeper insights.
- Build a dashboard to visualize churn trends and factors.

## SQL Queries

```sql
create database Telco_Customer_Churn;

-- 1. Count of Total coloumn:

SELECT COUNT(*) AS column_count  
WHERE TABLE_NAME = 'telco-customer-churn';

-- 2. Count of Total Rows :

SELECT COUNT(*) AS TotalRows
FROM `telco-customer-churn`;

-- ------------------- Problem Statements --------------------- 

-- 1. Calculate the total number of customers and their average monthly charges.

SELECT COUNT(*) AS Total_Customers, AVG(MonthlyCharges) AS Average_Monthly_Charges 
FROM `telco-customer-churn`;

-- 2. Find the distribution of customers based on contract types (Month-to-Month, One-Year, Two-Year).

SELECT Contract, COUNT(*) AS Total_Customers
FROM `telco-customer-churn`
GROUP BY Contract;

-- 3. Determine churn rates for each type of contract.

SELECT Contract, 
       COUNT(*) AS Total_Customers, 
       SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS Churn_Customers,
       (SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*)) AS Churn_Rate
FROM `telco-customer-churn`
GROUP BY Contract;
 
-- 4. Calculate the average tenure of customers.

SELECT AVG(tenure) AS Average_Tenure
FROM `telco-customer-churn`;

-- 5. Analyze churn rates for customers with short (<12 months), medium (12–24 months), and long (>24 months) tenure.

SELECT CASE 
           WHEN tenure < 12 THEN 'Short-Term'
           WHEN tenure BETWEEN 12 AND 24 THEN 'Medium-Term'
           ELSE 'Long-Term'
       END AS Tenure_Category,
       COUNT(*) AS Total_Customers,
       SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS Churn_Customers,
       (SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*)) AS Churn_Rate
FROM `telco-customer-churn`
GROUP BY Tenure_Category;

-- 6. Check the effect of online security services on churn rates.

SELECT OnlineSecurity, 
       COUNT(*) AS Total_Customers, 
       SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS Churn_Customers,
       (SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*)) AS Churn_Rate
FROM `telco-customer-churn`
GROUP BY OnlineSecurity;


-- 7. Analyze churn rates based on payment methods.

SELECT PaymentMethod, 
       COUNT(*) AS Total_Customers, 
       SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS Churn_Customers,
       (SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*)) AS Churn_Rate
FROM `telco-customer-churn`
GROUP BY PaymentMethod;

-- 8. Analyze churn among senior citizens compared to non-senior citizens.

SELECT SeniorCitizen, 
       COUNT(*) AS Total_Customers, 
       SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS Churn_Customers,
       (SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*)) AS Churn_Rate
FROM `telco-customer-churn`
GROUP BY SeniorCitizen;
 
 -- 9. Calculate the total revenue generated for each contract type.
 
 SELECT Contract, 
       SUM(MonthlyCharges) AS Total_Revenue
FROM `telco-customer-churn`
GROUP BY Contract;

-- 10. Identify how many customers opted out of internet services.

SELECT InternetService, COUNT(*) AS Total_Customers
FROM `telco-customer-churn`
WHERE InternetService = 'No';

-- 11. Compare churn rates between male and female customers.

SELECT gender, 
       COUNT(*) AS Total_Customers,
       SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS Churn_Customers,
       (SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*)) AS Churn_Rate
FROM `telco-customer-churn`
GROUP BY gender;

-- 12. Analyze the impact of having dependents on churn.

SELECT Dependents, 
       COUNT(*) AS Total_Customers, 
       SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS Churn_Customers,
       (SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*)) AS Churn_Rate
FROM `telco-customer-churn`
GROUP BY Dependents;

-- 13. Analyze churn rates for customers with and without phone service.

SELECT PhoneService, 
       COUNT(*) AS Total_Customers, 
       SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS Churn_Customers,
       (SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*)) AS Churn_Rate
FROM `telco-customer-churn`
GROUP BY PhoneService;

-- 14. Analyze how technical support impacts churn.

SELECT TechSupport, 
       COUNT(*) AS Total_Customers, 
       SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS Churn_Customers,
       (SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*)) AS Churn_Rate
FROM `telco-customer-churn`
GROUP BY TechSupport;

-- 15. Calculate the total revenue generated by each type of internet service.

SELECT InternetService, 
       SUM(MonthlyCharges) AS Total_Revenue
FROM `telco-customer-churn`
GROUP BY InternetService;

-- 16. Determine how many customers use multiple lines and their churn rates.

SELECT MultipleLines, 
       COUNT(*) AS Total_Customers, 
       SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS Churn_Customers,
       (SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*)) AS Churn_Rate
FROM `telco-customer-churn`
GROUP BY MultipleLines;

-- 17. Analyze churn rates among customers using streaming services.

SELECT StreamingTV, StreamingMovies, 
       COUNT(*) AS Total_Customers, 
       SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS Churn_Customers
FROM `telco-customer-churn`
GROUP BY StreamingTV, StreamingMovies;

-- 18. Calculate average monthly charges for senior citizens vs. non-senior citizens.

SELECT SeniorCitizen, 
       AVG(MonthlyCharges) AS Average_Revenue
FROM `telco-customer-churn`
GROUP BY SeniorCitizen;

-- 19. Investigate how paperless billing impacts churn.

SELECT PaperlessBilling, 
       COUNT(*) AS Total_Customers, 
       SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS Churn_Customers,
       (SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*)) AS Churn_Rate
FROM `telco-customer-churn`
GROUP BY PaperlessBilling;
```

 
## Insights and Recommendations
- Highlight churn trends (e.g., month-to-month contracts have a higher churn rate).
- Identify services that can reduce churn (e.g., offering discounts for annual contracts).
- Showcase SQL skills and actionable insights derived from the dataset.

 




