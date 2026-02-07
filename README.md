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

Goal 2: I want to see cumulative sales month by month.

. Why measurable? I can sum the total sales for any month 

. Window funtion: SUM() OVER()

Goal 3: I want to see growth compared to last month.

. Why measurable? Compare this month's sales to last month's 

. Window function: LAG() or LEAD()

Goal 4: I want to categorize customers into 4 groups by how much they buy.

. Why measurable? Helps marketing by know who buys the most

. Window function: NTILE()

Goal 5: I want know 3-month moving average sales to smooth trends.

. Why measurable? Shows trends over months without spikes 

. Window function: AVG() OVER()


Q3. Database Schema Design

Table1 farmers

. famer_id

. full_name

. phone

. location

.date 

Table2 clients(customer)

. client_id

. full_name

. phone

. location

. date 

Table3 products 

. category

. product_name

. price 

.quantity

.unit

.date




