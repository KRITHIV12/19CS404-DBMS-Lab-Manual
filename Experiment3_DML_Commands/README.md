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
-- 
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
 

For example:

Result
id          base        base_status
----------  ----------  -----------
1           2           Provided
2           3           Provided
3           3           Provided
4           4           Provided


```sql
-- SELECT
    id,
    base,
    CASE 
       WHEN base IS NOT NULL THEN 'Provided'
    ELSE 'Not Provided'
    END AS base_status
FROM Calculations;
```

**Output:**

<img width="1311" height="482" alt="image" src="https://github.com/user-attachments/assets/224ec181-8fde-40ea-8081-0ad1f6957f58" />


**Question 2**
---
-- 
Write a SQL query to find all employees along with the day of the week on which they were hired from the emp table

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
For example:

Result
ename       hiredate    day_of_week
----------  ----------  -----------
JONES       1981-04-02  Thursday
MARTIN      1981-09-28  Monday
BLAKE       1981-05-01  Friday
CLARK       1981-06-09  Tuesday
SCOTT       1982-12-09  Thursday
KING        1981-11-17  Tuesday
TURNER      1981-09-08  Tuesday


```sql
-- SELECT
    ename,
    hiredate,
    CASE strftime ('%w',hiredate)
       WHEN '0' THEN 'Sunday'
       WHEN '1' THEN 'Monday'
       WHEN '2' THEN 'Tuesday'
       WHEN '3' THEN 'Wednesday'
       WHEN '4' THEN 'Thursday'
       WHEN '5' THEN 'Friday'
       WHEN '6' THEN 'Saturday'
    END AS day_of_week
FROM emp;
```

**Output:**

<img width="1313" height="389" alt="image" src="https://github.com/user-attachments/assets/0b772adb-d033-4896-9549-a33bedb26db1" />


**Question 3**
---
-- 
Write a SQL query to Delete All Doctors with a NULL Specialization

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
For example:

Test	Result
SELECT * FROM doctors;
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics
4           Febin       Jones
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics


```sql
--
DELETE FROM Doctors
WHERE Specialization IS NULL;
```

**Output:**
<img width="1305" height="920" alt="image" src="https://github.com/user-attachments/assets/e8009932-d103-4b6e-af88-a7c074f95896" />


**Question 4**
---
-- 
Write a SQL statement to change the email column of employees table with 'Unavailable' for all employees in employees table.


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

                             

For example:

Test	Result
SELECT EMPLOYEE_ID,FIRST_NAME,EMAIL FROM EMPLOYEES LIMIT 2;
EMPLOYEE_ID  FIRST_NAME  EMAIL
-----------  ----------  -----------
100          Steven      Unavailable
101          Neena       Unavailable


```sql
--
UPDATE employees
SET email ='Unavailable';
```

**Output:**

<img width="1301" height="498" alt="image" src="https://github.com/user-attachments/assets/24a7b95c-fef1-4df0-8e0b-879465be9651" />


**Question 5**
---
-- Write a SQL query to Delete customers with 'GRADE' 3 or 'AGENT_CODE' 'A008' whose 'OUTSTANDING_AMT' is less than 5000

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
changes()
----------
1


```sql
-- 
       
DELETE FROM Customer
WHERE (GRADE = 3 OR AGENT_CODE = 'A008')
  AND OUTSTANDING_AMT < 5000;
```

**Output:**

<img width="1332" height="563" alt="image" src="https://github.com/user-attachments/assets/761ed592-c41d-4ae2-a290-5624d10f55b9" />

**Question 6**
---
-- Write a query to fetch details of employees whose EmpLname ends with an alphabet ‘A’ and contains five alphabets.
EmployeeInfo Table

EmpID

EmpFname

EmpLname

Department

Project

Address

DOB

Gender

1

Sanjay

Mehra

HR

P1

Hyderabad(HYD)

01/12/1976

M

2

Ananya

Mishra

Admin

P2

Delhi(DEL)

02/05/1968

F



For example:

Result
EmpID       EmpFname    EmpLname    Department  Project     Address         DOB         Gender
----------  ----------  ----------  ----------  ----------  --------------  ----------  ----------
1           Sanjay      Mehra       HR          P1          Hyderabad(HYD)  1976-12-01  M

```sql
-- SELECT * FROM EmployeeInfo
WHERE EmpLname LIKE '____A';
```

**Output:**
<img width="1344" height="301" alt="image" src="https://github.com/user-attachments/assets/243f4cf0-d544-47ab-afa0-577060e6a7d7" />

**Question 7**
---
--  Write a query to fetch only the place name(string before brackets) from the Address column of EmployeeInfo table.

EmpID

EmpFname

EmpLname

Department

Project

Address

DOB

Gender

1

Sanjay

Mehra

HR

P1

Hyderabad(HYD)

01/12/1976

M

2

Ananya

Mishra

Admin

P2

Delhi(DEL)

02/05/1968

F

 

For example:

Result
PlaceName
----------
Hyderabad
Delhi
Mumbai
Hyderabad
Delhi


```sql
--
SELECT substr(Address, 1, instr(Address, '(') - 1) AS PlaceName
FROM EmployeeInfo;
```

**Output:**

<img width="1318" height="330" alt="image" src="https://github.com/user-attachments/assets/095a20a9-47bd-4cda-b003-0f5cb553234e" />

**Question 8**
---
-- Write a SQL statement to Increase the selling price per unit by 5% for product ID 15 who's sale is on '2023-01-31'.

sales(sale_id,sale_date,product_id,quantity,sell_price,total_sell_price)

For example:

Test	Result
select changes();
changes()
----------
3


```sql
--
UPDATE sales
SET sell_price = sell_price * 1.05
WHERE product_id = 15
  AND sale_date = '2023-01-31';
```

**Output:**

<img width="1313" height="441" alt="image" src="https://github.com/user-attachments/assets/dabc1d1e-3130-49e0-8baf-e31ef7a8d616" />

**Question 9**
---
-- Write a SQL query to calculate the original price using the discount percentage and the given discounted price. Return product_id, discounted_price, discount_percentage, and original_price.

Sample table: Products

product_id | discounted_price | discount_percentage

 ------------+------------------+---------------------

 101 | 45.00 | 0.10 

102 | 63.75 | 0.15 

103 | 80.00 | 0.20

 

 

 

For example:

Result
product_id  discounted_price  discount_percentage  original_price
----------  ----------------  -------------------  --------------
101         45.0              0.1                  50.0
102         63.75             0.15                 75.0
103         80.0              0.2                  100.0

```sql
-- SELECT
    product_id,
    discounted_price,
    discount_percentage,
    discounted_price / (1 - discount_percentage) AS original_price
FROM Products;
```

**Output:**
<img width="1315" height="312" alt="image" src="https://github.com/user-attachments/assets/db4d0183-9f4c-448e-a4b4-64b73db37874" />


**Question 10**
---
-- Write a SQL query to find all those customers who does not have any grade. Return customer_id, cust_name, city, grade, salesman_id.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
For example:

Result
customer_id  cust_name    city        grade       salesman_id
-----------  -----------  ----------  ----------  -----------
1            John Mathew  New York                5000
2            Michel John  Paris                   2000

```sql
--SELECT
    customer_id,
    cust_name,
    city,
    grade,
    salesman_id
FROM customer
WHERE grade IS NULL;
```

**Output:**

<img width="1301" height="398" alt="image" src="https://github.com/user-attachments/assets/04913dd7-0ff0-4a4b-b8b5-3575211767fb" />

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
