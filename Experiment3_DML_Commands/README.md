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
Write a SQL query to find employees who were hired after January 1, 2020.

emp table

cid         name        type        
----------  ----------  ---------- 
0           empno       INT         
1           ename       VARCHAR(100)
2           job         VARCHAR(50)
3           mgr         INT        
4           hiredate    DATE        
5           sal         DECIMAL(10,2)  
6           comm        DECIMAL(10,2)  
7           deptno      INT         
-- 

```sql
select * from emp where hiredate > '2020-01-01';
```

**Output:**
<img width="1196" height="347" alt="image" src="https://github.com/user-attachments/assets/ea094a34-f617-4d21-8580-422fa98e582e" />


**Question 2**
---
Write a SQL query to delete a specific doctor from Doctors table whose ID is 1.

Sample table: Doctors

attributes: doctor_id, first_name, last_name, specialization
-- 

```sql
DELETE FROM Doctors
WHERE doctor_id = 1;
```

**Output:**
<img width="1235" height="317" alt="image" src="https://github.com/user-attachments/assets/2b9935fb-264c-440e-b356-21e37de0832b" />


**Question 3**
---
Update the 'Selling_Price' to add 10% extra margin for all products supplied by the supplier with id 6.

PRODUCTS TABLE

name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT
--

```sql
UPDATE Products
SET sell_price = sell_price + (sell_price * 0.10)
WHERE supplier_id = 6;
```

**Output:**
<img width="1191" height="533" alt="image" src="https://github.com/user-attachments/assets/d29813fa-787c-4c2d-af6c-a92ae136ad63" />


**Question 4**
---
Write a query to list all products where the discount amount exceeds $50. The discount amount is calculated as original_price * discount_percentage. Return product_id, original_price, discount_percentage, and discount_amount.

Sample table: Products

product_id | original_price | discount_percentage

-----------------------------------------------------------

"101" "50" "0.1"

"102" "150" "0.15"

"103" "200" "0.2"

"104" "300" "0.25"

 

```sql
select product_id,original_price,discount_percentage,(original_price*discount_percentage) as discount_amount from Products where discount_amount>50;

```

**Output:**
<img width="1226" height="315" alt="image" src="https://github.com/user-attachments/assets/66ecf404-7055-4599-8f46-806e70985cf2" />


**Question 5**
---
Write a SQL query to classify base in the Calculations table as 'Provided' if it is not NULL, otherwise 'Not Provided'.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0
-- 

```sql
SELECT 
    id,
    base,
    CASE
        WHEN base IS NOT NULL THEN 'Provided'
        ELSE 'Not Provided'
    END AS base_status
FROM Calculations;
```

**Output:**
<img width="1208" height="548" alt="image" src="https://github.com/user-attachments/assets/743a58f6-2558-4e29-9147-b9ec76c988d7" />


**Question 6**
---
Write a SQL query to calculate the discounted price for products whose original price is between $50 and $150. Return product_id, original_price, discount_percentage, and discounted_price.

Sample table: Products

product_id | original_price | discount_percentage

 ------------+----------------+--------------------- 

101 | 50.00 | 0.10 

102 | 125.00 | 0.15

 103 | 200.00 | 0.20
-- 

```sql
select product_id,original_price,discount_percentage,original_price-(original_price*discount_percentage) as discounted_price from Products where original_price between 50 and 150;
```

**Output:**
<img width="1215" height="366" alt="image" src="https://github.com/user-attachments/assets/1ef91a71-60a3-4cb3-8938-9e9e90f5a912" />


**Question 7**
---
Update the reorder level to 40 pieces for all products belonging to the 'Grocery' category in the products table.

PRODUCTS TABLE

name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT
--

```sql
UPDATE Products
SET reorder_lvl = 40
WHERE category = 'Grocery';
```

**Output:**
<img width="1202" height="415" alt="image" src="https://github.com/user-attachments/assets/4f8d9890-5373-4a59-a1a0-ddd000a36cb9" />


**Question 8**
---
Change the supplier name to upper case where contact person contains ' Singh' in suppliers table.

name               type
-----------------  ---------------
supplier_id        INT
supplier_name      VARCHAR(100)
contact_person     VARCHAR(100)
phone_number       VARCHAR(20)
email              VARCHAR(100)
address            VARCHAR(250)
-- 

```sql
update suppliers set supplier_name=UPPER(supplier_name) where contact_person like '%Singh%';

```

**Output:**
<img width="1194" height="345" alt="image" src="https://github.com/user-attachments/assets/68b06d01-2237-4565-8fd8-5cc400a4beee" />


**Question 9**
---
Write a SQL statement to change salary of employee to 8000 whose Employee ID is 105, if the existing salary is less than 5000.


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
-- 

```sql
update Employees set salary=8000 where employee_id=105 and salary<5000;
```

**Output:**
<img width="1204" height="259" alt="image" src="https://github.com/user-attachments/assets/cf8d2576-e582-41ad-a8bc-e1df0829344a" />


**Question 10**
---
Write a SQL query to find the details of those salespeople who live in cities other than Paris and Rome. Return salesman_id, name, city, commission.

Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
-- 

```sql
SELECT salesman_id, name, city, commission
FROM salesman
WHERE city NOT IN ('Paris', 'Rome');
```

**Output:**
<img width="1213" height="396" alt="image" src="https://github.com/user-attachments/assets/42f4a8de-5943-49ed-b015-99ae82b35199" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
