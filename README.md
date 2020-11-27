Sales Insights Data Analysis Project

*Data Analysis Using SQL*

1. Show all customer records

  use sales;
  SELECT * FROM customers;
  
2. Show total number of customers

  SELECT count(*) FROM customers;

3. Show transactions for Chennai market (market code for chennai is Mark001)

  SELECT * FROM transactions WHERE market_code='Mark001';

4. Show distinct product codes that were sold in chennai.

  SELECT distinct product_code FROM transactions where market_code='Mark001';
  
5. Show transactions where currency is US dollars

  SELECT * from transactions where currency="USD";
   
6. Show transactions in 2020 join by date table

  SELECT 
      t.*, d.*
  FROM
      transactions t
          INNER JOIN
      date d ON t.order_date = d.date
  WHERE
      d.year = 2020;
      
 7. Show total revenue in year 2020
 
  SELECT 
      SUM(t.sales_amount)
  FROM
      transactions t
          INNER JOIN
      date d ON t.order_date = d.date
  WHERE
      d.year = 2020
          AND t.currency = 'INR\r'
          OR t.currency = 'USD\r';
          
8. Show total revenue in year 2020, January Month

  SELECT 
      SUM(t.sales_amount) AS total_sales_amount
  FROM
      transactions t
          JOIN
      date d ON t.order_date = d.date
  WHERE
      d.year = 2020
          AND d.month_name = 'January'
          AND (t.currency = 'INR\r'
          OR t.currency = 'USD\r'
  );
  
9. Show total revenue in year 2020 in Chennai

SELECT 
    SUM(t.sales_amount)
FROM
    transactions t
        INNER JOIN
    date d ON t.order_date = d.date
WHERE
    d.year = 2020
        AND t.market_code = 'Mark001';
        
  
*Data Analysis Using Power BI*

1. Formula to create norm_amount column

= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)
