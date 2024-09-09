# Coffee Shop Sales Analysis☕

## Table of Contents

- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Tools](#tools)
- [Data Preparation](#data-preparation)
- [Explanatory Data Analysis](#explanatory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results](#results)
- [Recommendation](#recommendation)
- [Limitations](#limitations)
- [References](#references)

### Project Overview
This project analyzes coffee shop sales data to reveal customer preferences, peak times, and top products that drive growth. By unlocking these insights, it empowers businesses to refine their strategies, maximize revenue, and create memorable customer experiences. In a market where every choice matters, this analysis is key to staying ahead and thriving. Dive into the data to discover what makes your coffee shop truly stand out!

![georh](https://github.com/user-attachments/assets/64cc62b6-975f-4e56-a60e-31ea6278c25a)
![Power BI Desktop 9_5_2024 7_00_29 PM](https://github.com/user-attachments/assets/78109407-d851-4044-97b4-ab517727f10a)

### Data Source

Sales data: The data is sourced from Maven Analytics as an Excel file format containing sales transaction records January to June 2023.The dataset included columns such as;Transaction ID, Transaction Date, Transaction Time, Transaction Quantity, Store ID, Store Location, Product ID, Unit Price, Product Category, and Product Type.             
### Tools

- Power BI: Data Transformation and cleaning, generating interactive dashboard.[Download here](https://www.microsoft.com/en-us/download/details.aspx?id=58494)
- Power Point: Designing of the dashboard.[Download here](https://www.microsoft.com/en-us/microsoft-365/powerpoint)

### Data Preparation


1.**Data Cleaning**

- Handling Missing Values: Identified and addressed missing values in essential columns (e.g., Transaction Date, Unit Price). Missing entries were either replaced with appropriate defaults or removed to maintain data quality.
- Removing Duplicates: Checked for duplicate records using Transaction ID as a unique identifier and removed any duplicates to ensure data integrity.
- Correcting Data Types: Converted all columns to their appropriate data types, such as ensuring that Transaction Date was in a date format and Unit Price was in a numerical format'

2.**Data Transformation**

- Date and Time Formatting: Extracted additional features like the day of the week, month, and hour from Transaction Date and Transaction Time to analyze sales patterns over different time intervals.
- Creating Calculated Columns: Added calculated columns such as Total Sales (Transaction Quantity multiplied by Unit Price) to facilitate analysis of revenue generation.
- Categorization: Grouped products into broader categories to simplify analysis (e.g., merging subcategories into main categories like "Beverages" or "Pastries").
- Creation of a Date Table: Created a dedicated Date Table to support time-based analysis, such as daily sales trends, monthly growth, and peak sales periods covering all dates within the analysis period (January 1, 2023, to June 30, 2023). The table included columns for Date, Year, Month, Day, Quarter, Week Number, and Day of the Week.
- Relationship Setup: Established a relationship between the Date Table and the Transaction Date field in the sales data to enable accurate time intelligence calculations and dynamic filtering across the dashboard.
  
3.**Data Integration**

- Merging Datasets: Combined multiple data sources where necessary, such as integrating product details with sales records to provide a complete view of sales performance by product type and category.
- Normalization: Standardized data formats to ensure consistency across the datasets (e.g., uniform currency formatting).

4.**Data Validation**

- Quality Checks: Performed quality checks to verify data accuracy, completeness, and consistency. Outliers and anomalies were identified and handled to avoid skewed results.
- Final Review: Conducted a final review of the dataset, using descriptive statistics and summary reports to ensure readiness for analysis.

### Explanatory Data Analysis

 **Sales Analysis**
1. **Total Sales**: What were the total sales figures for each month?
2. **MoM Sales Difference**: What is the difference in sales between the current month and the previous month?
3. **MoM Sales Difference in Percentage**: What is the month-over-month (MoM) percentage change in sales?

 **Footfall Analysis**
1. **Total Footfall**: What was the total number of customers for each month?
2. **MoM Footfall Difference**: How did footfall numbers change compared to the previous month?
3. **MoM Footfall Difference in Percentage**: What is the percentage change in footfall month-over-month?

 **Quantity Sold Analysis**
1. **Total Quantity Sold**: What was the total quantity of products sold each month?
2. **MoM Quantity Difference**: What is the difference in the quantity sold compared to the previous month?
3. **MoM Quantity Difference in Percentage**: What is the percentage change in quantity sold month-over-month?

**Sales vs. Days of the Month Analysis**
1. **Daily Sales Trend**: What is the sales trend over the days of each month?
2. **Sales Peak Days**: Which days of the month have the highest sales?
3. **Sales Average Line**: How do daily sales compare to the overall monthly average?

 **Product Analysis**
1. **Product Category Performance**: Which product categories generated the most sales?
2. **Product Type Performance**: Which specific product types were the top sellers?
3. **Product Trends Over Time**: Are there any seasonal or monthly trends in product performance?

 **Weekend vs. Weekdays Analysis**
1. **Sales Comparison**: How do sales on weekends compare to weekdays?
2. **Customer Behavior**: What is the difference in customer behavior between weekends and weekdays?
3. **Revenue Proportion**: What percentage of total sales is attributed to weekends vs. weekdays?

 **Store Location Analysis**
1. **Top Performing Locations**: Which store locations generated the highest sales?
2. **Location-Based Trends**: Are there any noticeable trends in sales based on store location?
3. **Location and Footfall**: How does footfall differ across various store locations, and how does it impact sales?

### Data Analysis
```DAX functions

Sales = sumx(Transactions,Transactions[transaction_qty] * Transactions[unit_price])

```

```DAX functions

CM Sales = 
    VAR selected_month = SELECTEDVALUE('Date Table'[Month-Year])
    RETURN
        TOTALMTD(CALCULATE([Sales], 'Date Table'[Month-Year] = selected_month), 'Date Table'[Date])
```
```DAX functions
PM Sales = CALCULATE([CM Sales],DATEADD('Date Table'[Date], -1,MONTH))
```
```DAX functions
MoM Growth & Diff Sales = 
    VAR month_diff = [CM Sales] - [PM Sales]
    VAR mom = ([CM Sales] - [PM Sales]) / [PM Sales]
    VAR _sign = IF(month_diff > 0, "+", "")
    VAR _sign_trend = IF(month_diff > 0, "▲", "▼")
    RETURN
        _sign_trend & " " & _sign & FORMAT(mom, "#0.0%") & " | " & _sign & FORMAT(month_diff / 1000, "0.0K") & " vs PM"
```
### Results
The summary of my findings are as follows:

- **Sales Growth**: Sales, footfall, and quantity sold have all shown a positive increase compared to the previous month, signaling strong growth momentum and improved customer engagement.

- **Daily and Monthly Trends**: An interactive date calendar reveals daily sales peaks and patterns, helping to identify the most and least active days. A line chart with an average sales line provides a clear view of overall monthly sales momentum, highlighting key trends and fluctuations.

- **Top Store Locations**: Hell’s Kitchen emerges as the top-performing location with the highest sales, while Astoria and Lower Manhattan show the most dynamic growth rates, indicating potential hotspots for further expansion or targeted marketing efforts.

- **Customer Favorites**: The top 5 best-selling product types are Barista Espresso, Brewed Chai Tea, Hot Chocolate, Gourmet Brewed Coffee, and Brewed Herbal Tea. These insights point to customer preferences that can help guide inventory management and promotional strategies.

- **Revenue Patterns**: Most revenue is generated during weekdays, suggesting that weekday-focused promotions could be particularly effective. Understanding these patterns can help tailor marketing efforts to maximize sales during peak times.

- **Product Popularity**: Coffee continues to lead as the most popular product category, with tea closely following. This preference can guide future product development and promotional campaigns to cater to customer tastes.

### Recommendation 
Based on my findings, here are my targeted recommendations:

- **Enhance Weekday Promotions**: Given that weekdays generate the most revenue, lets consider implementing targeted promotions, discounts, or special events on weekdays to boost sales further.

- **Focus on High-Growth Locations**: Lets Invest in marketing and expansion efforts in high-growth locations like Astoria and Lower Manhattan since these areas show dynamic growth and could benefit from additional resources and targeted campaigns.
  
- **Optimize Product Inventory**: Prioritize stocking and promoting the top-selling products—Barista Espresso, Brewed Chai Tea, Hot Chocolate, Gourmet Brewed Coffee, and Brewed Herbal Tea. Ensure these items are prominently featured and available to meet customer demand.

- **Leverage Daily Sales Patterns**: Use of insights from the daily sales calendar to adjust staffing levels, inventory management, and marketing efforts. For  example, preparing for high sales days with additional staff and stock.

- **Strengthen Coffee and Tea Offerings**: Since coffee is the top category and tea is also popular, lets consider expanding our offerings in these areas by Introduce new coffee and tea variations or seasonal specials to attract and retain customers.

- **Analyze and Adapt Store-Specific Strategies**: Tailoring of marketing and sales strategies to individual store locations based on their performance. Hell’s Kitchen, being the top performer, may benefit from loyalty programs or exclusive promotions, while other locations could use strategies to replicate its success.

- **Monitor and Adjust Sales Trends**: Continuously tracking sales trends using our monthly line chart and daily calendar. Adjusting strategies based on observed patterns to stay ahead of market trends.

### Limitations

-**Limited Data Scope**: The analysis is constrained by the data being limited to a specific period hence restricting the comprehensiveness of the insights.
-**External Factors**: Changes in market conditions, such as seasonal trends, economic fluctuations, or local events, might affect sales but could not be captured.
-**Static Analysis**: The analysis is based on historical data hence could not account for real-time changes .

### References
- [Data Science for Business](https://www.researchgate.net/publication/256438799_Data_Science_for_Business)
- [Customer behavior analysis: What you need to know](https://www.qualtrics.com/experience-management/customer/customer-behavior-analysis/) 





