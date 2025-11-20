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
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $1500.

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
```sql
SELECT*FROM CUSTOMERS 
WHERE SALARY>1500;
```

**Output:**

<img width="498" height="469" alt="image" src="https://github.com/user-attachments/assets/ece7bba7-617b-46c0-9ae4-f7ae33ad744d" />


**Question 2**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi

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

 

```sql
SELECT*FROM CUSTOMERS
WHERE ADDRESS='Delhi';
```

**Output:**

<img width="598" height="317" alt="image" src="https://github.com/user-attachments/assets/baaaa6e1-2ab4-4680-a512-08c6c081e175" />


**Question 3**
---
Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER

```sql
SELECT name,city
FROM customer
WHERE city IN(
SELECT city
FROM customer
WHERE id IN(3,7)
);
```

**Output:**

<img width="529" height="379" alt="image" src="https://github.com/user-attachments/assets/5d2f4310-f01a-4873-928c-f8d98e8cd295" />


**Question 4**
---
Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

```sql
SELECT student_id,student_name,subject,grade
FROM GRADES g1
WHERE grade IN (
SELECT MAX(grade)
FROM GRADES g2
WHERE g1.subject=g2.subject
);
```

**Output:**

<img width="553" height="397" alt="image" src="https://github.com/user-attachments/assets/81b9c264-aa21-47fc-9255-4e9c909fa1f8" />


**Question 5**
---
Write a SQL query to Retrieve the medications with dosages equal to the highest dosage

Table Name: Medications (attributes: medication_id, medication_name, dosage)

```sql
SELECT medication_id AS medic,medication_name,dosage
FROM Medications
WHERE dosage=(SELECT MAX(dosage)
FROM Medications
);
```

**Output:**

<img width="541" height="342" alt="image" src="https://github.com/user-attachments/assets/6703f3bc-b49b-413b-92dd-8f81f735e5a6" />


**Question 6**
---
From the following tables write a SQL query to find the order values greater than the average order value of 10th October 2012. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

Note: date should be yyyy-mm-dd format

ORDERS TABLE

name            type
----------     ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int
```sql
SELECT ord_no,purch_amt,ord_date,customer_id,salesman_id
FROM ORDERS
WHERE purch_amt> (SELECT AVG(purch_amt)
FROM ORDERS
WHERE ord_date='2012-10-10'
);
```

**Output:**

<img width="544" height="428" alt="image" src="https://github.com/user-attachments/assets/b6963205-7f96-4340-9721-6a8e0a895f9c" />


**Question 7**
---
From the following tables, write a SQL query to find all the orders issued by the salesman 'Paul Adam'. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

```sql
SELECT ord_no,purch_amt,ord_date,customer_id,salesman_id
FROM orders
WHERE salesman_id IN (SELECT(salesman_id)
FROM salesman
WHERE name='Paul Adam'
);
```

**Output:**

<img width="523" height="320" alt="image" src="https://github.com/user-attachments/assets/b8a85f1d-9653-49de-bf51-a27915b492b7" />

**Question 8**
---
From the following tables write a SQL query to find salespeople who had more than one customer. Return salesman_id and name.

salesman table

name                 type
---------------   ---------------
salesman_id       numeric(5)
name                  varchar(30)
city                     varchar(15)
commission       decimal(5,2)

```sql
SELECT salesman_id, name
FROM salesman
WHERE salesman_id IN (
  SELECT salesman_id
  FROM customer
  GROUP BY salesman_id
  HAVING COUNT(*) > 1
);

```

**Output:**

<img width="525" height="360" alt="image" src="https://github.com/user-attachments/assets/877f5e65-9645-449f-87b0-46812b18269e" />

**Question 9**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 1 million

Employee Table

name             type

------------   ---------------

id                    INTEGER

name              TEXT

age                 INTEGER

city                 TEXT

income           INTEGER
```sql
SELECT id, name, age, city, income
FROM Employee
WHERE age < (
  SELECT AVG(age)
  FROM Employee
  WHERE income>1000000
);


```

**Output:**

<img width="504" height="342" alt="image" src="https://github.com/user-attachments/assets/6e1f506f-f4ff-4dad-b43b-1d54d32dbcac" />

**Question 10**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh

Employee Table

name             type

------------   ---------------

id                    INTEGER

name              TEXT

age                 INTEGER

city                 TEXT

income           INTEGER
```sql
SELECT id, name, age, city, income
FROM Employee
WHERE age < (
  SELECT AVG(age)
  FROM Employee
  WHERE income > 250000
);

```

**Output:**

<img width="535" height="471" alt="image" src="https://github.com/user-attachments/assets/a6e388f8-cb96-4389-be3d-16f1dc081e00" />


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
