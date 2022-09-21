WHERE EXAMPLE 1 - get a list of product IDs and product names that are in product category 1

SELECT
   
 product_id,
   
 product_name,
   
 product_category_id
FROM farmers_market.product
WHERE
   
 product_category_id = 1
LIMIT 5

-----------------------

WHERE EXAMPLE 2 - report everything a particular customer has ever purchased and how much they paid for it, sorted by market date, vendor ID, and product ID

SELECT 
   
 market_date, 
   
 customer_id, 
   
 vendor_id,
   
 product_id,
   
 quantity, 
   
 quantity * cost_to_customer_per_qty AS price 
FROM farmers_market.customer_purchases
WHERE customer_id = 4
ORDER BY market_date, vendor_id, product_id
LIMIT 5

---------------------------

FILTERING ON MULTIPLE CONDITIONS - find everything two customers in particular bought

SELECT 
   
 market_date, 
   
 customer_id, 
   
 vendor_id,
   
 product_id,
   
 quantity,

 quantity * cost_to_customer_per_qty AS price 
FROM farmers_market.customer_purchases
WHERE customer_id=3 
   
 OR customer_id = 5
ORDER BY market_date, customer_id, vendor_id, product_id

NOW SHOW WHAT WOULD HAPPEN (NOTHING WILL RETURN) IF WE USED AND

SELECT 
   
 market_date, 
   
 customer_id, 
   
 vendor_id,
   
 product_id,
   
 quantity,

 quantity * cost_to_customer_per_qty AS price 
FROM farmers_market.customer_purchases
WHERE customer_id = 3 
   
 AND customer_id = 5
ORDER BY market_date, customer_id, vendor_id, product_id

------------------------------

FILTERING USING MULTIPLE AND OR STATEMENTS - stuff in parentheses gets evaluated first - find products where product ID is in a certain range of values or equal to a given value

SELECT 
 
 product_id,

 product_name
FROM farmers_market.product
WHERE
   
 product_id = 10
   
 OR (product_id> 3
   
 AND product_id < 8)

--------------------------

FILTERING USING MULTIPLE COLUMNS - purchases made by customer 4 at vendor 7

SELECT 
 
 market_date,

 customer_id, 
   
 vendor_id, 
   
 quantity * cost_to_customer_per_qty AS price
FROM farmers_market.customer_purchases
WHERE 
   
 customer_id = 4
   
 AND vendor_id = 7

------------------------------

FILTERING WITH NOT EXACT CONDITIONS - find the booths that vendor 2 was assigned to before march 9 2019

SELECT *
FROM farmers_market.vendor_booth_assignments
WHERE
   
 vendor_id = 9
   
 AND market_date <= '2019-04-09'
ORDER BY market_date

———-------------------------

BETWEEN - booth assignments for vendor 7 for dates between march 2 and march 16 2019


FIRST WITHOUT BETWEEN

SELECT * 
FROM farmers_market.vendor_booth_assignments
WHERE
   
 vendor_id = 7
   
 AND (market_date >= '2019-04-02' and market_date <= ‘2019-04-16’)
ORDER BY market_date

NOW WITH BETWEEN

SELECT * 
FROM farmers_market.vendor_booth_assignments
WHERE
   
 vendor_id = 7
   
 AND market_date BETWEEN '2019-04-02' and '2019-04-16' 
ORDER BY market_date


-----------------------------------

IN - Customers with last names Diaz, Edwards, or Wilson

WITHOUT IN

SELECT
   
 customer_id, 
   
 customer_first_name,
   
 customer_last_name
FROM farmers_market.customer
WHERE
   
 customer_last_name = 'Diaz'
   
 OR customer_last_name = 'Edwards'
   
 OR customer_last_name = 'Wilson'
ORDER BY customer_last_name, customer_first_name

WITH IN

SELECT
   
 customer_id, 
   
 customer_first_name,

 customer_last_name
FROM farmers_market.customer
WHERE
   
 customer_last_name IN ('Diaz', 'Edwards', 'Wilson')
ORDER BY customer_last_name, customer_first_name

---------------------------

LIKE - Names like Jeremy

SELECT
   
 customer_id, 
   
 customer_first_name,
   
 customer_last_name
FROM farmers_market.customer
WHERE
   
 customer_first_name LIKE 'Jer%'

---------------------------

IS NULL - find the products where the product size is not given, or NULL

SELECT * 
FROM farmers_market.product
WHERE product_size IS NULL

--------------------------

TRIM - find the products where the product size is not given, or NULL


SELECT * 
FROM farmers_market.product
WHERE 
   
 product_size IS NULL 
   
 OR TRIM(product_size) = ''

---------------------------

FILTERING USING SUBQUERIES - find purchases that were made at the farmers market on days when it rained

Value in market_date_infor table called market_rain_flag that tells us if it rained or not using 0s and 1s. But the customer purchase data is stored in a different table > customer_purchases 

SHOW market date info table: 

SELECT market_date, market_rain_flag
FROM farmers_market.market_date_info
WHERE market_rain_flag = 1

SUBQUERY WILL FIRST BE EVALUATED, RETURN A BUNCH OF DATES AND THE OUTER QUERY JUST FINDS THOSE DATES IN THE PURCHASES TABLE

SELECT 
   
 market_date, 
   
 customer_id, 
   
 vendor_id, 
   
 quantity * cost_to_customer_per_qty price
FROM farmers_market.customer_purchases
WHERE 
   
 market_date IN
      
 (
      
 SELECT market_date
      
 FROM farmers_market.market_date_info
      
 WHERE market_rain_flag = 1
      
 )
LIMIT 5


