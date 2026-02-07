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
