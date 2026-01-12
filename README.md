# ☕ Coffee Shop Sales Analysis Dashboard

A comprehensive business intelligence project analyzing coffee shop sales data across multiple locations, providing actionable insights through advanced SQL analytics and interactive Power BI visualizations.

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Data Analysis](https://img.shields.io/badge/Data%20Analysis-FF6B6B?style=for-the-badge&logo=analytics&logoColor=white)

## 📊 Project Overview

This project delivers end-to-end sales analytics for a multi-location coffee shop chain, transforming raw transactional data into strategic business insights. The solution encompasses data cleaning, advanced SQL querying, KPI development, and interactive dashboard creation.

### Key Metrics Tracked
- **Total Sales**: $99K (March 2023) with +29.8% MoM growth
- **Total Orders**: 21,229 transactions (+29.8% vs previous month)
- **Total Quantity Sold**: 30,406 units (+29.1% MoM growth)

## 🎯 Business Objectives

1. Monitor sales performance across three store locations
2. Identify peak sales hours and days for optimal staffing
3. Analyze product category performance and top-selling items
4. Track month-over-month growth trends
5. Compare weekday vs weekend sales patterns
6. Enable data-driven decision making for inventory and operations

## 🛠️ Technical Stack

### Data Processing & Analysis
- **MySQL**: Complex queries with window functions, aggregations, and date/time transformations
- **Power BI Desktop**: Interactive dashboard with drill-down capabilities
- **Data Modeling**: Optimized schema design for analytical workloads

### Key SQL Techniques Implemented
- Window Functions (LAG) for MoM calculations
- Date/Time manipulation and formatting
- Conditional aggregations (CASE statements)
- Subqueries and CTEs for complex analytics
- Performance optimization with proper indexing

## 📈 Dashboard Features

### KPI Cards with Trend Indicators
- Real-time sales, orders, and quantity metrics
- Visual MoM percentage change indicators
- Comparison against previous month performance

### Interactive Visualizations
1. **Sales Trend Analysis**: Daily sales patterns with average benchmarking
2. **Calendar Heat Map**: Daily performance visualization for quick insights
3. **Weekday/Weekend Split**: 74.23% weekday vs 25.77% weekend distribution
4. **Location Performance**: Comparative analysis across Hell's Kitchen, Lower Manhattan, and Astoria
5. **Product Analytics**: Category and item-level sales breakdown
6. **Hourly Heatmap**: Day-by-hour sales matrix for operational planning

## 📁 Project Structure

```
coffee-shop-sales-analysis/
├── data/
│   └── coffee_shop_sales.csv
├── sql/
│   ├── data_transformation.sql
│   ├── kpi_queries.sql
│   └── analysis_queries.sql
├── dashboard/
│   └── Coffee_Shop_Sales_Dashboard.pbix
├── documentation/
│   ├── SQL_Queries_Documentation.pdf
│   └── Dashboard_Screenshots.pdf
└── README.md
```

## 🔍 Key Insights Discovered

### Sales Performance
- **Peak Hours**: 8-10 AM accounts for highest transaction volume ($12K-$13K)
- **Best Performing Location**: Hell's Kitchen leads with $33.11K (+28.7% growth)
- **Top Product Category**: Coffee generates $38.30K (38.7% of total sales)

### Growth Opportunities
- Weekend sales represent only 25.77% of revenue - potential for targeted promotions
- Afternoon hours (11 AM - 5 PM) show consistent $6K revenue - opportunity for lunch menu expansion
- Branded merchandise shows highest growth rate (+45.8%) despite low volume

### Operational Insights
- Consistent performance across all three locations (±$100 variance)
- Strong correlation between weekday patterns and commuter behavior
- Hot Chocolate and Barista Espresso emerge as top individual products

## 💡 SQL Highlights

### Month-over-Month Growth Calculation
```sql
SELECT 
    MONTH(transaction_date) AS month,
    ROUND(SUM(unit_price * transaction_qty)) AS total_sales,
    (SUM(unit_price * transaction_qty) - LAG(SUM(unit_price * transaction_qty), 1)
    OVER (ORDER BY MONTH(transaction_date))) / LAG(SUM(unit_price * transaction_qty), 1) 
    OVER (ORDER BY MONTH(transaction_date)) * 100 AS mom_increase_percentage
FROM coffee_shop_sales
WHERE MONTH(transaction_date) IN (4, 5)
GROUP BY MONTH(transaction_date);
```

### Sales Status vs Average
```sql
SELECT 
    day_of_month,
    CASE 
        WHEN total_sales > avg_sales THEN 'Above Average'
        WHEN total_sales < avg_sales THEN 'Below Average'
        ELSE 'Average'
    END AS sales_status,
    total_sales
FROM (
    SELECT 
        DAY(transaction_date) AS day_of_month,
        SUM(unit_price * transaction_qty) AS total_sales,
        AVG(SUM(unit_price * transaction_qty)) OVER () AS avg_sales
    FROM coffee_shop_sales
    WHERE MONTH(transaction_date) = 5
    GROUP BY DAY(transaction_date)
) AS sales_data;
```

## 📊 Dashboard Preview

The Power BI dashboard provides:
- Dynamic month/year filtering
- Interactive calendar view with tooltips
- Drill-through capabilities for detailed analysis
- Color-coded performance indicators
- Mobile-responsive design

## 🚀 How to Use

1. **Database Setup**
   ```sql
   -- Import the coffee_shop_sales.csv
   -- Run data_transformation.sql for proper formatting
   -- Execute kpi_queries.sql for analysis
   ```

2. **Dashboard Access**
   - Open `Coffee_Shop_Sales_Dashboard.pbix` in Power BI Desktop
   - Refresh data connections to your MySQL database
   - Explore interactive visualizations

3. **Custom Analysis**
   - Modify SQL queries for specific date ranges
   - Add additional KPIs as needed
   - Export results for presentations

## 📌 Business Recommendations

Based on the analysis:

1. **Staffing Optimization**: Increase staff during 8-10 AM peak hours
2. **Weekend Promotions**: Implement targeted campaigns to boost weekend sales
3. **Product Focus**: Expand hot chocolate and espresso varieties (top performers)
4. **Inventory Management**: Align stock levels with hour-by-hour demand patterns
5. **Location Strategy**: Replicate Hell's Kitchen's successful practices across other locations

## 🔄 Future Enhancements

- [ ] Predictive analytics for sales forecasting
- [ ] Customer segmentation analysis
- [ ] Seasonal trend identification
- [ ] Real-time dashboard with automated data refresh
- [ ] Integration with POS system for live updates
- [ ] Profitability analysis by product and location

## 📝 Technical Skills Demonstrated

- Advanced SQL (Window Functions, CTEs, Complex Joins)
- Data Transformation & Cleaning
- KPI Development & Business Metrics
- Data Visualization & Dashboard Design
- Business Intelligence Analysis
- Performance Optimization
- Storytelling with Data

## 👤 Author

**[Ahmed Rafi]**
- LinkedIn: [www.linkedin.com/in/rafianalytics]
- Email: [ahmedrafi.analytics@gmail.com]

## 📄 License

This project is available for educational and portfolio purposes.

---

⭐ If you found this project helpful, please consider giving it a star!

**Tags**: `data-analytics` `sql` `power-bi` `business-intelligence` `dashboard` `mysql` `data-visualization` `kpi-analysis`
