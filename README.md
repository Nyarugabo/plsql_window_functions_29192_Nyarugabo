# plsql_window_functions_29192_Nyarugabo
Q1. Problem Definition
 Business Context
----------------------
This the online market platform (Freshmark)
-----------------------
Data Challenges
------------------------
FreshMaket is digital platform that connecrs farmers directly and buyers, enabling them to list,sell and purchase agriculcural products easly. 
It's simplifies the market place, increase farmer's profits and gives customers to fresh,localy food.

Q2. Success Criteria 

Five measurable goals.

Goal 1: i want to know the % selling products in each category.

. Why measurable? Becuase i can calculate total seles per product and category.

. window function: RANK() (to rank products within each category)

![image alt](https://github.com/Nyarugabo/plsql_window_functions_29192_Nyarugabo/blob/9490c3bfdb1073798ca8646ccf53c0b6ba6372ff/images/images/RANK.png).

Goal 2: I want to see cumulative sales month by month.

. Why measurable? I can sum the total sales for any month 

. Window funtion: SUM() OVER()

![image alt](https://github.com/Nyarugabo/plsql_window_functions_29192_Nyarugabo/blob/ea8be273fa686d59e202be0317251478638c7748/images/images/SUM.png).

Goal 3: I want to see growth compared to last month.

. Why measurable? Compare this month's sales to last month's 

. Window function: LAG() or LEAD()

![image alt](https://github.com/Nyarugabo/plsql_window_functions_29192_Nyarugabo/blob/478c2518e264e535b91f075d03156562b848112b/images/images/LAG.png).

Goal 4: I want to categorize customers into 4 groups by how much they buy.

. Why measurable? Helps marketing by know who buys the most

. Window function: NTILE()

![image alt](https://github.com/Nyarugabo/plsql_window_functions_29192_Nyarugabo/blob/0309ee8dc2c5a8407480bbe57dfb9e3a5f62b003/images/images/NTILE.png)

Goal 5: I want know 3-month moving average sales to smooth trends.

. Why measurable? Shows trends over months without spikes 

. Window function: AVG() OVER()

![image alt](https://github.com/Nyarugabo/plsql_window_functions_29192_Nyarugabo/blob/0309ee8dc2c5a8407480bbe57dfb9e3a5f62b003/images/images/AVG.png)


Q3. Database Schema Design

![image alt](https://github.com/Nyarugabo/plsql_window_functions_29192_Nyarugabo/blob/820d411e26b3ffb3cd4064378936f1fd1a1593f7/images/images/DB%20schema.png).

Q4.  SQL JOINs Implementation

1. INNER JOIN: Rerieve transactions wiith valid custmoers and products

SELECT
order_id, 
full_name AS client_name,
product_name,
quantity,
total_price,
order_date
FROM orders
INNER JOIN clients ON client_id = client_id
INNER JOIN products ON product_id = product_id;

OUT PUT

![image alt](https://github.com/Nyarugabo/plsql_window_functions_29192_Nyarugabo/blob/c4e165fa606f128d2f4997b6c67183d9da7c4122/images/INNER%20JOIN.png).

Business Interpretation :

Shows real orders where both client and product exist. Managment can track active sales and revenue.

2. LEFT JOIN: Identify with no orders

SELECT
client_id,
full_name,
order_id
FROM clients 
LEFT JOIN orders ON client_id = client_id
WHERE order_id IS NULL;

OUT PUT

![image alt](https://github.com/Nyarugabo/plsql_window_functions_29192_Nyarugabo/blob/de057e4281eb09b6c5c5caca0a851bc0e396651f/images/LEFT%20JOIN.png).

Business Interpretation:

Identifies clients who registered but never purchased. Useful for targeting promotions or loyalty campaigns.

3. RIGHT JOIN: Detect products with no sales activity

SELECT
product_id,
product_name,
order_id,
FROM orders
RIGHT JOIN products ON product_id = product_id
WHERE order_id IS NULL;

OUT PUT 

![image alt](https://github.com/Nyarugabo/plsql_window_functions_29192_Nyarugabo/blob/10f5de0c623f579385b50c169071a12126c3beef/images/RIGHT%20JOIN.png).

Business Interpretation:

Finds products that were never sold. Useful for inventory management

4. FULL OUTER JOIN: Compare customers and products including unmatched rocords

SELECT 
client_id,
c.full_name As client_name,
product_id,
product_name,
order_id,
FROM clients
LEFT JOIN orders ON c.client_id = o.client_id
LEFT JOIN products ON O.product_id = p.product_id

UNION

SELECT
client-id,
c.full_name AS clients_Name,
product_id,
product_name,
order_id,
LEFT JOIN products ON p.product_id = o.product_id
LEFT JOIN orders ON o.client_id = c.client_id

out put

![image alt](https://github.com/Nyarugabo/plsql_window_functions_29192_Nyarugabo/blob/2ef4021d92a902947e91a36825ccb45b6448f4d2/images/FULL%20JOIN.png).

Business Interpretation:

Gives a full overview of clients products, highlighting both unmatched clients(no orders) and unmatched products(never sold).

5. SELF JOIN: Compare customers within the same location

SELECT
c1.client_id AS client1_id,
c1.full_name AS client1_name,
c2.client_id AS client2_id,
c2.full_name AS client2_id,
c1.location
FROM client
INNER JOIN clients c1.location = c2.location AND c1.client_id < c2.client_id;

OUT PUT

![image alt](https://github.com/Nyarugabo/plsql_window_functions_29192_Nyarugabo/blob/be6d830b04c5b8cc966238f60081b3ee979dbc0a/images/SELF%20JOIN.png).

Business Interpretation:

Finds pairs of clients located in the same city. Useful for targeting region specific marketing or logistics planning.
