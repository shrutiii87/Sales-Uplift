-- 1. QUESTION
CREATE TABLE region_sales_last_quarter AS
SELECT 
    Region,
    SUM(TotalAmount) AS TotalSales
FROM retailtransactions
WHERE Date >= DATE_SUB(CURDATE(), INTERVAL 3 MONTH)
GROUP BY Region;


-- 2. QUESTION
CREATE TABLE top5_products AS
SELECT 
    ProductName,
    SUM(TotalAmount) AS Revenue
FROM retailtransactions
GROUP BY ProductName
ORDER BY Revenue DESC
LIMIT 5;


-- 3. QUESTION
CREATE TABLE monthly_sales_trend AS
SELECT 
    DATE_FORMAT(Date, '%Y-%m') AS Month,
    Region,
    SUM(TotalAmount) AS TotalSales
FROM retailtransactions
GROUP BY Month, Region
ORDER BY Month, Region;

-- 4. QUESTION
CREATE TABLE region_contribution AS
SELECT 
    Region,
    ROUND(
        (SUM(TotalAmount) * 100.0) / 
        (SELECT SUM(TotalAmount) FROM retailtransactions),
        2
    ) AS ContributionPercent
FROM retailtransactions
GROUP BY Region;


-- 5. QUESTION
CREATE TABLE online_offline_sales AS
SELECT 
    DATE_FORMAT(Date, '%Y-%m') AS Month,
    SalesChannel,
    SUM(TotalAmount) AS TotalSales
FROM retailtransactions
GROUP BY Month, SalesChannel
ORDER BY Month;


-- 6. QUESTION
CREATE TABLE category_sales_trend AS
SELECT 
    DATE_FORMAT(Date, '%Y-%m') AS Month,
    Category,
    SUM(TotalAmount) AS TotalSales
FROM retailtransactions
GROUP BY Month, Category
ORDER BY Month, TotalSales DESC;


-- 7. QUESTION
CREATE TABLE frequent_customers AS
SELECT 
    CustomerID,
    COUNT(*) AS PurchaseCount
FROM retailtransactions
GROUP BY CustomerID
HAVING COUNT(*) > 10
ORDER BY PurchaseCount DESC;