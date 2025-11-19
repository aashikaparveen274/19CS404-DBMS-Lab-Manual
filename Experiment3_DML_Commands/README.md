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
Write a SQL statement to Update the hire_date of employees in department 50 to 2024-01-24.

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
```sql
UPDATE Employees 
SET hire_date = '2024-01-24'
WHERE department_id = 50;
```

**Output:**


<img width="1036" height="190" alt="image" src="https://github.com/user-attachments/assets/afddbc8f-6d4b-4c52-853c-050d9de4680d" />

**Question 2**
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
```sql
UPDATE suppliers 
SET supplier_name = UPPER(supplier_name)
WHERE contact_person LIKE '%Singh%';
```

**Output:**


<img width="1167" height="202" alt="image" src="https://github.com/user-attachments/assets/434acd29-959b-4875-8bf8-a78b69117562" />


**Question 3**
---
Write a SQL statement to Update the per_unit_price to 25 and total_price accordingly in purchases table where purchase_date is '2022-08-15' and product_id is 12.

```sql
UPDATE purchases 
SET per_unit_price=25,
    total_price=quantity*25
WHERE purchase_date='2022-08-15' and product_id=12;
```

**Output:**


<img width="1133" height="322" alt="image" src="https://github.com/user-attachments/assets/3baa1a1c-9171-44dc-b67e-2bc45467d598" />

**Question 4**
---
Increase the reorder level by 30% for products from 'Food' category having quantity in stock less than 50% of existing reorder level in the products table
name               type
--------------  ----------
product_id         INT
product_name       VARCHAR(10)
category           VARCHAR(50)
cost_price         DECIMAL(10)
sell_price         DECIMAL(10)
reorder_lvl        INT
quantity              INT
supplier_id           INT
```sql
UPDATE products 
SET reorder_lvl=reorder_lvl*1.3
WHERE category='Food' AND quantity < (reorder_lvl*0.5);
```

**Output:**


<img width="1135" height="249" alt="image" src="https://github.com/user-attachments/assets/7d05a8ef-82e2-43f3-9a77-c094fa0ba8e8" />

**Question 5**
---
Write a SQL statement to Increase the selling price by 10% for all products in the 'Bakery' category in the products table.

Products table

---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id
```sql
UPDATE Products
SET sell_price=sell_price*1.10
WHERE category ='Bakery';
```

**Output:**


<img width="1023" height="353" alt="image" src="https://github.com/user-attachments/assets/7334b827-5564-4cb7-9df1-deaa937914db" />

**Question 6**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is odd.


```sql
DELETE FROM customer
WHERE GRADE % 2!=0;
```

**Output:**


<img width="1063" height="312" alt="image" src="https://github.com/user-attachments/assets/8db8dc15-0c69-40f8-b0dd-168b34f407e3" />


**Question 7**
---
Write a SQL query to Delete customers with 'GRADE' 3 or 'AGENT_CODE' 'A008' whose 'OUTSTANDING_AMT' is less than 5000
```sql
DELETE FROM Customer
WHERE (GRADE=3 OR AGENT_CODE='A008' ) AND OUTSTANDING_AMT<5000;
```

**Output:**


<img width="1117" height="303" alt="image" src="https://github.com/user-attachments/assets/8af392c9-9cc4-45d8-8888-b3afaf83d7a1" />

**Question 8**
---
Write a SQL query to Delete customers from 'customer' table where 'CUST_NAME' has exactly 6 characters.
```sql
DELETE FROM Customer
WHERE LENGTH(CUST_NAME)=6;
```

**Output:**


<img width="1107" height="585" alt="image" src="https://github.com/user-attachments/assets/e066e6b6-11e9-4e3a-894f-95f942bf96ac" />

**Question 9**
---
Write a SQL query to Delete customers with following conditions

'CUST_COUNTRY' is not in a list of specified countries ('UK', 'USA', 'Canada')
'GRADE' is greater than or equal to 3

```sql
DELETE FROM Customer
WHERE CUST_COUNTRY NOT IN ('UK','USA','Canada')
and GRADE>=3;
```

**Output:**


<img width="1043" height="368" alt="image" src="https://github.com/user-attachments/assets/615267b2-dfc2-48cf-b57e-c67a0537f1f4" />


**Question 10**
---
Write a SQL query to Delete a Specific Surgery whose ID is 3
```sql
DELETE FROM Surgeries 
where surgery_id=3;
```

**Output:**


<img width="1267" height="335" alt="image" src="https://github.com/user-attachments/assets/13c396a1-b2c1-47cc-bee8-15d568614d6b" />

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
