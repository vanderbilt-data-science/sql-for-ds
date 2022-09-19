Below, you can find the SQL commands we saw on day 1 of the workshop series. 

**Simplest Select Statement**

SELECT * FROM farmers_market.product

**LIMIT in SQL**

SELECT * 
FROM farmers_market.product
LIMIT 5

**TIP: Always make it a habit to individually list all column names in the case something changes in the backend:**

SELECT product_id, product_name
FROM farmers_market.product
LIMIT 5

**ORDER BY IMPLEMENTATION:**

SELECT product_id, product_name
FROM farmers_market.product
ORDER BY product_name
LIMIT 5

**ORDER BY DESC IMPLEMENTATION:**

SELECT product_id, product_name
FROM farmers_market.product
ORDER BY product_id DESC
LIMIT 5

**ORDER BY TWO COLUMNS:**

SELECT market_date, vendor_id, booth_number 
FROM farmers_market.vendor_booth_assignments
ORDER BY market_date, vendor_id
LIMIT 5

**IN-LINE CALCULATION IMPLEMENTATION**

SELECT 
    
 market_date, 
    
 customer_id, 
    
 vendor_id, 
    
 quantity, 
    
 cost_to_customer_per_qty,
    
 quantity * cost_to_customer_per_qty 
FROM farmers_market.customer_purchases
LIMIT 10

**IN-LINE CALCULATION WITH ALIAS**

SELECT 
    
 market_date, 
    
 customer_id, 
    
 vendor_id, 
    
 quantity * cost_to_customer_per_qty AS price 
FROM farmers_market.customer_purchases
LIMIT 10

**ROUNDING IMPLEMENTATION**

SELECT 
    
 market_date,

 customer_id, 
    
 vendor_id, 
    
 ROUND(quantity * cost_to_customer_per_qty, 2) AS price 
FROM farmers_market.customer_purchases
LIMIT 10

**CONCATENATION IMPLEMENTATION**

SELECT *
FROM farmers_market.customer
LIMIT 5

SELECT 
    
 customer_id,
    
 CONCAT(customer_first_name, " ", customer_last_name) AS customer_name
FROM farmers_market.customer
LIMIT 5

**CONCATENATION IMPLEMENTATION WITH ORDERING**

SELECT 
 
 customer_id,
 
 CONCAT(customer_first_name, " ", customer_last_name) AS customer_name
 
FROM farmers_market.customer
 
ORDER BY customer_last_name, customer_first_name
 
LIMIT 5


**NESTING FUNCTIONS IMPLEMENTATION**

SELECT 
    
 customer_id,

 UPPER(CONCAT(customer_last_name, ", ", customer_first_name)) AS customer_name
FROM farmers_market.customer
ORDER BY customer_last_name, customer_first_name
LIMIT 5



