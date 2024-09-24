## Sales Insights (Brick & mortar business) Data Analysis Project
![text](https://github.com/elsayedg/Sales-Insights-Brick-and-mortar-business/blob/main/Pic/Cover%20Photo_Sales%20Insights%20Brick%20%26%20mortar%20business.jpg)

1. SQL database dump is in db_dump.sql file above. Download  [db_dump.sql](https://github.com/elsayedg/Sales-Insights-Brick-and-mortar-business/blob/main/db_dump.sql) file to your local computer and import it.

### Data Analysis Using SQL

1. Show all customer records

    `SELECT * FROM customers;`

1. Show total number of customers

    `SELECT count(*) FROM customers;`

1. Show transactions for Chennai market (market code for chennai is Mark001

    `SELECT * FROM transactions where market_code='Mark001';`

1. Show distrinct product codes that were sold in chennai

    `SELECT distinct product_code FROM transactions where market_code='Mark001';`

1. Show transactions where currency is US dollars

    `SELECT * from transactions where currency="USD"`

1. Show transactions in 2020 join by date table

    `SELECT transactions.*, date.*
     FROM transactions JOIN date
     ON transactions.order_date=date.date
     where date.year=2020;`

1. Show total revenue in year 2020,

    `SELECT SUM(transactions.sales_amount)
     FROM transactions JOIN date
     ON transactions.order_date=date.date
     where date.year=2020 and transactions.currency="INR" or transactions.currency="USD";`
	
1. Show total revenue in year 2020, January Month,

    `SELECT SUM(transactions.sales_amount)
    FROM transactions JOIN date
    ON transactions.order_date=date.date
    where date.year=2020 and and date.month_name="January"
    and (transactions.currency="INR" or transactions.currency="USD");`

1. Show total revenue in year 2020 in Chennai

    `SELECT SUM(transactions.sales_amount)
     FROM transactions JOIN date
     ON transactions.order_date=date.date
     where date.year=2020
     and transactions.market_code="Mark001";`


Data Analysis Using Power BI
============================

### Key Insight Dashboard

   ![alt text](https://github.com/elsayedg/Sales-Insights-Brick-and-mortar-business/blob/main/Pic/1-%20Key%20Insights.png)

* Sales Overview: This dashboard provides a high-level overview of sales performance, including total sales, sales by region, and sales by product.
* Sales Trend: This dashboard shows the trend of sales over time.
* Top Customers: This dashboard shows the top 5 customers by total sales.


#### DAX Formula Used to create norm_amount column for USD Currency


`= Table.AddColumn(sales_transactions, "sales_amount_normlized", each if [currency] = "USD" then [sales_amount]*75 else [sales_amount])`

### Profit Analysis Dashboard

   ![alt text](https://github.com/elsayedg/Sales-Insights-Brick-and-mortar-business/blob/main/Pic/2-%20Profit%20Analysis.png)
* as you can see we dive deep into 2020 year to see the trend and all other profit analysis
* it provides other dimensions analysis for the Revenue by showing the % of each region's customer and market besides the % of Profit Contribution from the Total Profit


#### DAX Formula Used to create norm_amount column for USD Currency

* `Revenue Contribution % = DIVIDE([Revenue],CALCULATE([Revenue],ALL('sales products'),ALL('sales customers'),ALL('sales markets')))`
* `Profit Margin Contribution % = DIVIDE([Total profit Margin],CALCULATE([Total profit Margin],ALL('sales products'),ALL('sales customers'),ALL('sales markets')))`
* `Profit Margin % = DIVIDE([Total profit Margin],[Revenue],0)`

### Performance Insights Dashboard

   ![alt text](https://github.com/elsayedg/Sales-Insights-Brick-and-mortar-business/blob/main/Pic/3-%20Performance%20Insights.png)
* as you can see we analyze the performance of 2020 to see the difference between this year and the last one through a combo chart
* More important is identifying every market in which region contributes to our lose in profit 


#### DAX Formula Used to create norm_amount column for USD Currency

* `Revenue LY = CALCULATE([Revenue],SAMEPERIODLASTYEAR('sales date'[date]))`
* `Profit Target = GENERATESERIES(-0.05, 0.15, 0.01)`
* `Profit Target Value = SELECTEDVALUE('Profit Target'[Profit Target])`
* `Target Diff = [Profit Margin %] - 'Profit Target'[Profit Target Value]`

#### Resources Download
* 3 dashboards in one PDF [here](https://github.com/elsayedg/Sales-Insights-Brick-and-mortar-business/blob/main/Sales%20Report.pdf) 
* Power BI file [here](https://github.com/elsayedg/Sales-Insights-Brick-and-mortar-business/blob/main/sales.pbix) but, you must install the sales database as mentioned above to work on your PC. 
