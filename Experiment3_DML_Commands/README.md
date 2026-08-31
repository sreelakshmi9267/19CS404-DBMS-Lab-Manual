# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
Write a SQL statement to Increase the salary by 500 and email as 'updated' for employees with job ID 'SA_REP' and commission percentage greater than 0.15


Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id 
For example:

Test	Result
SELECT EMPLOYEE_ID, FIRST_NAME, EMAIL, SALARY, JOB_ID FROM EMPLOYEES 
WHERE job_id = 'SA_REP' AND EMAIL='updated' LIMIT 5;
EMPLOYEE_ID  FIRST_NAME  EMAIL       SALARY      JOB_ID
-----------  ----------  ----------  ----------  ----------
150          Peter       updated     10500       SA_REP
151          David       updated     10000       SA_REP
152          Peter       updated     9500        SA_REP
153          Christophe  updated     8500        SA_REP
154          Nanette     updated     8000        SA_REP


```sql
update employees
set salary=salary+500,
email='updated'
where job_id='SA_REP'and
commission_pct>0.15;
```

**Output:**

<img width="1235" height="614" alt="image" src="https://github.com/user-attachments/assets/d8cc0227-09d7-4006-98c5-1573b80a50f7" />


**Question 2**
---
Write a SQL query to delete a doctor from Doctors table whos specialization is 'Cardiology'

Sample table: Doctors

attributes: doctor_id, first_name, last_name, specialization


```sql
delete from doctors 
where specialization='Cardiology';
```

**Output:**
<img width="1236" height="475" alt="image" src="https://github.com/user-attachments/assets/cd38903e-369e-41c5-b53a-56f7e5331980" />


**Question 3**
---
Write a SQL statement to display name and commission of first 5 salesmen.

table info

salesman(name,commission) 

For example:

Result
name        commission
----------  ----------
James Hoog  0.15
Nail Knite  0.13
Lauson Hen  0.12


```sql
select name, commission
from salesman
limit 5;
```

**Output:**

<img width="1245" height="549" alt="image" src="https://github.com/user-attachments/assets/3e4394fc-857c-44a5-8e3a-3f6ad4109b19" />


**Question 4**
---
Write a SQL query to Delete a Specific Surgery whose ID is 3 or surgeon ID is 4.

Sample table: Surgeries
<img width="665" height="148" alt="image (1)" src="https://github.com/user-attachments/assets/7b5ae165-3ba3-46a9-8e9b-c729aaef6324" />


For example:

Test	Result
--After Deletion
SELECT * FROM surgeries;
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28
3           3           3           2024-03-25
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28

```sql
delete from surgeries
where surgery_id=3 or surgeon_id=4;
```

**Output:**
<img width="1296" height="811" alt="image" src="https://github.com/user-attachments/assets/fd42962f-3f74-446e-adf5-c6796842af3c" />

**Question 5**
---
Write a SQL query to label rows in the Calculations table as 'Even' if value1 is even, otherwise 'Odd'.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0
 

For example:

Result
id          value1      parity
----------  ----------  ----------
1           -87.65      Odd
2           45.78       Odd
3           89.99       Odd
4           -0.005      Even


```sql
select id,value1,
case
when cast(value1 as integer)%2=0 then 'Even'
else 'Odd'
end as parity
from calculations;
```

**Output:**
<img width="1236" height="573" alt="image" src="https://github.com/user-attachments/assets/d80eb893-77e5-4d8d-ac11-d673ea0caeff" />


**Question 6**
---
Write a SQL query to select orders between 500 and 4000 (begin and end values are included). Exclude orders amount 948.50 and 1983.43. Return ord_no, purch_amt, ord_date, customer_id, and salesman_id.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
For example:

Result
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70003       2480.4      2012-10-10  3009         5003
70013       3045.6      2012-04-25  3002         5001


```sql
select ord_no,purch_amt,ord_date,customer_id,salesman_id 
from orders
where purch_amt between 500 and 4000 and 
purch_amt not in (948.50,1983.43);
```

**Output:**
<img width="1242" height="491" alt="image" src="https://github.com/user-attachments/assets/a0a219c7-e581-4ed2-bb9d-5fe2642ae09d" />


**Question 7**
---
Write a SQL statement to Update the address to '58 Lakeview, Magnolia' where supplier ID is 5 in the suppliers table.

Suppliers Table 

name               type
-----------------  ---------------
supplier_id        INT
supplier_name      VARCHAR(100)
contact_person     VARCHAR(100)
phone_number       VARCHAR(20)
email              VARCHAR(100)
address            VARCHAR(250)
For example:

Test	Result
select changes();
changes()
----------
1


```sql
update suppliers
set address='58 Lakeview, Magnolia'
where supplier_id=5;
```

**Output:**
<img width="1237" height="494" alt="image" src="https://github.com/user-attachments/assets/6be66112-9c87-4402-bebb-52b66efed467" />


**Question 8**
---
Write a SQL statement to Display names and city of salesman, who belongs to the city of London or Rome. Inventory.db
<img width="716" height="292" alt="inventory" src="https://github.com/user-attachments/assets/f0518ac5-950f-4a87-970a-e64a72eba40c" />


Inventory database

For example:

Result
name        city
----------  ----------
Pit Alex    London
Paul Adam   Rome


```sql
select name,city
from salesman
where city in ('London','Rome');
```

**Output:**
<img width="1241" height="452" alt="image" src="https://github.com/user-attachments/assets/f85a6359-5647-42db-bca9-6b1ce9af1747" />


**Question 9**
---
Write a SQL query to Delete customers with following conditions

'CUST_COUNTRY' is not in a list of specified countries ('UK', 'USA', 'Canada')
'GRADE' is greater than or equal to 3
Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |

```sql
delete from Customer
where CUST_COUNTRY not in ('UK', 'USA', 'Canada')
and GRADE >=3;
```

**Output:**
<img width="1244" height="515" alt="image" src="https://github.com/user-attachments/assets/3424a25c-d95e-475e-b327-48f86b3ff5b1" />


**Question 10**
---
Write a SQL query to Delete customers with 'GRADE' 3 or 'AGENT_CODE' 'A008' whose 'OUTSTANDING_AMT' is less than 5000

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
changes()
----------
1


```sql
delete from Customer 
where (GRADE=3 or AGENT_CODE='A008') and
OUTSTANDING_AMT<5000;
```

**Output:**

<img width="1238" height="490" alt="image" src="https://github.com/user-attachments/assets/7faf2441-4a95-4efe-a54f-c49cc951a836" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
