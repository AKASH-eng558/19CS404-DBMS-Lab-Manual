# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
Write a SQL query to find the number of employees who are having the same age removing the duplicate values.

Sample table: employee

-- 

```sql
SELECT 
    COUNT(DISTINCT age) AS COUNT
FROM employee;
```

**Output:**
<img width="1174" height="375" alt="image" src="https://github.com/user-attachments/assets/5ee9d936-0458-43ae-820d-aa1c9cc7f135" />


**Question 2**
---
Write a SQL query that counts the number of unique salespeople. Return number of salespeople.

Sample table: orders
--

```sql
SELECT 
    COUNT(DISTINCT salesman_id) AS COUNT
FROM orders;
```

**Output:**
<img width="1190" height="318" alt="image" src="https://github.com/user-attachments/assets/3c6b1437-624f-4902-b685-d9b392622176" />


**Question 3**
---
Write a SQL query to find the maximum purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001
--

```sql
SELECT 
    MAX(purch_amt) AS MAXIMUM
FROM orders;
```

**Output:**
<img width="1216" height="315" alt="image" src="https://github.com/user-attachments/assets/7f6a8f2a-9917-431e-8bd4-ae1fc9adc352" />


**Question 4**
---
How many medical records does each doctor have?

Sample table:MedicalRecords Table

--

```sql
SELECT 
    DoctorID,
    COUNT(*) AS TotalRecords
FROM MedicalRecords
GROUP BY DoctorID
ORDER BY DoctorID;
```

**Output:**
<img width="1234" height="707" alt="image" src="https://github.com/user-attachments/assets/9c73cd6f-9afe-4d8a-b8d4-f6cbdcffc4fa" />


**Question 5**
---
<img width="1212" height="265" alt="image" src="https://github.com/user-attachments/assets/106f0414-d2bd-4590-815f-bb5bb08fe49e" />

--

```sql
SELECT 
    DoctorID,
    COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY DoctorID
ORDER BY DoctorID;
```

**Output:**
<img width="1155" height="633" alt="image" src="https://github.com/user-attachments/assets/65a5fc81-c793-48e4-9c75-24f293992464" />


**Question 6**
---
<img width="1173" height="260" alt="image" src="https://github.com/user-attachments/assets/161d6f06-34ca-4bb8-85e4-1f5e53597d4d" />

-- 

```sql
SELECT 
    DATE(AppointmentDateTime) AS AppointmentDate,
    COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY DATE(AppointmentDateTime);
```

**Output:**
<img width="1199" height="718" alt="image" src="https://github.com/user-attachments/assets/67e1960c-5f9e-4dcd-870a-7fe1b2135a49" />


**Question 7**
---
<img width="1239" height="285" alt="image" src="https://github.com/user-attachments/assets/3200aaf6-ae94-4458-a988-e04cd25e595d" />

--

```sql
SELECT 
    occupation,
    AVG(workhour)
FROM employee1
GROUP BY occupation
HAVING AVG(workhour) BETWEEN 10 AND 12;
```

**Output:**
<img width="1193" height="431" alt="image" src="https://github.com/user-attachments/assets/1248fe40-b54d-4870-aadf-910ded67c11d" />


**Question 8**
---
<img width="1222" height="264" alt="image" src="https://github.com/user-attachments/assets/e28b8a70-cae8-437a-9122-2217bfb33b08" />

-- 

```sql
SELECT 
    (age / 5) * 5 AS age_group,
    AVG(age)
FROM customer1
GROUP BY (age / 5) * 5
HAVING AVG(age) < 24;
```

**Output:**
<img width="1214" height="377" alt="image" src="https://github.com/user-attachments/assets/59445287-907c-4177-99bc-731f12a96b21" />


**Question 9**
---
<img width="1217" height="297" alt="image" src="https://github.com/user-attachments/assets/50f620dc-9700-4621-bb0b-87af0d5fb40e" />

-- 

```sql
SELECT 
    age,
    MAX(income)  
FROM employee
GROUP BY age
HAVING MAX(income) > 2000000;
```

**Output:**
<img width="1214" height="386" alt="image" src="https://github.com/user-attachments/assets/976b1a82-dde7-4541-8ac5-c20433935532" />


**Question 10**
---
<img width="1204" height="296" alt="image" src="https://github.com/user-attachments/assets/6cad0bb5-ed6f-4709-a990-ba2be3158ad5" />

--

```sql
SELECT 
  category_id, 
  MIN(price) AS Price
FROM products
GROUP BY category_id
HAVING MIN(price) < 10;
```

**Output:**
<img width="1229" height="426" alt="image" src="https://github.com/user-attachments/assets/8723fb8f-0cfe-4610-a9eb-20b37a3b25fe" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
