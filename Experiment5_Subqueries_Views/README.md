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
<img width="894" height="320" alt="image" src="https://github.com/user-attachments/assets/0831b64f-085a-444f-834b-36aa9c2283a5" />

-- 

```sql
SELECT medication_id, medication_name, dosage
FROM Medications
WHERE dosage = (
    SELECT MIN(dosage)
    FROM Medications
);
```

**Output:**
<img width="1201" height="469" alt="image" src="https://github.com/user-attachments/assets/f59f12fb-da40-4248-9ab2-28ee68bed1d3" />


**Question 2**
---
<img width="1171" height="404" alt="image" src="https://github.com/user-attachments/assets/004d2439-c50d-4dcd-99c2-a2f65e956ea3" />

--

```sql
SELECT *
FROM Grades g
WHERE grade = (
    SELECT MAX(grade)
    FROM Grades
    WHERE subject = g.subject
);
```

**Output:**
<img width="1209" height="524" alt="image" src="https://github.com/user-attachments/assets/a2661ac4-26b2-433c-8282-11b7be7f4b1f" />


**Question 3**
---
Write a SQL query to List departments with names longer than the average length

Departments Table
-- 

```sql
SELECT department_id, department_name
FROM departments
WHERE LENGTH(department_name) > (
    SELECT AVG(LENGTH(department_name))
    FROM departments
);
```

**Output:**
<img width="857" height="414" alt="image" src="https://github.com/user-attachments/assets/fe86f0df-3f91-44bb-b1f8-9629f2b429e9" />


**Question 4**
---
<img width="1126" height="387" alt="image" src="https://github.com/user-attachments/assets/378eda89-0f44-42e6-93ba-e73d8f84381d" />

-- 

```sql
SELECT *
FROM Customers
WHERE address = 'Delhi';
```

**Output:**
<img width="1198" height="368" alt="image" src="https://github.com/user-attachments/assets/d66e807e-8afa-41f9-9cf1-f4ae089f2b5a" />

**Question 5**
---
<img width="1111" height="345" alt="image" src="https://github.com/user-attachments/assets/873ec9d3-24dd-4eb0-aff6-1a024d70d27c" />

-- 

```sql
SELECT *
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 1000000
);
```

**Output:**
<img width="1193" height="397" alt="image" src="https://github.com/user-attachments/assets/5626cf8d-f9be-4812-af6a-b7db12a900d6" />


**Question 6**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi and age below 30

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
-- 

```sql
SELECT *
FROM CUSTOMERS
WHERE ADDRESS = 'Delhi'
AND AGE < 30
ORDER BY ID;
```

**Output:**
<img width="1204" height="390" alt="image" src="https://github.com/user-attachments/assets/f756912c-c957-4235-ab8c-d67000412274" />


**Question 7**
---
<img width="1203" height="448" alt="image" src="https://github.com/user-attachments/assets/e02491aa-ef23-46b1-a5a0-6cfac8a8ae1c" />

-- 

```sql
SELECT o.ord_no, o.purch_amt, o.ord_date, o.customer_id, o.salesman_id
FROM orders o
JOIN salesman s ON o.salesman_id = s.salesman_id
WHERE s.city = 'New York';
```

**Output:**
<img width="1215" height="506" alt="image" src="https://github.com/user-attachments/assets/08e332d6-4e78-491a-8db8-ca37ae6fb40e" />


**Question 8**
---
<img width="1195" height="443" alt="image" src="https://github.com/user-attachments/assets/731ce69e-9baa-4c02-99f2-4e349cae0dd2" />

-- 

```sql
SELECT o.ord_no, o.purch_amt, o.ord_date, o.customer_id, o.salesman_id
FROM orders o
JOIN salesman s ON o.salesman_id = s.salesman_id
WHERE s.city = 'London';
```

**Output:**
<img width="1223" height="419" alt="image" src="https://github.com/user-attachments/assets/14edb397-9918-4a94-999b-1f036eb0d762" />


**Question 9**
---
<img width="1201" height="275" alt="image" src="https://github.com/user-attachments/assets/150a7df5-f99d-4a57-be3c-c23318fde56c" />

-- 

```sql
SELECT grade, COUNT(*)
FROM customer
WHERE grade > (
    SELECT AVG(grade)
    FROM customer
    WHERE city = 'New York'
)
GROUP BY grade;
```

**Output:**
<img width="637" height="322" alt="image" src="https://github.com/user-attachments/assets/da75e55a-89d3-4b63-85a5-93add61b0085" />


**Question 10**
---
Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES
--

```sql
SELECT *
FROM Grades g
WHERE grade = (
    SELECT MAX(grade)
    FROM Grades
    WHERE subject = g.subject
);

```

**Output:**
<img width="1193" height="443" alt="image" src="https://github.com/user-attachments/assets/1d58b4a8-cd63-440c-859a-88dc62436ef3" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
