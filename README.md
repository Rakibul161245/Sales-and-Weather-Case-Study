# Case Study: The Impact of Weather on Sales

## 1. Statement of the Business Task
The goal of this case study is to determine if weather conditions impact sales performance. The business wants to understand how weather factors such as temperature, rainfall, and wind speed influence the quantity of products sold and sales revenue. This will help optimize marketing strategies and inventory management.

## 2. Data Sources

### Sales Data:
- **Date**: The date of the sale.
- **Product_ID**: A unique identifier for each product.
- **Product_Name**: The name of the product.
- **Quantity_Sold**: The number of units sold on a given day.
- **Sales_Amount**: The total sales revenue in dollars on a given day.

### Weather Data:
- **Date**: The date of the weather report.
- **Temp9am** and **Temp3pm**: Temperature readings at 9 AM and 3 PM.
- **MinTemp** and **MaxTemp**: The minimum and maximum temperatures for the day.
- **Rainfall**: Total rainfall recorded for the day.
- **RainToday**: Whether or not it rained today (Boolean).
- **Evaporation**, **Sunshine**: Other weather metrics like evaporation and sunshine.
- **WindGustDir** and **WindGustSpeed**: The direction and speed of the strongest gust of wind.
- **WindDir9am**, **WindDir3pm**: Wind direction at 9 AM and 3 PM.
- **WindSpeed9am**, **WindSpeed3pm**: Wind speed at 9 AM and 3 PM.
- **Humidity9am**, **Humidity3pm**: Humidity levels at 9 AM and 3 PM.
- **Pressure9am**, **Pressure3pm**: Atmospheric pressure at 9 AM and 3 PM.
- **Cloud9am**, **Cloud3pm**: Cloud cover at 9 AM and 3 PM.

Both tables are linked by the Date field, allowing for analysis of how weather influences daily sales.

## 3. Data Cleaning and Manipulation
Before performing the analysis, several data cleaning steps were applied:

- **Handling Missing Data**: Rows with missing weather data were either filled with averages or excluded if necessary.
- **Data Consistency**: Ensured that dates between the sales and weather tables matched.
- **Outliers**: Identified unusual sales values and extreme weather conditions for review.
- **Data Types**: Ensured numerical and date data were properly formatted.

### SQL Queries for Data Cleaning:

```sql
-- Check for any missing data in sales
SELECT * FROM sales WHERE Quantity_Sold IS NULL OR Sales_Amount IS NULL;

-- Check for missing weather data
SELECT * FROM weather WHERE Temp9am IS NULL OR Rainfall IS NULL;

-- Ensure date consistency between both tables
SELECT s.Date, w.Date FROM sales s
LEFT JOIN weather w ON s.Date = w.Date
WHERE w.Date IS NULL;

## 4. Analysis Summary
The following analysis was conducted:

- **Correlation Analysis**: Examined the correlation between weather variables (e.g., temperature, rainfall) and sales performance.
- **Sales Trends Based on Weather**: Investigated how specific weather conditions affected sales.
- **Top Weather Conditions for Sales**: Identified the ideal weather conditions associated with the highest sales.
- **Product-Specific Trends**: Analyzed if certain product categories were more affected by weather conditions.

### SQL Query for Analysis:
```sql
-- Correlation between weather and sales performance
SELECT w.Date, w.Temp9am, w.Temp3pm, w.Rainfall, s.Quantity_Sold, s.Sales_Amount
FROM weather w
JOIN sales s ON w.Date = s.Date
ORDER BY w.Date;

