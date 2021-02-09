CREATE TABLE #sales
(Sales_id INT, [date] datetime, customer_id INT, product_id INT , purchase_amount DECIMAL(10,8) )

DROP TABLE IF EXISTS #product
CREATE TABLE #product 
(p_id INT , P_Name NVARCHAR(20), Brand_id INT , B_name NVARCHAR(20))

INSERT INTO #product (p_id, P_Name, Brand_id,B_name) VALUES(   1, N'cap', 1, N'nike')
INSERT INTO #product (p_id, P_Name, Brand_id,B_name) VALUES(   2, N'cap', 2, N'adidas')
INSERT INTO #product (p_id, P_Name, Brand_id,B_name) VALUES(   3, N'cap', 3, N'puma')
INSERT INTO #product (p_id, P_Name, Brand_id,B_name) VALUES(   4, N'shoes', 1, N'nike')
INSERT INTO #product (p_id, P_Name, Brand_id,B_name) VALUES(   5, N'shoes', 2, N'adidas')
INSERT INTO #product (p_id, P_Name, Brand_id,B_name) VALUES(   6, N'shoes', 3, N'puma')
INSERT INTO #product (p_id, P_Name, Brand_id,B_name) VALUES(   7, N'socks', 1, N'nike')
INSERT INTO #product (p_id, P_Name, Brand_id,B_name) VALUES(   8, N'socks', 3, N'puma')

INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 1,'2018-10-12 19:46:47.833' , 1,1, 10 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 2,'2018-11-12 19:46:47.833' , 1,2, 20 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 3,'2017-9-12 19:46:47.833' , 3,1, 10 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 4,'2017-7-12 19:46:47.833' , 5,3, 30 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 5,'2019-1-12 19:46:47.833' , 6,1, 10 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 6,'2019-1-12 19:46:47.833' , 5,4, 70 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 7,'2019-11-12 19:46:47.833' , 1,1, 10 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 8,'2020-5-12 19:46:47.833' , 5,4, 70 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 9,'2020-3-12 19:46:47.833' , 6,2, 10 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 10,'2020-2-12 19:46:47.833' , 1,1, 10 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 11,'2019-7-15 19:46:47.833' , 1,1, 10 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 12,'2019-6-14 19:46:47.833' , 2,8, 30 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 13,'2019-5-12 19:46:47.833' , 1,6, 90 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 14,'2019-5-12 19:46:47.833' , 3,4, 70 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 15,'2019-5-12 19:46:47.833' , 4,5, 80 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 16,'2019-5-12 19:46:47.833' , 1,5, 80 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 17,'2019-5-12 19:46:47.833' , 4,5, 80 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 18,'2019-5-12 19:46:47.833' , 6,5, 80 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 19,'2019-5-12 19:46:47.833' , 1,4, 70 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 20,'2019-5-12 19:46:47.833' , 4,4, 70 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 21,'2019-5-12 19:46:47.833' , 6,4, 70 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 22,'2019-5-12 19:46:47.833' , 1,7, 25 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 23,'2019-5-12 19:46:47.833' , 4,7, 25 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 24,'2019-5-12 19:46:47.833' , 6,7, 25 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 25,'2020-5-12 19:46:47.833' , 5,4, 70 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 26,'2020-3-12 19:46:47.833' , 6,7, 25 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 127,'2020-2-12 19:46:47.833' , 1,7, 25 )
INSERT INTO #sales (Sales_id, date,customer_id, product_id,purchase_amount) VALUES ( 27,'2020-2-12 19:46:47.833' , 1,7, 25 )

-- Top 2 product in year 2019 -- Answer should be shoes and socks

SELECT TOP 2 p.p_name FROM (
SELECT distinct p.P_Name, COUNT(p.p_id) OVER(PARTITION BY p_name,DATEPART(YEAR,[date]) )AS rn FROM #product p
JOIN #sales s ON s.product_id = p.p_id
WHERE  DATEPART(YEAR,[date]) = 2019
--GROUP BY p.P_Name, DATEPART(YEAR,[date])
)p
ORDER BY rn DESC

-- top 2 product per year
SELECT t.product_name,
       t.purchase_year
FROM
(
    SELECT p.product_name,
           p.purchase_year,
           rn,
           DENSE_RANK() OVER (PARTITION BY p.purchase_year ORDER BY rn DESC) AS rank1
    FROM
    (
        SELECT DISTINCT
               p.P_Name AS product_name,
               YEAR([s].[date]) AS purchase_year,
               COUNT(p.p_id) OVER (PARTITION BY P_Name, YEAR(s.[date])) AS rn
        FROM #sales s
            JOIN #product p
                ON p.p_id = s.product_id
				--ORDER BY  YEAR(s.[date])
    ) p
) t
WHERE t.rank1 <= 2;
--ORDER BY rn DESC, p.purchase_year

--second method

SELECT A.product_name, A.purchase_year FROM (
	SELECT DISTINCT
               p.P_Name AS product_name,
               YEAR([s].[date]) AS purchase_year,
			   RANK() OVER(PARTITION BY YEAR([s].[date]) ORDER BY COUNT(p.p_id) desc) AS product_Count
        FROM #sales s
            JOIN #product p
                ON p.p_id = s.product_id
				GROUP BY  p.P_Name ,YEAR([s].[date]))A 
		WHERE A.product_Count <=2
			

-- question 3 List of Customer who bought both brand nike and adidas and atleat 2 products in each brand
SELECT DISTINCT a.customer_id FROM (
SELECT DISTINCT	p.B_name,s.customer_id,
	   COUNT(p.p_id) OVER(PARTITION BY p.B_name, s.customer_id) AS product_count_per_Customer,
	   DENSE_RANK() OVER (PARTITION BY s.customer_id ORDER BY p.B_name) AS brand_per_customer
FROM #product p
    JOIN #sales s
        ON p.p_id = s.product_id
		WHERE p.B_name IN ('nike','adidas')
		--ORDER BY s.customer_id
		)a
		WHERE a.product_count_per_Customer >=2
		AND a.brand_per_customer = 2
	

-- List of customers whoes total purchase incresed from 2018 but decresed from 2020
;WITH customer_countEarlier as(
SELECT DISTINCT  s.customer_id,
	   COUNT(p.p_id)AS product_count_per_Customer
FROM #product p
    join #sales s
        ON p.p_id = s.product_id
		WHERE YEAR([s].[date]) IN (2018,2017)
		GROUP BY s.customer_id)
, customer_countLater AS (
SELECT DISTINCT s.customer_id,
	   COUNT(p.p_id) AS product_count_per_Customer
FROM #product p
    join #sales s
        ON p.p_id = s.product_id
		WHERE YEAR([s].[date]) IN ( 2020)
		GROUP BY s.customer_id
)
SELECT * FROM customer_countEarlier ce
JOIN customer_countLater cl ON cl.customer_id = ce.customer_id
WHERE  ce.product_count_per_Customer < cl.product_count_per_Customer

-- how many unit were sold in 2019

SELECT p.P_Name, COUNT(p.p_id)
FROM #product p
    join #sales s
        ON p.p_id = s.product_id
		WHERE YEAR([s].[date]) IN ( 2019)
	GROUP BY p.P_Name

--- items which were ordered in 2019 but not ordered in 2017
SELECT DISTINCT p.P_Name
FROM #product p
    join #sales s
        ON p.p_id = s.product_id
		WHERE YEAR([s].[date]) IN ( 2019)
	AND NOT EXISTS (SELECT 1
FROM #product p1
    join #sales s1
        ON p1.p_id = s1.product_id 
         AND p1.P_Name = p.P_Name
		WHERE YEAR([s1].[date]) IN ( 2017))


-- second method

SELECT DISTINCT p.P_Name
FROM #product p
    join #sales s
        ON p.p_id = s.product_id
		WHERE YEAR([s].[date]) IN ( 2019)
	AND p.P_Name NOT IN  (SELECT p1.P_Name
FROM #product p1
    join #sales s1
        ON p1.p_id = s1.product_id 
		WHERE YEAR([s1].[date]) IN ( 2017))

-- how many units were sold in each category that cost less than $20, between $20 and $50 and more than $50? Output category|units_0_20| units_20_50| units_50_plus
SELECT p.P_Name, 
SUM(CASE WHEN s.purchase_amount <20 THEN 1 ELSE 0 END) 'units_0_20',
SUM(CASE WHEN s.purchase_amount >=20 AND s.purchase_amount <50 THEN 1 ELSE 0 END) 'units_20_50',
SUM(CASE WHEN s.purchase_amount >= 50 THEN 1 ELSE 0 END) 'units_50_plus'
FROM #product p
    join #sales s
        ON p.p_id = s.product_id
		GROUP BY p.P_Name

-- find the number of unique day each employee worked

CREATE TABLE #employee (emp_id INT , task_id INT, start_day NVARCHAR(10), end_day NVARCHAR(10))

INSERT INTO #employee (  emp_id,  task_id,  start_day,  end_day)VALUES(   1,   1,   N'Monday',  N'Wednesday'  )
INSERT INTO #employee (  emp_id,  task_id,  start_day,  end_day)VALUES(   1,   2,   N'Monday',  N'Tuesday'  )
INSERT INTO #employee (  emp_id,  task_id,  start_day,  end_day)VALUES(   1,   3,   N'Friday',  N'Friday'  )
INSERT INTO #employee (  emp_id,  task_id,  start_day,  end_day)VALUES(   2,   1,   N'Monday',  N'Friday'  )
INSERT INTO #employee (  emp_id,  task_id,  start_day,  end_day)VALUES(   2,   1,   N'Tuesday',  N'Wednesday'  )

-- hint Calendar day table or date dimension table
DROP TABLE IF EXISTS #calendar 
CREATE TABLE #calendar (Calendar_day NVARCHAR(12), calendar_day_of_week NVARCHAR(10), calendar_yer INT , calendar_month INT )

INSERT INTO #calendar (Calendar_day, calendar_day_of_week, calendar_yer,calendar_month)VALUES( N'1900/01/01', N'Wednesday', 1900,  3 )
INSERT INTO #calendar (Calendar_day, calendar_day_of_week, calendar_yer,calendar_month)VALUES( N'1900/01/01', N'Thrusday', 1900,  4 )
INSERT INTO #calendar (Calendar_day, calendar_day_of_week, calendar_yer,calendar_month)VALUES( N'1900/01/01', N'Friday', 1900,  5 )
INSERT INTO #calendar (Calendar_day, calendar_day_of_week, calendar_yer,calendar_month)VALUES( N'1900/01/01', N'Monday', 1900,  1 )
INSERT INTO #calendar (Calendar_day, calendar_day_of_week, calendar_yer,calendar_month)VALUES( N'1900/01/01', N'Tuesday', 1900,  2 )

--;WITH range AS  (
--SELECT e.*, c.calendar_month
--FROM #employee e
--JOIN #calendar c ON c.calendar_day_of_week= e.start_day
--union
--SELECT e.*, c1.calendar_month 
--FROM #employee e
--JOIN #calendar c1 ON c1.calendar_day_of_week= e.end_day) 
--,range2 AS (SELECT DISTINCT r1.emp_id,r1.task_id, r1.start_day, r1.end_day, r1.calendar_month FROM range r1
--JOIN range r2 ON r2.emp_id <> r1.emp_id AND r2.calendar_month = r1.calendar_month 
--AND r2.task_id = r1.task_id)
--SELECT DISTINCT r.emp_id,r.task_id, r.start_day,r.end_day FROM range r
--LEFT JOIN range2 r2 ON r2.emp_id = r.emp_id AND r2.task_id = r.task_id AND r2.calendar_month = r.calendar_month
--WHERE r2.emp_id IS NULL

--SELECT *  
--FROM #employee e

--SELECT * FROM #calendar

---- second approach

--SELECT e.*, c.calendar_month, c1.calendar_month FROM #employee e
-- JOIN #calendar c ON c.calendar_day_of_week= e.start_day
--  JOIN #calendar c1 ON c1.calendar_day_of_week= e.end_day

--;WITH work_range AS (
--  SELECT task_id,c.calendar_month AS Startday, c1.calendar_month AS endDay,
--  CASE WHEN e.start_day = 'Monday' OR e.end_day ='Monday' THEN e.emp_id ELSE 0 END AS 'Monday' ,
--  CASE WHEN e.start_day = 'Tuesday' OR e.end_day ='Tuesday' THEN e.emp_id ELSE 0 END AS 'Tuesday',
--  CASE WHEN e.start_day = 'Wednesday' OR e.end_day ='Wednesday' THEN e.emp_id ELSE 0 END AS 'Wednesday',
--  CASE WHEN e.start_day = 'Thrusday' OR e.end_day ='Thrusday' THEN e.emp_id ELSE 0 END AS 'Thrusday',
--  CASE WHEN e.start_day = 'Friday' OR e.end_day ='Friday' THEN e.emp_id ELSE 0 END AS 'Friday' 
--  FROM #employee e
--  JOIN #calendar c ON c.calendar_day_of_week= e.start_day
--  JOIN #calendar c1 ON c1.calendar_day_of_week= e.end_day)
--  SELECT * FROM work_range wr


 ; with days_num as (
  SELECT *
  FROM (
    VALUES ('monday', 1), ('tuesday', 2), ('wednesday', 3), ('thursday', 4), ('friday', 5)
  ) AS d (day, day_no)
),
emp_day_nums as (
  select emp_id, d1.day_no AS start_day_no, d2.day_no AS end_day_no
  from #employee t
  join days_num d1 on d1.day = t.start_day
  join days_num d2 on d2.day = t.end_day
)
select emp_id,COUNT(distinct d.day_no) AS distinct_days
from emp_day_nums e
join days_num d on d.day_no between e.start_day_no and e.end_day_no
group by emp_id


--second way
; with days_num as (
  SELECT *
  FROM (
    VALUES ('monday', 1), ('tuesday', 2), ('wednesday', 3), ('thursday', 4), ('friday', 5)
  ) AS d (day, day_no)
)
SELECT 
   t.emp_id,
   SUM(CASE 
      WHEN d1.day_no = d2.day_no THEN 1
      ELSE d2.day_no - d1.day_no
   END) AS no_of_days
FROM #employee t
JOIN days_num d1 
   ON t.start_day = d1.day
JOIN days_num d2
   ON t.end_day = d2.day
GROUP BY t.emp_id


  -- how many orders customer placed each month
  DROP TABLE IF EXISTS #Customer
  
  CREATE TABLE #Customer (CustomerDate DATETIME, customer_id INT , order_id INT, unit INT , country NVARCHAR(3) )
  INSERT INTO #Customer  ( CustomerDate, customer_id, order_id, unit, country)VALUES ( '2019/07/01', 1,  112, 5, N'US' )
  INSERT INTO #Customer  ( CustomerDate, customer_id, order_id, unit, country)VALUES ( '2019/07/02', 1,  211, 4, N'US' )
  INSERT INTO #Customer  ( CustomerDate, customer_id, order_id, unit, country)VALUES ( '2019/08/02', 2,  511, 4, N'EU' )
  INSERT INTO #Customer  ( CustomerDate, customer_id, order_id, unit, country)VALUES ( '2019/09/01', 3,  322, 1, N'JP' ) 
  INSERT INTO #Customer  ( CustomerDate, customer_id, order_id, unit, country)VALUES ( '2019/09/01', 3,  322, 2, N'JP' )
  INSERT INTO #Customer  ( CustomerDate, customer_id, order_id, unit, country)VALUES ( '2019/08/05', 1,  378, 6, N'US' )
  INSERT INTO #Customer  ( CustomerDate, customer_id, order_id, unit, country)VALUES ( '2019/09/10', 1,  456, 7, N'US' )


  SELECT DATEPART(MONTH, CustomerDate) Monthvalue, COUNT(DISTINCT customer_id) FROM #Customer
  group BY DATEPART(MONTH, CustomerDate)

  -- find average quantity of books sold for every order_id every year
  DROP TABLE IF EXISTS #orders
  CREATE TABLE #orders(Order_year INT, order_month INT , order_id INT, seller_id INT , book NVARCHAR(10), quantity INT , price DECIMAL(10,2))

  INSERT INTO #orders  (   Order_year, order_month, order_id, seller_id, book, quantity, price )  VALUES  (   2008,  6, 1, 888, N'HP',  2,  2000  )
  INSERT INTO #orders  (   Order_year, order_month, order_id, seller_id, book, quantity, price )  VALUES  (   2008,  6, 1, 888, N'LoTR',  1,  1000  )
  INSERT INTO #orders  (   Order_year, order_month, order_id, seller_id, book, quantity, price )  VALUES  (   2009,  7, 2, 999, N'HP',  1,  1000  )

  SELECT Order_year,order_id , AVG(quantity) Avg_quantity
  FROM #orders
  GROUP BY Order_year, order_id

 -- find max orders of books sold every year

  SELECT order_id , max(quantity) max_quantity
  FROM #orders
  GROUP BY  order_id


  --what will be result of below query

  CREATE TABLE #runner (id INT , runner_name NVARCHAR(20))

  INSERT INTO #runner  (  id,  runner_name ) VALUES  (   1,  N'John Doe'  )
  INSERT INTO #runner  (  id,  runner_name ) VALUES  (   2,  N'Jane Doe'  )
  INSERT INTO #runner  (  id,  runner_name ) VALUES  (   3,  N'Alice Jones'  )
  INSERT INTO #runner  (  id,  runner_name ) VALUES  (   4,  N'Bobby Louis'  )
  INSERT INTO #runner  (  id,  runner_name ) VALUES  (   5,  N'Lisa Romero'  )
  INSERT INTO #runner  (  id,  runner_name ) VALUES  (   6,  N'Sara John'  )

  CREATE TABLE #races (id INT, race_event NVARCHAR(50), winner_id INT)

  INSERT INTO #races  (id, race_event, winner_id ) VALUES (   1, N'100 meter',  2  )
  INSERT INTO #races  (id, race_event, winner_id ) VALUES (   2, N'500 meter',  3  )
  INSERT INTO #races  (id, race_event, winner_id ) VALUES (   3, N'cross- country',  2  )
  INSERT INTO #races  (id, race_event, winner_id ) VALUES (   4, N'triathalon',  NULL  )


  SELECT * FROM #runner  WHERE id NOT IN (SELECT winner_id FROM #races  )-- no output because of null
    SELECT * FROM #runner r WHERE  NOT EXISTS (SELECT 1 FROM #races ra WHERE  ra.winner_id = r.id )-- no output because of null
  SELECT * FROM #runner WHERE id NOT IN (SELECT winner_id FROM #races WHERE winner_id IS NOT NULL)

  SELECT runner_name + ';' FROM #runner FOR XML PATH ('')

===================================
Youtube SQL interview question

Table 1 - Employees:
Id
Salary

Table 2 - projects
employee_id
project_id
start_dt
end_dt

Part 1 : Find the 5 lowest paid employee who have done at least 10 project:

Select id 
from employee 
where id in (
Select employee_id 
from projects
Group by employee_id
Having count(end_dt) >= 10) a 
Order by salary asc
Limit 5

Or

Select
 e.id
From
 Employee e
INNER JOIN project p ON e.id = p.employee_id
GROUP BY e.id
HAVING COUNT(p.end_dt) >= 10
ORDER BY e.salary ASC
LIMIT 5

Part 2 - What is the sum of the salaries of employee that have not finished a project

Select
sum(e.salary) AS Total_salary
From employee e
INNER JOIN project p ON e.id = p.employee_id
Where end_dt IS NULL

OR

With CTE as
(SELECT *, case when end_dt is null then 1 else 0 end as null_end_dt from projects)

Select
sum(e.salary) AS Total_salary
From employee e
INNER JOIN CTE c ON e.id = c.employee_id
Having count(project_id) = sum(null_end _dt)

OR

Select
sum(e.salary) AS Total_salary
From employee e
Where e.id not in (
Select employee_id
From projects
Where end_dt is not null) a -- Has done at least 1 project

Part 3 - Lets say that it time to give annual raise for few. How to determine who should get

Sol 
-- Marginal increase in performance
-- Project length
-- Project count

 

































