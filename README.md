# AtliQ Hardwares  sales-insight-data-analysis
Sales Insights Data Analysis Project

 Atliq hardware is facing a lot of challenges the market is growing dynamically and the sales is going down so as  a data analyst I am going to analyse the data and build a report which  can acessed from anywhere even from a smartphone 

SQL database  db_dump_version_2.sql

## Data Analysis Using SQL

1 . Show all customer records

  `SELECT * FROM customers;`

 2 . Show total number of customers

   `SELECT count(*) FROM customers;`

 3 . Show transactions for Chennai market (market code for chennai is Mark001

   `SELECT * FROM transactions where market_code='Mark001';`

 4 . Show distrinct product codes that were sold in chennai

   `SELECT distinct product_code FROM transactions where market_code='Mark001';`

 5 . Show transactions where currency is US dollars

   `SELECT * from transactions where currency="USD"`

 6 . Show transactions in 2020 join by date table

   `SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;`

 7 . Show total revenue in year 2020,

   `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.currency="INR\r" or transactions.currency="USD\r";`

 8 . Show total revenue in year 2020, January Month,

   `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and and date.month_name="January" and (transactions.currency="INR\r" or transactions.currency="USD\r");`

 9 . Show total revenue in year 2020 in Chennai

   `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.market_code="Mark001";`

## Data Analysis Using Power BI
 1 . Formula to create normalized sales_amount 
 
   `= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)`
		 
 2 .  formula to create a new measure Revenue
 
   `= SUM('sales transctions'[sales_amount])`

 3 . formula to create a new measure Total Sales Qty
 
   `= SUM('sales transactions'[sales_qty])`
			
 4 . formula to create a new measure profit margin % 
 
   `= DIVIDE([Total profit_margin],[Revenue],0)`
		 
 5 . formula to create a new measure Profit margin contribution % 
 
   `= DIVIDE([Total profit_margin], CALCULATE([Total profit margin], ALL('sales product'), ALL('sales customers'), ALL('sales markets')))`
		 
 6 . formula to create a new measure Revenue contribution %
 
   `= DIVIDE([Revenue], CALCULATE([Revenue], ALL('sales product'), ALL('sales customers'), ALL('sales markets')))`
		 
 7 . formula to create a new measure Revenue LY ( last year)
 
   `= CALCULATE([Revenue],SAMEPERIODLASTYEAR('sales date'[date]))`
		 
 8 . formula to create a new measure profit target value 
 
   `= SELECTED VALUES('profit target[profit target])`
		 
 9 . formula to create a new measure target Diff
 
   `= [profit margin %]- 'profit target'[profit target value]` 
