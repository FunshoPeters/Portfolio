# Portfolio
#### My Data Analytics and Marketing Analytics Portfolio on Github.

## Data Analyst Portfolio Project: Sales Management
![alt text](https://github.com/FunshoPeters/Portfolio/blob/main/images/Alt-Version__Data-Analyst-Portfolio-Project-%E2%80%93-Sales-Management-%E2%80%93-FunshoPeters.jpg "Salary by Position")
* Created a tool that estimates data science salaries (MAE ~ $ 11K) to help data scientists negotiate their income when they get a job.
* Scraped over 1000 job descriptions from glassdoor using python and selenium
* Engineered features from the text of each job description to quantify the value companies put on python, excel, aws, and spark. 
* Optimized Linear, Lasso, and Random Forest Regressors using GridsearchCV to reach the best model. 
* Built a client facing API using flask 

### The Scenario

I am a data analyst working in the marketing analyst team at Adventure Works.  Steve, the sales manager emailed me the following business request;

__*Steven  - Sales Manager:*__

__*Hi Funsho,*__

__*I hope you are doing well. We need to improve our internet sales reports and want to move from static reports to visual dashboards.*__

__*Essentially, we want to focus it on how much we have sold of what products, to which clients and how it has been over time.
Seeing as each sales person works on different products and customers it would be beneficial to be able to filter them also.*__

__*We measure our numbers against budget so I added that in a spreadsheet so we can compare our values against performance. 
The budget is for 2021 and we usually look 2 years back in time when we do analysis of sales.*__

__*Let me know if you need anything else!*__

__*Steven*__

### Business Request Overview

The business request for this data analyst project is for an Executive Sales Report for the sales managers. The table below breaks down the request, the role of the person that made the request, the purpose of the request and the tools I will need.

| Role  | Request | Purpose | Acceptance Criteria |
| ------------- | ------------- | ------------ | ------------- |
| Sales Manager  | To get a dashboard overview of internet sales  | Can follow better which customers and products sells the best | A Power BI dashboard which updates data once a day  |
| Sales Representative  | A detailed overview of Internet Sales per Customers  | Can follow up my customers that buys the most and who we can sell more to | A Power BI dashboard which allows me to filter data for each customer  |
| Sales Representative  | A detailed overview of Internet Sales per Products  | Can follow up my Products that sells the most | A Power BI dashboard which allows me to filter data for each Product  |
| Sales Manager  | A dashboard overview of internet sales  | Follow sales over time against budget | A Power Bi dashboard with graphs and KPIs comparing against budget.  |

### The Data Source

The dataset is taken from the AdventureWorks sample dataset on the Microsoft website. I chose the Data Warehouse version which has been structured for analysis purpose. 

The data can be found [here](https://learn.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-ver15&tabs=ssms).

### Data Cleansing & Transformation with SQL

I setup a practice environment that consisted of SQL Server. Next,I then went through the data to understand tables and columns I would need for my report, I then cleaned them and transformed for analysis purpose.
 
***How I cleaned and Transformed:***
- Used the **AS** Statement to rename the coumns.
- Selected only the columns that were relevant to the request.
- Used the **LET** statment to shorten the months (i.e January became 'Jan').
- Used a **CASE** Statemnt for the gender colums, changing M and F to Male and Femmale.
- Used the **LEFT JOIN** statement to a cloumn for Customer City from another table.
- Used the **ORDER BY** Statement to order.

Below are the SQL statements for cleansing and transforming necessary data.

#### DIM_Calendar:

```sql
-- Cleansed DIM_Date Table --
SELECT 
  [DateKey], 
  [FullDateAlternateKey] AS Date, 
  [EnglishDayNameOfWeek] AS Day, 
  [EnglishMonthName] AS Month, 
  Left([EnglishMonthName], 3) AS MonthShort,   -- Useful for front end date navigation and front end graphs.
  [MonthNumberOfYear] AS MonthNo, 
  [CalendarQuarter] AS Quarter, 
  [CalendarYear] AS Year 
FROM 
 [AdventureWorksDW2019].[dbo].[DimDate]
WHERE 
  CalendarYear >= 2019
```


#### DIM_Customers:

```sql
-- Cleansed DIM_Customers Table --
SELECT 
  c.customerkey AS CustomerKey, 
  c.firstname AS [First Name], 
  c.lastname AS [Last Name], 
  c.firstname + ' ' + lastname AS [Full Name],   -- Combined First and Last Name
  CASE c.gender WHEN 'M' THEN 'Male' WHEN 'F' THEN 'Female' END AS Gender,
  c.datefirstpurchase AS DateFirstPurchase, 
  g.city AS [Customer City] -- Joined in Customer City from Geography Table
FROM 
  [AdventureWorksDW2019].[dbo].[DimCustomer] as c
  LEFT JOIN dbo.dimgeography AS g ON g.geographykey = c.geographykey 
ORDER BY 
  CustomerKey ASC -- Ordered List by CustomerKey
```


#### DIM_Products:

```sql
-- Cleansed DIM_Products Table --
SELECT 
  p.[ProductKey], 
  p.[ProductAlternateKey] AS ProductItemCode, 
  p.[EnglishProductName] AS [Product Name], 
  ps.EnglishProductSubcategoryName AS [Sub Category], -- Joined in from Sub Category Table
  pc.EnglishProductCategoryName AS [Product Category], -- Joined in from Category Table
  p.[Color] AS [Product Color], 
  p.[Size] AS [Product Size], 
  p.[ProductLine] AS [Product Line], 
  p.[ModelName] AS [Product Model Name], 
  p.[EnglishDescription] AS [Product Description], 
  ISNULL (p.Status, 'Outdated') AS [Product Status] 
FROM 
  [AdventureWorksDW2019].[dbo].[DimProduct] as p
  LEFT JOIN dbo.DimProductSubcategory AS ps ON ps.ProductSubcategoryKey = p.ProductSubcategoryKey 
  LEFT JOIN dbo.DimProductCategory AS pc ON ps.ProductCategoryKey = pc.ProductCategoryKey 
order by 
  p.ProductKey asc
```


#### FACT_InternetSales:

```sql
-- Cleansed FACT_InternetSales Table --
SELECT 
  [ProductKey], 
  [OrderDateKey], 
  [DueDateKey], 
  [ShipDateKey], 
  [CustomerKey], 
  [SalesOrderNumber], 
  [SalesAmount]  
FROM 
  [AdventureWorksDW2019].[dbo].[FactInternetSales]
WHERE 
  LEFT (OrderDateKey, 4) >= YEAR(GETDATE()) -2 -- Ensures we always only bring two years of date from extraction.
ORDER BY
  OrderDateKey ASC
```


### Data Model

The data model after the cleaned and prepared tables were read into Power BI is shown in the screenshot below.

![alt text](https://github.com/FunshoPeters/Portfolio/blob/main/images/20221005-144711253.png "Data Model")

### Sales Management Dashboard in Power Bi

The finished sales management dashboard is a one page dashboard and overview, there are two other table for Customers Details and Product Details. All three dashboards provide an interactive overview that lets stackholders filter data for valuable business information. The ustomers Details and Product Details show combining tables for necessary details and visualizations to show sales over time, per customers and per products.

## Click the picture to to open the dashboard and try it out!

[![name](https://github.com/FunshoPeters/Portfolio/blob/main/images/1-Dashboard-screenshot.jpg)](https://app.powerbi.com/view?r=eyJrIjoiZDc2ZjYzYzctYzk4Mi00ZDk1LWEwZmQtNTE5OTZiNjFhZTQyIiwidCI6ImI3MTQ0ZjZlLWQ5NjQtNDFkNi1iM2Y5LWY3OTUyZTQ3YjY0MSJ9)
