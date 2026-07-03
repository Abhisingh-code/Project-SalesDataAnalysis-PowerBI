# Sales-Data-Analysis Dashboard

### Dashboard Link : https://app.powerbi.com/groups/me/reports/dd477caa-bba9-4174-92a8-9d8749c76d32/78bae55938c7b3fdd5f2?redirectedFromSignup=1&experience=power-bi


## Problem Statement

This dashboard helps the business understand its sales performance better. It helps the company know how their products are performing in terms of sales, profit, and quantity sold. Through different visuals, they get to know their top-performing and low-performing products, & thus they can improve their strategies by identifying these areas. It also lets them understand sales trends over time, city-wise performance, and the impact of discounts and promotions.

Since, there is a significant gap between top-performing and low-performing products, thus the company must work on improving sales of low-performing products.

Also since total sales is high but profit is comparatively lower, thus they must try to optimize discount strategies to improve profitability.


### Steps followed

Step 1 : Load data into Power BI Desktop, dataset contains sales transaction data excel file.

Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.

Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".

Step 4 : In "Dim Promotion" table in Power Query Editor, under add column, conditional column was selected and column named  "Percentage" was added and in "PromotionID" "0" represents no discount was given.

Step 5 :It was observed that in none of the columns errors & empty values were present except columns named "Price Per Unit", "Total Sales", "Discount Percentage", "Discount Value", "Net       Sales" contains null values in (Fact Table).

Step 6 : Under Home tab, Merge Queries, Left Outer join was applied between "Fact table" and "Dim Product" using ProductID,

      (a) For bringing values to "Price Per Unit" column

      (b) For "Total Sales", under add column, Custom column was selected ("Unit sold" and "Price Per Unit" columns was multiplied)

      (c) Left Outer join was applied between "Fact table" and "Dim Promotion" using "PromotionID" for "Discount percentage" and null values was replaced by "0"

      (d) For "Discount Value" ("Total Sales" and "Discount Value" was multiplied and divided by 100) and changed the column name to "Discount"

      (e) For "Net Sales" ("Total Sales" and "Discount" was subtracted)

      (f) "Profit" column was added in "Fact Table" (0.1 * "Net Sales") 

## Top/Bottom 5 Analysis

Step 7 : product performance visuals were created to represent :

      (a) Top 5 products by sales,

     (using Stacked bar chart) field named "Product Name" was added to the y-axis and "Net Sales"(Sum) was added to x-axis, Using visual level filter from the filters pane, Top N filtering was used.

      (b) Bottom 5 products by sales,

      (using Stacked bar chart) field named "Product Name" was added to the y-axis and "Net Sales"(Sum) was added to x-axis, Using visual level filter from the filters pane, Top N filtering was used and under show items Bottom was selected.

      (c) Top 5 products by quantity

      (using Stacked bar chart) field named "Product Name" was added to the y-axis and "Unit Sold"(Sum) was added to x-axis, Using visual level filter from the filters pane, Top N filtering was used.

      (d) Bottom 5 products by quantity
 
     (using Stacked bar chart) field named "Product Name" was added to the y-axis and "Unit Sold"(Sum) was added to x-axis, Using visual level filter from the filters pane, Top N filtering was used and under show items Bottom was selected.

     (e) Top 5 products by profit

     (using Stacked bar chart) field named "Product Name" was added to the y-axis and "Profit"(Sum) was added to x-axis, Using visual level filter from the filters pane, Top N filtering was used.

     (f) Bottom 5 products by profit

     (using Stacked bar chart) field named "Product Name" was added to the y-axis and "Profit"(Sum) was added to x-axis, Using visual level filter from the filters pane, Top N filtering was used and under show items Bottom was selected.

## Overview

Step 8 : A line chart was added to represent "Sales Trends by Period"(under visualization pane, under build visual Field named "Date(dd/mm/yyyy) was added for year, quarter, month and       day" to the x-axis and "Net Sales"(Sum) was added to y-axis). and to see different periods drill down, drill up and go to next level in hierarchy can be used. 

Step 9 : A Scatter chart was added to represent "Profit v/s Net Sales" relationship under visualization pane, under build visual field named "profit"(Don't Summarize) was added to x-axis   
and "Net Sales"(Don't Summarize) was added to y-axis.

Step 10 : A Stacked bar chart was added to represent "Average Discount by Promotion Categories" and "Discount"(Average) was added to x-axis and "Promotion name" was added to y-axis and blank was removed because it has no significance and it only showed where discount was not allotted.

Step 11 : A Clustered bar chart was added to represent "Sales by City" and "City" was added to y-axis and "Net Sales"(Sum) was added to x-axis. 

Step 12 : In "Fact table" an Index Column was added and renamed it as "OrderID" and it will used to identify each order because each order in this tables represents one unique order  

Step 13 : A card visuals were added to represent "Number of Orders" and "OrderID"[Count(Distinct)] was added in the fields.

Step 14 : Two new tables were added, Under Modelling tab-new table

     (1) Date Table 1(DAX)
         Date Table 1 = CALENDARAUTO()

     (2) Date Table 2(DAX)  
         Date Table 2 = CALENDARAUTO() 
and as we want the data type same for the both the tables, In table view, under column tools tab, Data type(Date) was selected and Format(Long date) was selected and in model view, one to many relationship was created between "Fact table" and the "Date Tables(1 & 2)" and the "Date Table 2" was not kept active.


## Comparison Sales/Profit/Quantity Approach 1 (It is not a recommended model cause it will increase the size Cause two Dax measures were used here to create Date Table)

Step 15 : Slicers were added for filtering data by field  "Date" form "Date Table 1" and "Date table 2".

Step 16 : Measures were created to calculate Total Sales, Total Profit and Total Quantity sold.

      (1) Total Sales(DAX)

          Sum of Net Sales = CALCULATE(SUM('Fact Table'[Net Sales   ]),ALL('Date Table 1'),USERELATIONSHIP('Date Table 2'[Date],'Fact Table'[Date (dd/mm/yyyy)]))

      (2)Total Profit(DAX)

         Total Profit = CALCULATE(SUM('Fact Table'[Profit]),ALL('Date Table 1'),
         USERELATIONSHIP('Date Table 2'[Date],'Fact Table'[Date (dd/mm/yyyy)]))

      (3)Total Quantity sold(DAX)

         Total Quantity Sold = CALCULATE(SUM('Fact Table'[Units Sold]),ALL('Date Table 1'),
         USERELATIONSHIP('Date Table 2'[Date],'Fact Table'[Date (dd/mm/yyyy)]))

Step 17 : Clustered Column Charts were added to represent Total Sales, Total Profit and Total Quantity sold.
Total Sales, "Net Sales"(Sum) and "Sum of net sales" was added in y-axis and then renamed as "sales 1" and "Sales 2".
Total Profit, "Profit"(Sum) and "Total Profit" was added in y-axis and then renamed as "Profit 1" and "Profit 2".
Total Quantity sold, "Units Sold"(Sum) and "Quantity Sold" was added in y-axis and then renamed as "Quantity 1" and "Quantity 2".


## Comparison Sales/Profit/Quantity Approach 2 

Step 18 : Slicers were added for filtering data by field "Date (dd/mm/yyyy)" and then renamed as "Date Filter 1" and "Date Filter 2"
and then six stacked bar charts were added to represent Total Sales, "Net sales"(Sum) added in x-axis, Total Profit, "Profit"(Sum) added in x-axis, Total Quantity sold, "Units Sold"(Sum) added in x-axis,select "Date Filter 1" and under format tab, select Edit Interactions and select none for charts under "Date Filter 2" and same process was used for charts under"Date Filter 2  


## Table Visual

Step 19 : A table visual was created to repersent fields named Customer ID, OrderID, Date(dd/mm/yyyy), Discount(Don't Summarize), Discount Percentage(Don't Summarize), Net sales(Don't Summarize), Price Per Unit(Don't Summarize), ProductID, Profit(Don't Summarize) ,PromotionID, Total sales(Don't Summarize), Units Sold(Don't Summarize). 

Step 20 : Slicers were added to Represent 
"Date" from (Date Table 1), 
"Customer Name" from (Dim Customers),
"Product Name" from (Dim Products),
"Promotion Name" from (Dim Promotion)

and new Dax Measure was created to make all slicers interact with each other

Sum Dim = SUM('Fact Table'[Net Sales   ])

now under Filters pane, Select customer Name, and in add data fields here add "Sum Dim", under show items, select is not blank and apply filter and same process was done for slicers named
"Date", "Product Name", "Promotion Name". 
 
Step 21 : The report was then published to Power BI Service.
Snapshot of Dashboard (Power BI Service)

(Dashboard snapshot)

Report Snapshot (Power BI DESKTOP)

(Report snapshot)


### Insights

A multi-page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard;

[1] Overall Performance

Total Sales = 122M

Total Profit = 12.2M

Total Quantity Sold = 7.1K 

[2] Sales Trends

Sales trend varies from year 2020 to 2024.

Some years show lower performance indicating fluctuations in business.

[3] Product Performance

Top 5 Products by Sales =

Apple iPhone 14

Apple MacBook Air

Sony Bravia 55" TV

Samsung Galaxy S21

HP Pavilion Laptop

Bottom 5 Products by Sales =

Tupperware Lunch Box

L'Oreal Shampoo

Nivea Body Lotion

Dove Soap Pack

Colgate Toothpaste

thus, higher revenue is generated from electronic products.

[4] City-wise Sales

Higher sales observed in cities like Bhopal, Kanpur and Indore.

Lower sales observed in cities like Bangalore and Hyderabad.

    thus, sales distribution is uneven across cities. 
 
[5] Discount & Promotion Analysis

Higher discounts observed in promotional categories like weekend and clearance sales.

    thus, promotions significantly impact sales.
  
[6] Profit vs Net Sales

Profit increases with increase in net sales.

    thus, both are positively correlated.
  
[7] Order Insights

Total Number of Orders ≈ 3.51K

    thus, moderate number of transactions contribute to total sales.
  


