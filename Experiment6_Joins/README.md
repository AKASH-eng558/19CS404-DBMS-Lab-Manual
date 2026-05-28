# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
<img width="1197" height="449" alt="image" src="https://github.com/user-attachments/assets/54268558-6fa9-4505-a030-fd1a45a0bfc4" />

--

```sql
SELECT 
    p.first_name AS patient_name
FROM patients p
INNER JOIN doctors d
ON p.doctor_id = d.doctor_id
WHERE d.first_name = 'Emily'
  AND d.last_name = 'Johnson'
  AND p.discharge_date IS NOT NULL;
```

**Output:**
<img width="742" height="388" alt="image" src="https://github.com/user-attachments/assets/380b6420-36b4-49f7-99d8-4e49d36fdbff" />


**Question 2**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the specialization from the "doctors" table (aliased as "Doctor_specialization"), with an inner join on the "doctor_id" column and a condition filtering for patients admitted between '2024-01-01' and '2024-01-31'.

PATIENTS TABLE:
name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

DOCTORS TABLE:

name             type
---------------  ---------------
doctor_id        INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
specialization   VARCHAR(100)

For example:
-- 

```sql
SELECT 
    p.first_name AS patient_name,
    d.specialization AS Doctor_specialization
FROM patients p
INNER JOIN doctors d
    ON p.doctor_id = d.doctor_id
WHERE p.admission_date BETWEEN '2024-01-01' AND '2024-01-31';
```

**Output:**
<img width="908" height="378" alt="image" src="https://github.com/user-attachments/assets/b3fb23b5-22b4-43fe-b79b-aa6c35f4d0fc" />


**Question 3**
---
<img width="1217" height="609" alt="image" src="https://github.com/user-attachments/assets/eaaa76e8-f305-4782-b5b9-c50e6dfa2402" />

-- 

```sql
SELECT 
    c.cust_name AS "Customer Name",
    c.city,
    s.name AS "Salesman",
    s.commission
FROM customer c
INNER JOIN salesman s
ON c.salesman_id = s.salesman_id;
```

**Output:**
<img width="1235" height="724" alt="image" src="https://github.com/user-attachments/assets/6c2b8899-fa28-4e34-af36-749ec7d9bb18" />


**Question 4**
---
<img width="1193" height="453" alt="image" src="https://github.com/user-attachments/assets/4cc51c77-bef5-4ff4-af90-4959e4a501c4" />

--

```sql
SELECT 
    s.name,
    c.cust_name,
    c.city,
    c.grade,
    c.salesman_id
FROM salesman s
LEFT JOIN customer c
ON s.salesman_id = c.salesman_id
WHERE c.grade <= 100;
```

**Output:**
<img width="1214" height="575" alt="image" src="https://github.com/user-attachments/assets/3898c277-26d0-46a4-b298-53b42e3e916c" />


**Question 5**
---
<img width="1158" height="766" alt="image" src="https://github.com/user-attachments/assets/6d20aaa9-469b-4293-a10e-be098ca40d5d" />

-- 

```sql
SELECT 
    o.ord_no,
    o.purch_amt,
    c.cust_name,
    c.city
FROM orders o
INNER JOIN customer c
ON o.customer_id = c.customer_id
WHERE o.purch_amt BETWEEN 500 AND 2000;
```

**Output:**
<img width="1182" height="478" alt="image" src="https://github.com/user-attachments/assets/46f064c0-7840-4b6e-8e4d-fad54fb37e60" />


**Question 6**
---
<img width="1182" height="410" alt="image" src="https://github.com/user-attachments/assets/49219ae1-ffd7-4c9e-a09c-4d226353c56a" />

-- 

```sql
SELECT 
    t.*
FROM test_results t
INNER JOIN patients p
    ON t.patient_id = p.patient_id
WHERE p.first_name = 'Alice';
```

**Output:**
<img width="1195" height="411" alt="image" src="https://github.com/user-attachments/assets/635fd910-6efa-4cd8-a6f0-2b43a97aee63" />


**Question 7**
---
<img width="1138" height="414" alt="image" src="https://github.com/user-attachments/assets/ea9bfb12-605e-45c0-bd18-c5f19e4aeec9" />

-- 

```sql
SELECT c.*
FROM customer c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
WHERE o.ord_date BETWEEN '2012-08-01' AND '2012-08-30';
```

**Output:**
<img width="1228" height="439" alt="image" src="https://github.com/user-attachments/assets/35e05b24-b88a-4450-9f62-1c61c83134cf" />


**Question 8**
---
QL statement to generate a report with customer name, city, order number, order date, order amount, salesperson name, and commission to determine if any of the existing customers have not placed orders or if they have placed orders through their salesman or by themselves.

Sample table: customer
-- 

```sql
SELECT 
    c.cust_name,
    c.city,
    o.ord_no,
    o.ord_date,
    o.purch_amt AS "Order Amount",
    s.name,
    s.commission
FROM customer c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
LEFT JOIN salesman s
ON c.salesman_id = s.salesman_id;
```

**Output:**
<img width="1134" height="590" alt="image" src="https://github.com/user-attachments/assets/7890a876-d2d7-4937-b7fe-2a69729e8ea2" />


**Question 9**
---
<img width="1226" height="385" alt="image" src="https://github.com/user-attachments/assets/b26ffd8f-7a50-47b8-84c1-d29bd5cdd0e8" />

-- 

```sql
SELECT 
    p.first_name AS patient_name,
    t.test_name
FROM patients p
INNER JOIN test_results t
ON p.patient_id = t.patient_id;
```

**Output:**
<img width="957" height="476" alt="image" src="https://github.com/user-attachments/assets/24a743a7-1e83-46b8-9639-4912a4132fc0" />


**Question 10**
---
Write the SQL query that achieves the selection of all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.
-- 

```sqlSELECT 
    t.*
FROM test_results t
INNER JOIN patients p
    ON t.patient_id = p.patient_id
WHERE p.first_name = 'Alice';
```

**Output:**
<img width="1255" height="454" alt="image" src="https://github.com/user-attachments/assets/92417dac-de06-482c-8d66-b6222c33a2f8" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
