# Homework 3: Essential SQL

-  	Due on Saturday, September 14 at 11:59pm
-  	Weight: 8% of total grade
-  	Upload one .sql file with your queries

# AGGREGATE
1. Write a query that determines how many times each vendor has rented a booth at the farmer’s market by counting the vendor booth assignments per `vendor_id`.
   Solution:
      SELECT vendor_id, COUNT(booth_number) AS 'Times Rented' 
      FROM vendor_booth_assignments
      GROUP BY vendor_id;

2. The Farmer’s Market Customer Appreciation Committee wants to give a bumper sticker to everyone who has ever spent more than $2000 at the market. Write a query that generates a list of customers for them to give stickers to, sorted by last name, then first name. 
**HINT**: This query requires you to join two tables, use an aggregate function, and use the HAVING keyword.
   Solution:
       SELECT cp.customer_id AS 'ID', c.customer_first_name AS 'First Name', c.customer_last_name AS 'Last Name', cp.quantity AS 'Qty', cost_to_customer_per_qty AS 'Cost Per Qty', 
       (quantity*cost_to_customer_per_qty) AS 'Cost'
       FROM customer_purchases AS cp
       INNER JOIN customer AS c
          ON cp.customer_id = c.customer_id
       GROUP BY c.customer_id
       HAVING SUM(cost) >= 2000
       ORDER BY c.customer_first_name , c.customer_last_name 

# Temp Table
1. Insert the original vendor table into a temp.new_vendor and then add a 10th vendor: Thomass Superfood Store, a Fresh Focused store, owned by Thomas Rosenthal
**HINT**: This is two total queries -- first create the table from the original, then insert the new 10th vendor. When inserting the new vendor, you need to appropriately align the columns to be inserted (there are five columns to be inserted, I've given you the details, but not the syntax)

To insert the new row use VALUES, specifying the value you want for each column:  
`VALUES(col1,col2,col3,col4,col5)`
    Solution:
       DROP TABLE IF EXISTS temp.new_vendor;

       CREATE TEMP TABLE temp.new_vendor AS
         SELECT * from vendor;
	
       INSERT INTO temp.new_vendor
          VALUES(10,'Thomass Superfood Store', 'Fresh Focused', 'Thomas', 'Rosenthal');

       SELECT * FROM temp.new_vendor;

# Date
1. Get the customer_id, month, and year (in separate columns) of every purchase in the customer_purchases table.
**HINT**: you might need to search for strfrtime modifers sqlite on the web to know what the modifers for month and year are!
    Solution:
        DROP TABLE IF EXISTS temp.customer_purchases;
        CREATE TEMP TABLE temp.customer_purchases AS
          SELECT customer_id, product_id, market_date, quantity, cost_to_customer_per_qty, 
            (cost_to_customer_per_qty*quantity) AS 'cost',
		    (STRFTIME('%m',market_date )) AS 'Month',
		    (STRFTIME('%Y',market_date )) AS 'Year' 
		 
        FROM customer_purchases;

        SELECT * FROM temp.customer_purchases;

2. Using the previous query as a base, determine how much money each customer spent in April 2022. Remember that money spent is `quantity*cost_to_customer_per_qty`.
**HINTS**: you will need to AGGREGATE, GROUP BY, and filter...but remember, STRFTIME returns a STRING for your WHERE statement!!
     Solution:
      DROP TABLE IF EXISTS temp.customer_purchases;
      CREATE TEMP TABLE temp.customer_purchases AS
      SELECT customer_id, product_id, market_date, quantity, cost_to_customer_per_qty, 
         (cost_to_customer_per_qty*quantity) AS 'cost',
		 (STRFTIME('%m',market_date )) AS 'Month',
		 (STRFTIME('%Y',market_date )) AS 'Year' 	 
      FROM customer_purchases;

      SELECT customer_id, Month, Year, SUM(cost) AS 'Total Purchases in 04-2022'
      FROM temp.customer_purchases 

      WHERE (Month = '04' AND Year = '2022' )
      GROUP BY customer_id;    
