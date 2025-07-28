
#  Blinkit Sales & Customer Analytics Using SQL

##  Overview

This project provides a comprehensive analysis of **Blinkit’s retail sales data** using SQL for data cleaning, querying, and KPI extraction. The goal is to uncover business insights on customer satisfaction, product performance, and outlet efficiency. Visualizations (in Power BI) support data-driven decisions for product optimization and strategy alignment.

---

##  Project Objectives

- Clean and standardize inconsistent data for accurate analytics.
- Analyze sales, ratings, and item behavior by multiple dimensions (fat content, item type, outlet).
- Use SQL and Power BI for KPI extraction, pivot analysis, and dashboarding.
- Provide recommendations based on item, outlet, and location-level insights.

---

##  Dataset Details

- **Source**: `blinkit_data` (SQL table)
- **Fields**:  
  `Item_Fat_Content`, `Item_Type`, `Total_Sales`, `Rating`,  
  `Outlet_Size`, `Outlet_Type`, `Outlet_Establishment_Year`,  
  `Outlet_Location_Type`, `Item_Visibility`

---

##  Data Cleaning

Standardized `Item_Fat_Content` values:
```sql
UPDATE blinkit_data
SET Item_Fat_Content = CASE 
    WHEN Item_Fat_Content IN ('LF', 'low fat') THEN 'Low Fat'
    WHEN Item_Fat_Content = 'reg' THEN 'Regular'
    ELSE Item_Fat_Content
END;
```

---

##  KPIs Extracted

| KPI                 | Description                         |
|---------------------|-------------------------------------|
| **Total Sales**     | `SUM(Total_Sales)`                  |
| **Average Sales**   | `AVG(Total_Sales)`                  |
| **Number of Orders**| `COUNT(*)`                          |
| **Average Rating**  | `AVG(Rating)`                       |

---

##  Key Analyses & SQL Queries

### 1. Sales by Fat Content
```sql
SELECT Item_Fat_Content, SUM(Total_Sales) 
FROM blinkit_data 
GROUP BY Item_Fat_Content;
```

### 2. Sales by Item Type
```sql
SELECT Item_Type, SUM(Total_Sales) 
FROM blinkit_data 
GROUP BY Item_Type 
ORDER BY Total_Sales DESC;
```

### 3. Fat Content by Outlet (Pivot Table)
Transposed `Item_Fat_Content` to columns with sales values, segmented by `Outlet_Location_Type`.

### 4. Sales by Establishment Year
```sql
SELECT Outlet_Establishment_Year, SUM(Total_Sales) 
FROM blinkit_data 
GROUP BY Outlet_Establishment_Year;
```

### 5. Percentage of Sales by Outlet Size
```sql
SELECT Outlet_Size, 
       SUM(Total_Sales) AS Sales, 
       SUM(Total_Sales) * 100.0 / SUM(SUM(Total_Sales)) OVER() AS Sales_Percentage
FROM blinkit_data
GROUP BY Outlet_Size;
```

### 6. Sales by Location & Outlet Type
Mapped geographic and operational insights using location-wise and type-wise grouping.

---

##  Dashboard (Power BI)

-  **Bar Chart**: Total Sales by Item Type  
-  **Pie Chart**: Fat Content contribution  
-  **Line Chart**: Sales by Establishment Year  
-  **Map**: Sales by Location  
-  **Pivot Table**: Metrics by Outlet Type  
-  **KPI Cards**: Total Sales, Avg. Rating, etc.

---

##  Conclusion

- **Fat content** significantly affects user ratings and revenue.
- **Snacks and Dairy** top the sales chart among item types.
- **Outlet location** and **establishment year** influence performance.
- **Medium-sized outlets** dominate revenue contribution.

---

##  Tools Used

- **SQL (MSSQL / MySQL)** – for data cleaning & aggregation  
- **Power BI** – for dashboard and visual analysis  
- **Microsoft Excel** – (optional) intermediate review

---

##  Author

**Vinod Kumar**  
 [imvinodkumar29@gmail.com](mailto:imvinodkumar29@gmail.com)  
 [LinkedIn](https://www.linkedin.com/in/vinod-kumar-0411a7250/) | [GitHub](https://github.com/vinodkumartz)

---

##  Contributions and Suggestions Welcome!
