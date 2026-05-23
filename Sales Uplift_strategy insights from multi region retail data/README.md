# 📊 Sales Uplift: Strategy Insights from Multi-Region Retail Data

An end-to-end **Business Analytics Project** combining SQL data analysis with an interactive **Power BI Dashboard** to extract strategic insights from multi-region retail transactions. This project demonstrates real-world skills in SQL querying, data modeling, DAX measures, and Power BI dashboard design — built to support sales strategy decisions for Q3.

---

## 🚀 Project Overview

As a Business Analyst at a multi-region retail company, the goal was to analyze a large transaction dataset using SQL and Power BI. The dashboard empowers managers to explore sales trends, customer behavior, regional performance, and product strategy — all from a single interactive interface.

---

## 🧑‍🎓 Exam Details

| Field | Details |
|-------|---------|
| 📝 **Exam Title** | Sales Uplift: Strategy Insights from Multi-Region Retail Data |
| 🎓 **Exam Type** | Standalone Case-Based Practical |
| ⏳ **Duration** | 3 Hours |
| 📦 **Dataset** | `RetailTransactions.csv` (AI-generated) |
| 🔧 **Tools Used** | MySQL · Power BI Desktop |

---

## 🎬 Project Demo

[![Watch the Project Walkthrough](https://img.shields.io/badge/▶️%20Watch%20Demo-Google%20Drive-blue?style=for-the-badge&logo=google-drive)]

---

## 📁 Project Files

| File / Folder | Description |
|---------------|-------------|
| 📄 `Sale_uplift.pbix` | Main Power BI dashboard file |
| 📝 `Queries.txt` | All SQL queries used for data analysis |
| 📁 `SQL output tables/` | Exported results from each SQL query |
| 📁 `file used/` | Source CSV dataset (`RetailTransactions.csv`) |
| 📁 `Dashboard Preview/` | Screenshots of all dashboard pages |
| 📘 `README.md` | Project documentation |

---

## 📁 Dataset Structure

**File:** `RetailTransactions.csv`

| Column Name | Description |
|-------------|-------------|
| `TransactionID` | Unique ID of the transaction |
| `Date` | Date of transaction |
| `ProductName` | Name of product sold |
| `Category` | Product category |
| `Region` | Region of sale (East, West, North, South) |
| `SalesChannel` | Online / Offline |
| `Quantity` | Units sold |
| `UnitPrice` | Price per unit |
| `TotalAmount` | Total = Quantity × UnitPrice |
| `PaymentMode` | Credit Card, Cash, UPI, Net Banking |
| `CustomerID` | Unique ID of customer |

---

## 🧩 Project Tasks Breakdown

### 🔹 1️⃣ SQL Analysis (Part 1)

All queries were written and executed in **MySQL**, with output tables saved for use in Power BI.

#### ✅ Query 1 – Total Sales Per Region (Last Quarter)

```sql
CREATE TABLE region_sales_last_quarter AS
SELECT 
    Region,
    SUM(TotalAmount) AS TotalSales
FROM retailtransactions
WHERE Date >= DATE_SUB(CURDATE(), INTERVAL 3 MONTH)
GROUP BY Region;
```

#### ✅ Query 2 – Top 5 Best-Selling Products by Revenue

```sql
CREATE TABLE top5_products AS
SELECT 
    ProductName,
    SUM(TotalAmount) AS Revenue
FROM retailtransactions
GROUP BY ProductName
ORDER BY Revenue DESC
LIMIT 5;
```

#### ✅ Query 3 – Monthly Sales Trend Across All Regions

```sql
CREATE TABLE monthly_sales_trend AS
SELECT 
    DATE_FORMAT(Date, '%Y-%m') AS Month,
    Region,
    SUM(TotalAmount) AS TotalSales
FROM retailtransactions
GROUP BY Month, Region
ORDER BY Month, Region;
```

#### ✅ Query 4 – Region-wise Contribution to Total Sales (%)

```sql
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
```

#### ✅ Query 5 – Online vs Offline Sales by Month

```sql
CREATE TABLE online_offline_sales AS
SELECT 
    DATE_FORMAT(Date, '%Y-%m') AS Month,
    SalesChannel,
    SUM(TotalAmount) AS TotalSales
FROM retailtransactions
GROUP BY Month, SalesChannel
ORDER BY Month;
```

#### ✅ Query 6 – Sales Trend by Category

```sql
CREATE TABLE category_sales_trend AS
SELECT 
    DATE_FORMAT(Date, '%Y-%m') AS Month,
    Category,
    SUM(TotalAmount) AS TotalSales
FROM retailtransactions
GROUP BY Month, Category
ORDER BY Month, TotalSales DESC;
```

#### ✅ Query 7 – Frequent Customers (Purchased More Than 10 Times)

```sql
CREATE TABLE frequent_customers AS
SELECT 
    CustomerID,
    COUNT(*) AS PurchaseCount
FROM retailtransactions
GROUP BY CustomerID
HAVING COUNT(*) > 10
ORDER BY PurchaseCount DESC;
```

---

### 🔹 2️⃣ Power BI Dashboard (Part 2)

#### 📌 Home Page

The landing page presents the project title with a clean, branded layout and navigation to the main dashboard views.

![Home Page]([Dashboard%20Preview/Home_page.png](https://github.com/shrutiii87/Business-Case-Study/blob/main/Sales%20Uplift_strategy%20insights%20from%20multi%20region%20retail%20data/Dashboard%20Preview/Home%20page.png))

---

#### 📌 Main Overview Page

The primary dashboard view with KPI cards, monthly trends, regional breakdown, and sales channel distribution.

![Main Overview]([Dashboard%20Preview/Main_Overview.png](https://github.com/shrutiii87/Business-Case-Study/blob/main/Sales%20Uplift_strategy%20insights%20from%20multi%20region%20retail%20data/Dashboard%20Preview/Main%20Overview.png))

**KPI Cards:**
- **Total Sales** → `6.74M`
- **Total Transactions** → `500`
- **Unique Customers** → `487`
- **Average Order Value** → `13.49K`

**Monthly Sales Trend (Line Chart):**
- X-axis: `Year / Month`
- Y-axis: `Count of TotalSales`
- Visualizes transaction volume fluctuations across the full time range

**Region-wise Sales Breakdown (Pie Chart):**
- Each region (East, North, South, West) contributes equally at **25%** of total sales
- Highlights balanced regional distribution

**Sales Channel Distribution (Donut Chart):**
- Split between `Online` and `Offline` channels
- Useful for identifying channel-level strategy opportunities

**Slicers:**
- Month (dropdown), Region (checkboxes), SalesChannel (checkboxes)

---

#### 📌 Growth Focus Insights Page

A deep-dive page focused on customer value, product performance, and category trends.

![Growth Focus Insights]([Dashboard%20Preview/Growth_focus_insights.png](https://github.com/shrutiii87/Business-Case-Study/blob/main/Sales%20Uplift_strategy%20insights%20from%20multi%20region%20retail%20data/Dashboard%20Preview/Growth%20focus%20insights.png))

**Most Valuable Customers (Horizontal Bar Chart):**
- Y-axis: `CustomerID`
- X-axis: `Total Sales`
- Top 5: C8600, C7349, C6245, C9447, C2229

**Top 5 Products (Bar Chart):**
- Products: Smartphone, Headphones, Shoes, Sofa, Tablet
- Smartphone and Headphones lead with ~0.5M revenue each

**Category Performance Trend (Line Chart):**
- Tracks Beauty, Clothing, Electronics, Furniture, Groceries across Q1–Q4
- All categories show a notable dip in Q2/Q3 with partial recovery

**Slicers:**
- Category (dropdown), Product (dropdown)

---

#### 📌 Report Answers Page

A storytelling page that directly answers the manager's strategic questions using insight cards.

![Report Answers]([Dashboard%20Preview/Report_Page.png](https://github.com/shrutiii87/Business-Case-Study/blob/main/Sales%20Uplift_strategy%20insights%20from%20multi%20region%20retail%20data/Dashboard%20Preview/Report%20Page.png))

| Business Question | Key Insight |
|-------------------|-------------|
| 🏆 Most valuable customers? | C8600 (₹67,264), C7349 (₹49,756), C6245 (₹49,350), C9447 (₹49,321), C2229 (₹47,486) |
| 📦 Products to focus next quarter? | Smartphones, Headphones, Shoes, Perfume, Laptops — driving bulk of revenue |
| 🌐 Online vs Offline? | Online outperforms — stronger in Electronics & Beauty; Offline leads in Furniture & Groceries |
| 📍 Regions needing marketing push? | North & West need support for premium products; South & East already strong |

---

### 🔹 3️⃣ Interactivity

| Feature | Details |
|---------|---------|
| **Slicers** | Month, Region, SalesChannel — applied across pages |
| **KPI Cards** | Total Sales, Total Transactions, Unique Customers, Average Order Value |
| **Cross-filtering** | All visuals respond to slicer selections |
| **Storytelling Page** | Dedicated Report Answers page with business Q&A cards |
| **Category & Product Filters** | Dropdown slicers on Growth Focus Insights page |

---

## 📊 Dashboard Tab Structure

| Tab | Content |
|-----|---------|
| **Home** | Branded landing page with project title and navigation |
| **Main Overview** | KPIs, Monthly Trend Line, Region Pie Chart, Channel Donut, Slicers |
| **Growth Focus Insights** | Top Customers Bar, Top 5 Products Bar, Category Trend Line, Filters |
| **Report Answers** | Business Q&A cards with strategic insights |

---

## 📈 How to Use

1. Download or clone the repository
2. Open `Sale_uplift.pbix` in **Microsoft Power BI Desktop**
3. Import `RetailTransactions.csv` from the `file used/` folder if prompted to refresh data
4. Navigate tabs: **Main Overview → Growth Focus Insights → Report Answers**
5. Use **Month**, **Region**, and **SalesChannel** slicers to filter the entire dashboard
6. On the Growth Focus Insights page, use **Category** and **Product** dropdowns to drill deeper
7. Review the **Report Answers** page for ready-made strategic conclusions
8. Open **SQL output tables/** to cross-check dashboard data with raw query results

---

## 🛠️ Tools & Technologies Used

| Tool | Features Used |
|------|--------------|
| **MySQL** | SELECT, GROUP BY, HAVING, DATE_FORMAT, DATE_SUB, subqueries, CREATE TABLE AS |
| **Power BI Desktop** | Report View, Model View, Slicers, KPI Cards, Line/Pie/Bar/Donut Charts |
| **Power Query** | CSV import, data type corrections, column cleaning |
| **DAX** | Aggregation measures for KPI cards |
| **SQL Output Tables** | Pre-aggregated data reused as Power BI data sources |

---

## 💡 Key Business Insights

- 🏆 **C8600** is the single most valuable customer with **₹67,264** in total purchases
- 📱 **Smartphones & Headphones** are the top revenue-driving products — prioritize for Q3 promotions
- 🌐 **Online channel outperforms Offline** overall, especially in high-value Electronics & Beauty categories
- 🗺️ **South & East regions** are high performers; **North & West** need targeted marketing for premium products
- 📉 **All categories dip in Q2–Q3** — a seasonal pattern worth addressing with mid-year campaigns
- ⚖️ **Equal regional sales distribution (25% each)** suggests consistent reach but room to grow in underperforming categories per region

---

## 📤 Submission Contents

| File | Description |
|------|-------------|
| 📝 `Queries.txt` | SQL script with all 7 required queries |
| 📄 `Sale_uplift.pbix` | Completed Power BI dashboard |
| 📁 `SQL output tables/` | Exported CSV results from each SQL query |
| 📁 `Dashboard Preview/` | Screenshots of all dashboard pages |

---

## 👩‍💻 Shruti Bhawsar

📍 Ahmedabad

⭐ If you found this project useful — give this repository a ⭐ and feel free to fork or contribute!

🎯 Clean SQL. Sharp Visuals. Actionable Strategy.
