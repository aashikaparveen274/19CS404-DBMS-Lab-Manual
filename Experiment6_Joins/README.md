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
From the following tables write a SQL query to find those customers with a grade less than 300. Return cust_name, customer city, grade, Salesman, salesmancity. The result should be ordered by ascending customer_id. 

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12

```sql
SELECT 
    c.cust_name,
    c.city as city,
    c.grade,
    s.name as Salesman,
    s.city as city
FROM 
    customer c 
JOIN 
    salesman s on c.salesman_id=s.salesman_id
WHERE
    c.grade<300
ORDER BY 
    c.customer_id ASC;
```

**Output:**

<img width="517" height="610" alt="image" src="https://github.com/user-attachments/assets/8595a19a-7122-40b8-854e-3b20aad4ecf2" />

**Question 2**
---
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for appointments with an appointment date between '2024-01-01' and '2024-01-31'.

```sql
SELECT p.*
FROM patients p
INNER JOIN appointments a
ON p.patient_id=a.patient_id
WHERE a.appointment_date BETWEEN '2024-01-01' AND '2024-01-31';
```

**Output:**

<img width="517" height="391" alt="image" src="https://github.com/user-attachments/assets/41d400d4-eee3-4900-aa55-cc695e1909b2" />

**Question 3**
---
Write the SQL query that accomplishes the selection of the first name from the "patients" table (aliased as "patient_name") and the first name from the "doctors" table (aliased as "doctor_name"), with an inner join on the "doctor_id" column and a condition filtering for patients with a non-null discharge date.
```sql
SELECT 
    p.first_name as patient_name,
    d.first_name as doctor_name
FROM 
    PATIENTS p
INNER JOIN
    DOCTORS d on p.doctor_id=d.doctor_id
WHERE
    p.discharge_date is not null;
```

**Output:**

<img width="515" height="354" alt="image" src="https://github.com/user-attachments/assets/def89501-7410-4dc8-88f7-02fad492c8f9" />

**Question 4**
---
 From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
```sql
SELECT 
    c.cust_name as "Customer Name",
    c.city,
    s.name as "Salesman",
    s.commission
FROM 
    customer c
INNER JOIN 
    salesman s on c.salesman_id=s.salesman_id;
```

**Output:**

<img width="512" height="778" alt="image" src="https://github.com/user-attachments/assets/fb248d94-b5b1-44f9-a2d0-d2e0844ccead" />

**Question 5**
---
 From the following tables write a SQL query to find salespeople who received commissions of more than 12 percent from the company. Return Customer Name, customer city, Salesman, commission.  

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
```sql
SELECT
    c.cust_name AS "Customer Name",
    c.city AS "city",
    s.Name AS "Salesman",
    s.commission AS "commission"
FROM 
    customer c
JOIN 
    salesman s on c.salesman_id=s.salesman_id
WHERE
    s.commission>0.12;
```

**Output:**

<img width="514" height="620" alt="image" src="https://github.com/user-attachments/assets/e92d93f1-44c1-4ab5-98cc-dd838d4a52cc" />

**Question 6**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "salesman_name") and the "cust_name" column from the "customer" table (aliased as "customer_name"), with a left join on the "salesman_id" column.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)
```sql
SELECT 
    s.name AS salesman_name,
    c.cust_name AS customer_name
FROM 
    Salesman s 
LEFT JOIN
    Customer c on s.salesman_id=c.salesman_id;
```

**Output:**

![Output6](output.png)

**Question 7**
---
Write the SQL query that achieves the selection of admission dates from the "patients" table and surgery dates from the "surgeries" table, with an inner join on the "patient_id" column.
```sql
SELECT p.admission_date, s.surgery_date
FROM patients p
INNER JOIN surgeries s
ON p.patient_id=s.patient_id;
```

**Output:**

<img width="510" height="487" alt="image" src="https://github.com/user-attachments/assets/8309a642-c6b0-4039-bc4d-5fd5f7fbea36" />

**Question 8**
---
Write a SQL statement to make a report with customer name, city, order number, order date, and order amount in ascending order according to the order date to determine whether any of the existing customers have placed an order or not.
```sql
SELECT 
    c.cust_name,
    c.city,
    o.ord_no,
    o.ord_date,
    o.purch_amt AS "Order Amount"
FROM 
    customer c
LEFT JOIN 
    orders o ON c.customer_id=o.customer_id
ORDER BY 
    o.ord_date ASC;
    
```

**Output:**

<img width="497" height="838" alt="image" src="https://github.com/user-attachments/assets/1bfe0743-ab20-4afd-8774-a8906699d6d6" />

**Question 9**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), the "cust_name," "city," "grade," and "salesman_id" columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for salesman_id values that have more than one associated customer.
```sql
SELECT 
    s.name,
    c.cust_name,
    c.city,
    c.grade,
    c.salesman_id
FROM 
    salesman s
LEFT JOIN customer c ON s.salesman_id=c.salesman_id
WHERE s.salesman_id IN (
    SELECT salesman_id
    FROM customer
    GROUP BY salesman_id
    HAVING COUNT(customer_id)>1
);
```

**Output:**

<img width="525" height="468" alt="image" src="https://github.com/user-attachments/assets/4e356fb0-bafa-44b7-8da5-4128144af2a9" />

**Question 10**
---
write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.
```sql
SELECT 
    s.name AS Salesman,
    c.cust_name,
    c.city
FROM 
    salesman s
JOIN customer c on s.city = c.city;
```

**Output:**

<img width="497" height="484" alt="image" src="https://github.com/user-attachments/assets/13921010-340e-4b1f-afb8-b295df3da3ed" />


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
