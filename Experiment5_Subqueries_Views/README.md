# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
-- Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi and age below 30

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

 
 

For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
2           Khilan      25          Delhi       1500

```sql
-- select ID,NAME,AGE,ADDRESS,SALARY
FROM CUSTOMERS
WHERE ADDRESS='Delhi'and  AGE<30
ORDER by ID ASC;
```

**Output:**

<img width="1272" height="382" alt="image" src="https://github.com/user-attachments/assets/6f9df768-1381-4313-95ce-06807a1c68f3" />

**Question 2**
---
-- Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
For example:

Result
id     name             city             email            phone
-----  ---------------  ---------------  ---------------  ----------
6      Aarti Desai      Pune             aarti@gmail.com  890123456
7      Vivek Sharma     Chandigarh       vivek@gmail.com  980154021
8      Nisha Patel      Noida            nisha@gmail.com  901234567
9      Rajesh Singh     Hyderabad        rajesh@gmail.co  917654301


```sql
-- select *
from customer
where city <> (
select city
from customer
order by id DESC
limit 1
);
```

**Output:**
<img width="1301" height="497" alt="image" src="https://github.com/user-attachments/assets/ff375dcb-a667-4364-8685-0f6f9b91742c" />



**Question 3**
---
-- From the following tables, write a SQL query to find those salespeople who earned the maximum commission. Return ord_no, purch_amt, ord_date, and salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

orders table

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int
 

For example:

Result
ord_no      purch_amt   ord_date    salesman_id
----------  ----------  ----------  -----------
70002       65.26       2012-10-05  5001
70005       2400.6      2012-07-27  5001
70008       5760.0      2012-09-10  5001
70013       3045.6      2012-04-25  5001

```sql
--select ord_no,purch_amt,ord_date,salesman_id
from orders
where salesman_id IN (
select salesman_id
from salesman
where commission = (
select MAX(commission)
from salesman)
);
```

**Output:**

<img width="1032" height="493" alt="image" src="https://github.com/user-attachments/assets/2557a9c5-0d53-46af-99f4-28384a8df8e4" />


**Question 4**
---
-- From the following tables, write a SQL query to find all the orders generated in New York city. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

SALESMAN TABLE

name               type
-----------        ----------
salesman_id  numeric(5)
name             varchar(30)
city                 varchar(15)
commission   decimal(5,2)

ORDERS TABLE

name            type
----------      ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int

For example:

Result
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70002       65.26       2012-10-05  3002         5001
70005       2400.6      2012-07-27  3007         5001
70008       5760.0      2012-09-10  3002         5001
70013       3045.6      2012-04-25  3002       

```sql
-- select o.ord_no,purch_amt,o.ord_date,o.customer_id,o.salesman_id
from ORDERS o
join SALESMAN s ON o.salesman_id = s.salesman_id
where s.city='New York';
```

**Output:**

<img width="1222" height="512" alt="image" src="https://github.com/user-attachments/assets/4589fea4-4e91-41ec-bd63-d5117f53ccb1" />

**Question 5**
---
-- Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose AGE is LESS than $30

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

 
 

For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
2           Khilan      25          Delhi       1500
3           Kaushik     23          Kota        2000
4           Chaitali    25          Mumbai      6500
5           Hardik      27          Bhopal      8500
6           Komal       22          Hyderabad   4500
7           Muffy       24          Indore     

```sql
-- select ID,NAME,AGE,ADDRESS,SALARY
FROM CUSTOMERS
WHERE AGE<30;
```

**Output:**

<img width="1315" height="582" alt="image" src="https://github.com/user-attachments/assets/7aa55f95-6bba-472d-aa76-b4c24684c1b7" />


**Question 6**
---
--Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is EQUAL TO $1500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

 
 

For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
2           Khilan      25          Delhi       

```sql
--select *
from CUSTOMERS
where SALARY=1500;
```

**Output:**

<img width="1326" height="365" alt="image" src="https://github.com/user-attachments/assets/768dfdd1-5833-489c-9e4d-a45f00cc59f4" />


**Question 7**
---
--Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 1 million

Employee Table

name             type

------------   ---------------

id                    INTEGER

name              TEXT

age                 INTEGER

city                 TEXT

income           INTEGER

For example:

Result
id     name             age              city             income
-----  ---------------  ---------------  ---------------  ----------
101    Peter            32               NewYork          200000
102    Mark             32               California       300000
103    Donald           25               Arizona          1000000
105    Linklon          32               Georgia          250000


```sql
--select id, name, age, city,income
from Employee
where age < (
select avg(age)
from Employee
where income>1000000
);
```

**Output:**

<img width="1275" height="428" alt="image" src="https://github.com/user-attachments/assets/84da8ea2-e241-4a8d-984c-d2e3ce1482f5" />


**Question 8**
---
-- From the following tables, write a SQL query to determine the commission of the salespeople in Paris. Return commission.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

customer table

name         type
-----------  ----------
customer_id  int
cust_name    text
city         text
grade        int
salesman_id  int
For example:

Result
commission
----------
0.14


```sql
-- select commission
from salesman
where salesman_id IN (
select salesman_id
from customer
where city ='Paris'
);
```

**Output:**
<img width="408" height="303" alt="image" src="https://github.com/user-attachments/assets/229fe1d7-66df-4f6f-b426-ec52e7ac8332" />


**Question 9**
---
-- Write a SQL query to List departments with names longer than the average length

Departments Table (attributes: department_id, department_name)



For example:

Result
depar  department_name
-----  ---------------
5      Anesthesiologis


```sql
-- select department_id as depar,department_name
from Departments
where length(department_name)>(
       select AVG(length(department_name))
       From Departments
);
```

**Output:**

<img width="397" height="387" alt="image" src="https://github.com/user-attachments/assets/b79958ac-6c8d-4fbd-84e9-8e249f8f8c57" />

**Question 10**
---
-- From the following tables write a SQL query to find all orders generated by New York-based salespeople. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

orders table

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int
 

For example:

Result
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70002       65.26       2012-10-05  3002         5001
70005       2400.6      2012-07-27  3007         5001
70008       5760.0      2012-09-10  3002         5001
70013       3045.6      2012-04-25  3002    
```sql
-- 
```

**Output:**

<img width="1287" height="421" alt="image" src="https://github.com/user-attachments/assets/bc06642f-f639-4135-96fe-357998e9612f" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
