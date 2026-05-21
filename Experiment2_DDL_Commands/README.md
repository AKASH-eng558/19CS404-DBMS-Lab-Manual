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
Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.
--

```sql
create table Employees(
EmployeeID int PRIMARY KEY,
FirstName varchar(50) NOT NULL,
LastName varchar(50) NOT NULL,
Email varchar(50) UNIQUE,
Salary int CHECK (salary>0),
DepartmentID int,
FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)

)
```

**Output:**
<img width="1176" height="415" alt="image" src="https://github.com/user-attachments/assets/167ebdcd-4894-4cdf-986a-116b75500a36" />


**Question 2**
---
Create a table named Products with the following columns:

ProductID as INTEGER
ProductName as TEXT
Price as REAL
Stock as INTEGER
-- 

```sql
CREATE TABLE Products(
ProductID  INTEGER,
ProductName TEXT,
Price REAL,
Stock INTEGER

);
```

**Output:**
<img width="1218" height="330" alt="image" src="https://github.com/user-attachments/assets/52d0fd9a-4ca5-4556-be71-71a33f11f19d" />


**Question 3**
---
Write a SQL query to Rename the "city" column to "location" in the "customer" table.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
 
-- 

```sql
ALTER TABLE customer RENAME COLUMN city to location;
```

**Output:**
<img width="1203" height="337" alt="image" src="https://github.com/user-attachments/assets/a86631dd-bcec-4847-8d6c-492d655c3678" />


**Question 4**
---
Create a table named Reviews with the following columns:

ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT
---

```sql
CREATE TABLE Reviews (
    ReviewID INTEGER,
    ProductID INTEGER,
    Rating REAL,
    ReviewText TEXT
);
```

**Output:**
<img width="1215" height="432" alt="image" src="https://github.com/user-attachments/assets/40d3d8d0-0711-4196-849d-5eb490da0368" />


**Question 5**
---
In the Cusomers table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

CustomerID  Name          Address      City        ZipCode
----------  ------------  ----------   ----------  ----------
306         Diana Prince  Themyscira
307         Bruce Wayne   Wayne Manor  Gotham      10007
308         Peter Parker  Queens                   11375
-- 

```sql
INSERT INTO Customers(CustomerID, Name, Address, City, ZipCode) 
VALUES 
(306,'Diana Prince','Themyscira',null,null),
(307,'Bruce Wayne','Wayne Mano','Gotham','10007'),
(308,'Peter Parker','Queens',null,'11375');
```

**Output:**
<img width="1208" height="314" alt="image" src="https://github.com/user-attachments/assets/03fb05f2-9509-4c9e-b126-3a47b8953c11" />


**Question 6**
---
Write a SQL query to Add a new column mobilenumber as number in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
--

```sql
ALTER TABLE Student_details
ADD mobilenumber number;
```

**Output:**
<img width="1211" height="433" alt="image" src="https://github.com/user-attachments/assets/9dbef18e-2386-45e6-8327-cb43d93cb5ab" />


**Question 7**
---
Insert a product with ProductID 104, Name Tablet, and Category Electronics into the Products table, where Price and Stock should use default values.
-- 

```sql
insert into products(productID,Name,Category,Price,Stock)values(104,'Tablet','Electronics',100,50);
```

**Output:**
<img width="1196" height="231" alt="image" src="https://github.com/user-attachments/assets/b0e318b6-5fa3-45d2-8e5b-c15fa8bc53dd" />


**Question 8**
---
Create a table named Products with the following constraints:
ProductID as INTEGER should be the primary key.
ProductName as TEXT should be unique and not NULL.
Price as REAL should be greater than 0.
StockQuantity as INTEGER should be non-negative.
-- 

```sql
CREATE TABLE Products(
ProductID INTEGER PRIMARY KEY,
ProductName TEXT NOT NULL UNIQUE,
Price REAL CHECK(Price>0),
StockQuantity INTEGER CHECK(StockQuantity>=0)
);
```

**Output:**
<img width="1239" height="357" alt="image" src="https://github.com/user-attachments/assets/95d7e35d-56bb-4a99-9bc8-abeadbfc317e" />


**Question 9**
---
Insert the following products into the Products table:

Name        Category     Price       Stock
----------  -----------  ----------  ----------
Smartphone  Electronics  800         150
Headphones  Accessories  200         300
-- 

```sql
INSERT INTO Products( Name, Category, Price, Stock)
VALUES("Smartphone","Electronics","800 ","150");
INSERT INTO Products( Name, Category, Price, Stock)
VALUES("Headphones",  "Accessories",  "200",        "300");
```

**Output:**
<img width="1188" height="368" alt="image" src="https://github.com/user-attachments/assets/2cbf4897-c71c-40a8-8b42-fcdea0f9cf83" />


**Question 10**
---
Create a table named Locations with the following columns:

LocationID as INTEGER
LocationName as TEXT
Address as TEXT
-- 
```sql
CREATE TABLE Locations (
    LocationID INTEGER,
    LocationName TEXT,
    Address TEXT
);
```

**Output:**
<img width="1219" height="447" alt="image" src="https://github.com/user-attachments/assets/c1227311-7718-4bff-96ef-3bafb94fdaca" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
