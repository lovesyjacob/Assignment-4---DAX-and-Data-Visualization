# Assignment 4 – PowerBI DAX & Data Visualization

## Project Overview

This project involves analyzing e-commerce sales data using Power BI. The objective is to use DAX (Data Analysis Expressions) to transform the data, generate key metrics, and create compelling visualizations to gain insights into sales trends, profitability, and performance metrics.

## Data Sources

* `List of Orders.csv`

* `Order Details.csv`

* `Sales target.csv`

## Step 1: Data Preparation and Cleaning (Power Query)

Before modeling, the data was imported and cleaned using the Power Query Editor:

* Checked data types for consistency (e.g., Dates, Whole Numbers, Decimal Numbers).

* **Data Cleaning:** Identified trailing blank/null rows in the `List of Orders.csv` file (where all columns were empty) and successfully removed them using the "Remove Blank Rows" feature to ensure accurate analysis.

## Step 2: Data Modeling

Established relationships between the tables in the Model View prior to visualization:

* Created a **1-to-Many relationship** between `List of Orders` and `Order Details` using the `Order ID` column.

* Created a **Many-to-Many relationship** between `Sales target` and `Order Details` using the `Category` column.

## Step 3: Calculated Columns (DAX)

Added the following calculated columns to the `Order Details` table:

1. **Category Type:** Combined 'Category' and 'Sub-Category' into a single column.

   ```
   Category Type = 'Order Details'[Category] & " - " & 'Order Details'[Sub-Category]
   
   
   ```

2. **Revenue per Order:** Computed the total revenue per order.

   ```
   Revenue = 'Order Details'[Amount] * 'Order Details'[Quantity]
   
   
   ```

3. **Sales Category:** Categorized orders based on the average overall amount.

   ```
   Sales Category = 
   VAR AvgAmount = CALCULATE(AVERAGE('Order Details'[Amount]), ALL('Order Details'))
   RETURN IF('Order Details'[Amount] > AvgAmount, "Above Average", "Below Average")
   
   
   ```

## Step 4: Calculated Measures (DAX)

Created the following calculated measures to derive key insights:

1. **Order Count:** Counted the total unique orders.

   ```
   Order Count = DISTINCTCOUNT('Order Details'[Order ID])
   
   
   ```

2. **Average Profit in Delhi:** Calculated the average profit specifically for orders in Delhi.

   ```
   Avg Profit Delhi = 
   CALCULATE(AVERAGE('Order Details'[Profit]), 'List of Orders'[City] = "Delhi")
   
   
   ```

3. **Year-to-Date (YTD) Sales:** Calculated accumulated sales amount over time.

   ```
   YTD Sales = TOTALYTD(SUM('Order Details'[Amount]), 'List of Orders'[Order Date])
   
   
   ```

## Step 5: Data Visualization and Dashboard Formatting

Built and customized a professional dashboard with the following visualizations:

* **Sales Target Achievement (Clustered Column Chart):** Compared actual sales amounts against targets by category.

* **Max Profit Margin by Sub-Category (Donut Chart):** Analyzed the maximum profit achieved across different product sub-categories.

* **Monthly Sales Trend (Line Chart):** Visualized the sum of amounts over time (by Month).

* **Profit vs. Quantity (Scatter Chart):** Evaluated the relationship between quantity sold and profit yielded per sub-category.

* **Total Sales & Targets (KPI Cards):** Displayed high-level summary cards for Total Sales Amount and Total Target.

* **Minimum Target by Category (Table):** Used a table to dynamically display the minimum target threshold for each product category.

* **Sales Performance Matrix:** Cross-tabulated actual sales and targets across categories and months.

* **Geographic Sales Analysis (Map):** Highlighted total sales by city using bubble sizes.

* **Sales Distribution (Treemap):** Displayed sales volume distribution across sub-categories.

* **Order Count by State (Funnel Chart):** Visualized the distribution of order volumes across regions.

**Formatting Applied:**

* Added a clear, bold dashboard title using a text box.

* Updated default visual titles to professional, readable headings.
