1. Write a query that returns all customer purchases of product IDs 4 and 9. 

2. Write two queries, one using two conditions with an AND operator, and one using the BETWEEN operator, that will return all customer purchases made from vendors with vendor IDs between 8 and 10 (inclusive). 

3. Can you think of two different ways to change the final query we looked at so it would return purchases from days when it wasn't raining? See original query below:

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

4. Products can be sold by the individual unit or by bulk measures like lbs. or oz. Write a query that outputs the product_id and product_name columns from the product table, and add a column called prod_qty_type_condensed that displays the word “unit” if the product_qty_type is “unit,” and otherwise displays the word “bulk.” 

5. We want to flag all of the different types of pepper products that are sold at the market. Add a column to the previous query called pepper_flag that outputs a 1 if the product_name contains the word “pepper” (regardless of capitalization), and otherwise outputs 0. 

6. Can you think of a situation when a pepper product might not get flagged as a pepper product using the code from the previous exercise?

Teate, Renee M. P.. SQL for Data Scientists (p. 60). Wiley. Kindle Edition. 
