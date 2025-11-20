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
How many patients have expired insurance coverage for each insurance company?

```sql
select InsuranceCompany,COUNT(PatientID)AS TotalExpiredPatients
FROM Insurance
GROUP BY InsuranceCompany;
```

**Output:**

<img width="507" height="644" alt="image" src="https://github.com/user-attachments/assets/4941f78a-e3fa-4b71-a853-d4a7be198bab" />

**Question 2**
---
How many patients are there in each city?
```sql
select Address, COUNT(PatientID) AS TotalPatients
from Patients
GROUP BY Address;
```

**Output:**

<img width="489" height="326" alt="image" src="https://github.com/user-attachments/assets/ce17d337-5178-4771-bc88-e38939e0f6d1" />

**Question 3**
---
How many medical records are there for each patient?


```sql
select PatientID , COUNT(RecordID) as TotalRecords
from MedicalRecords
GROUP BY PatientID
```

**Output:**

<img width="462" height="479" alt="image" src="https://github.com/user-attachments/assets/6319d1f9-c4b2-4e35-97b4-19678216496d" />

**Question 4**
---
Write a SQL query to calculate total available amount of fruits that has a price greater than 0.5 . Return total Count. 

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL

```sql
select SUM(inventory)as total_available_amount
from fruits
where price>0.5;
```

**Output:**

<img width="571" height="314" alt="image" src="https://github.com/user-attachments/assets/e2df7749-36f6-40b0-81c7-521dcecc83de" />

**Question 5**
---
Write a SQL query to count the number of customers. Return number of customers.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002

```sql
select COUNT(customer_id)as COUNT
from customer
```

**Output:**

<img width="503" height="285" alt="image" src="https://github.com/user-attachments/assets/5cf9b45c-108c-4385-acea-114d64beb448" />

**Question 6**
---
Write a SQL query to  find the average salary of all employees?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
 
```sql
select avg(income)as Average_Salary
from employee;
```

**Output:**

<img width="568" height="245" alt="image" src="https://github.com/user-attachments/assets/e1f98236-8d7d-4e23-9a68-0b026a2cb494" />

**Question 7**
---
Write a SQL query to find the difference between the maximum and minimum price of fruits?

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
```sql
select MAX(price)-MIN(price)as price_diff
from fruits;
```

**Output:**

<img width="499" height="241" alt="image" src="https://github.com/user-attachments/assets/7d0cf382-c0cb-4fb0-bafa-aebaf445766d" />

**Question 8**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the maximum work hours for each date, and excludes dates where the maximum work hour is not greater than 12.
```sql
select jdate ,MAX(workhour) 
from employee1 
GROUP BY jdate
HAVING MAX(workhour)>12;
```

**Output:**

<img width="469" height="318" alt="image" src="https://github.com/user-attachments/assets/53deda1f-615b-451f-9507-f8c8e13d32c9" />

**Question 9**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the total work hours for each date, and excludes dates where the total work hour sum is not greater than 40.
```sql
select jdate,SUM(workhour)
from employee1
group by jdate
having SUM(workhour)>40;
```

**Output:**

<img width="544" height="348" alt="image" src="https://github.com/user-attachments/assets/262ae2d7-c75b-4432-ac1d-e8c38f62a428" />

**Question 10**
---
Write the SQL query that achieves the grouping of data by age intervals using the expression (age/5)5, calculates the total salary sum for each group, and excludes groups where the total salary sum is not greater than 5000.
```sql
select (age/5)*5 as age_group , SUM(salary)
from customer1
GROUP BY age_group
having SUM(salary)>5000;
```

**Output:**

<img width="503" height="324" alt="image" src="https://github.com/user-attachments/assets/87921992-f1d9-42ad-9354-037b3e4c707a" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
