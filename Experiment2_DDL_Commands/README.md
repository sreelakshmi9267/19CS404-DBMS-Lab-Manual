# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.

For example:
### Test	
INSERT INTO jobs (job_id, job_title, min_salary, max_salary) VALUES (1, 'Software Engineer', 9000, 15000);
SELECT * FROM jobs;
### Result
job_id      job_title          min_salary  max_salary
----------  -----------------  ----------  ----------
1           Software Engineer  9000        15000


```
CREATE TABLE jobs(
job_id INTEGER,
job_title VARCHAR(50) DEFAULT "",
min_salary INTEGER DEFAULT 8000,
max_salary INTEGER DEFAULT NULL
);
```

**Output:**
<img width="1240" height="421" alt="image" src="https://github.com/user-attachments/assets/540a20df-831f-40ef-902f-ae1bf7ecccce" />


**Question 2**
---
Insert the following customers into the Customers table:

CustomerID  Name         Address     City        ZipCode
----------  -----------  ----------  ----------  ----------
302         Laura Croft  456 Elm St  Seattle     98101
303         Bruce Wayne  789 Oak St  Gotham      10001
For example:

Test	Result
SELECT * FROM Customers;

CustomerID  Name         Address     City        ZipCode
----------  -----------  ----------  ----------  ----------
302         Laura Croft  456 Elm St  Seattle     98101
303         Bruce Wayne  789 Oak St  Gotham      10001

```sql
INSERT INTO Customers VALUES (302,'Laura Croft','456 Elm St','Seattle',98101);
INSERT INTO Customers VALUES (303,'Bruce Wayne','789 Oak St','Gotham',10001);
```

**Output:**

<img width="1233" height="473" alt="image" src="https://github.com/user-attachments/assets/36737e4f-5bad-4a2d-a411-77413e723005" />


**Question 3**
---
Write a SQL Query  to Rename attribute "name" to "first_name"  and add mobilenumber as number ,DOB as Date,State as varchar(30) in the table Companies. 

For example:

Test	Result
pragma table_info('Companies');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          int         0                       0
1           first_name  varchar(50  0                       0
2           address     text        0                       0
3           email       varchar(50  0                       0
4           phone       varchar(10  0                       0
5           mobilenumb  number      0                       0
6           DOB         Date        0                       0
7           State       varchar(30  0                       0

```sql
ALTER TABLE Companies RENAME COLUMN name TO first_name;
ALTER TABLE Companies ADD mobilenumber number; 
ALTER TABLE Companies ADD DOB Date;
ALTER TABLE Companies ADD State varchar(30);
```

**Output:**

<img width="1237" height="506" alt="image" src="https://github.com/user-attachments/assets/a8fffced-12d8-4947-949a-2c446b3c7682" />


**Question 4**
---
Create a table named Products with the following columns:

ProductID as INTEGER
ProductName as TEXT
Price as REAL
Stock as INTEGER
For example:

Test	Result
pragma table_info('Products');
cid   name        type        notnull     dflt_value  pk
----  ----------  ----------  ----------  ----------  ----------
0     ProductID   INTEGER     0                       0
1     ProductNam  TEXT        0                       0
2     Price       REAL        0                       0
3     Stock       INTEGER     0                       0
```sql
create table Products(
ProductID INTEGER,
ProductName TEXT,
Price REAL,
Stock INTEGER
);
```

**Output:**
<img width="1233" height="405" alt="image" src="https://github.com/user-attachments/assets/da5afeae-9901-4727-99ef-3ca111dde87d" />


**Question 5**
---
Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.
For example:

Test	Result
INSERT INTO Invoices (InvoiceID, InvoiceDate)
VALUES (1, '2024-08-08'),(1,'2024-09-08');
Error: UNIQUE constraint failed: Invoices.InvoiceID


```sql
create table Invoices(
InvoiceID INTEGER primary key,
InvoiceDate DATE,
DueDate DATE check(DueDate>InvoiceDate),
Amount REAL check(Amount>0)
);
```

**Output:**

<img width="1234" height="371" alt="image" src="https://github.com/user-attachments/assets/6a5abd62-a793-48c9-bdb2-2ec8368c7ecc" />


**Question 6**
---
Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).
For example:

Test	Result
INSERT INTO Customers (CustomerID, FirstName, LastName, Email) VALUES (1, 'Alice', 'Johnson', 'alice.johnson@example.com');
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
select * from orders;
OrderID     OrderDate   CustomerID
----------  ----------  ----------
1           2024-08-01  1

```sql
create table Orders(
OrderID INTEGER primary key,
OrderDate DATE not NULL,
CustomerID INTEGER references Customers(CustomerID) 
);
```

**Output:**
<img width="1235" height="372" alt="image" src="https://github.com/user-attachments/assets/9d023b77-e5fd-4e84-a748-b9f1f567129e" />


**Question 7**
---
Create a table named Products with the following constraints:
ProductID as INTEGER should be the primary key.
ProductName as TEXT should be unique and not NULL.
Price as REAL should be greater than 0.
StockQuantity as INTEGER should be non-negative.
For example:

Test	Result
INSERT INTO Products (ProductID, ProductName, Price, StockQuantity) VALUES (1, 'Laptop', 999.99, 10);
select * from Products;
ProductID   ProductName  Price       StockQuantity
----------  -----------  ----------  -------------
1           Laptop       999.99      10


```sql
create table Products(
ProductID INTEGER primary key,
ProductName TEXT unique not NULL,
Price REAL check(Price>0),
StockQuantity INTEGER check(StockQuantity>0)
);
```

**Output:**
<img width="1233" height="371" alt="image" src="https://github.com/user-attachments/assets/1d33c3fa-724a-451b-8cc7-c93165ee8956" />


**Question 8**
---
Insert a customer with CustomerID 301, Name Michael Jordan, Address 123 Maple St, City Chicago, and ZipCode 60616 into the Customers table.

For example:

Test	Result
SELECT * FROM Customers WHERE CustomerID = 301;
CustomerID  Name            Address       City        ZipCode
----------  --------------  ------------  ----------  ----------
301         Michael Jordan  123 Maple St  Chicago     60616


```sql
insert into Customers values (301,'Michael Jordan','123 Maple St','Chicago',60616);
```

**Output:**
<img width="1238" height="329" alt="image" src="https://github.com/user-attachments/assets/4c802cbc-5cd1-44e8-ae3d-3525e1ce7d51" />

**Question 9**
---
In the Products table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ProductID   Name              Category    Price       Stock
----------  ---------------   ----------  ----------  ----------
106         Fitness Tracker   Wearables
107         Laptop            Electronics  999.99      50
108         Wireless Earbuds  Accessories              100
 

For example:

Test	Result
SELECT * FROM Products;
ProductID   Name             Category    Price       Stock
----------  ---------------  ----------  ----------  ----------
106         Fitness Tracker  Wearables
107         Laptop           Electronic  999.99      50
108         Wireless Earbud  Accessorie              100


```sql
insert into Products values(106,'Fitness Tracker','Wearables',null,null);
insert into Products values(107,'Laptop','Electronic',999.99,50);
insert into Products values(108,'Wireless Earbud','Accessorie',null,100);
```

**Output:**
<img width="1236" height="379" alt="image" src="https://github.com/user-attachments/assets/3558ac15-c487-409e-9d80-d1dcf2eb1643" />

**Question 10**
---
Write an SQL query to add two new columns, designation and net_salary, to the table Companies. The designation column should have a data type of varchar(50), and the net_salary column should have a data type of number.

 

 

For example:

Test	Result
pragma table_info('Companies');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          int         0                       0
1           name        varchar(50  0                       0
2           address     text        0                       0
3           email       varchar(50  0                       0
4           phone       varchar(10  0                       0
5           designatio  varchar(50  0                       0
6           net_salary  number      0                       0


```sql
alter table Companies add designatio varchar(50);
alter table Companies add net_salary number;
```

**Output:**

<img width="1236" height="477" alt="image" src="https://github.com/user-attachments/assets/9c7c858f-dcdf-4d5a-a8c1-f4972f59dc62" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
