# Portfolio
#### My Data Analytics and Marketing Analytics Portfolio on Github.

## [Data Analyst Portfolio Project: Sales Management](https://github.com/FunshoPeters/Data-Analyst-Project-Sales-Management) 
![alt text](https://github.com/FunshoPeters/Portfolio/blob/main/images/Alt-Version__Data-Analyst-Portfolio-Project-%E2%80%93-Sales-Management-%E2%80%93-FunshoPeters.jpg "Data Analyst Portfolio Project - Sales Management")
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

### Data Cleansing & Transformation with SQL

I setup a practice environment that consisted of SQL Server. Next,I then went through the data to understand tables and columns I would need for my report, I then cleaned them and transformed for analysis purpose.
 
***How I cleaned and Transformed:***
- Used the **AS** Statement to rename the coumns.
- Selected only the columns that were relevant to the request.
- Used the **LET** statment to shorten the months (i.e January became 'Jan').
- Used a **CASE** Statemnt for the gender colums, changing M and F to Male and Femmale.
- Used the **LEFT JOIN** statement to a cloumn for Customer City from another table.
- Used the **ORDER BY** Statement to order.

