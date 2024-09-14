# Homework 2: Basic SQL 

-  	Due on Friday, September 13 at 11:59pm
-  	Weight: 8% of total grade
-  	Upload one .sql file with your queries

# SELECT
1. Write a query that returns everything in the customer table.
   ![image](https://github.com/user-attachments/assets/96effd49-eb45-445d-aa02-fc7cb5c22249)
2. Write a query that displays all of the columns and 10 rows from the customer table, sorted by customer_last_name, then customer_first_ name.
   ![image](https://github.com/user-attachments/assets/bb79dc1b-f0ab-4f78-ac3d-7d1f1a46de68)


# WHERE
1. Write a query that returns all customer purchases of product IDs 4 and 9.
 ![image](https://github.com/user-attachments/assets/a175c0a3-5e45-48b5-9dd0-a46102310646)
2. Write a query that returns all customer purchases and a new calculated column 'price' (quantity * cost_to_customer_per_qty), filtered by vendor IDs between 8 and 10 (inclusive) using either:
	1.  two conditions using AND
	 ![image](https://github.com/user-attachments/assets/45b2a8b3-d904-4b9b-81c4-672fcb73c1e3)
 	2.  one condition using BETWEEN
         ![image](https://github.com/user-attachments/assets/0bd1aafc-4393-436e-bcce-012f5f0bb975)

# CASE
1. Products can be sold by the individual unit or by bulk measures like lbs. or oz. Using the product table, write a query that outputs the `product_id` and `product_name` columns and add a column called `prod_qty_type_condensed` that displays the word “unit” if the `product_qty_type` is “unit,” and otherwise displays the word “bulk.”
 ![image](https://github.com/user-attachments/assets/8c7bde0d-b970-4650-af85-a67ef902d47c)

2. We want to flag all of the different types of pepper products that are sold at the market. Add a column to the previous query called `pepper_flag` that outputs a 1 if the product_name contains the word “pepper” (regardless of capitalization), and otherwise outputs 0.
 ![image](https://github.com/user-attachments/assets/8731f858-856d-46a6-8288-afa31fe49289)
 ![image](https://github.com/user-attachments/assets/93f69480-c56c-4156-b509-028ba685415d)
# JOIN
1. Write a query that `INNER JOIN`s the `vendor` table to the `vendor_booth_assignments` table on the `vendor_id` field they both have in common, and sorts the result by `vendor_name`, then `market_date`.
 ![image](https://github.com/user-attachments/assets/a918fc52-92de-4cff-885d-4d5a114c109c)
