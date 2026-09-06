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
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.

```sql
select o.ord_no,o.purch_amt,c.cust_name,c.city 
from orders as o  
join customer as c
on o.customer_id=c.customer_id
where o.purch_amt between 500 and 2000;
```

**Output:**

<img width="1230" height="499" alt="image" src="https://github.com/user-attachments/assets/93e3b40a-4867-4d53-8c4c-cdb22fb51b4a" />

**Question 2**
---
Write a SQL statement to join the tables salesman, customer and orders so that the same column of each table appears once and only the relational rows are returned. 

```sql
SELECT 
    o.ord_no,
    o.purch_amt,
    o.ord_date,
    c.cust_name,
    c.city AS customer_city,
    c.grade,
    s.name AS salesman_name,
    s.city AS salesman_city,
    s.commission
FROM 
    orders AS o
JOIN 
    customer AS c 
    ON o.customer_id = c.customer_id
JOIN 
    salesman AS s 
    ON o.salesman_id = s.salesman_id;
```

**Output:**

<img width="1335" height="650" alt="image" src="https://github.com/user-attachments/assets/b9484f67-7ad2-41a8-994c-38f3be085dbf" />

**Question 3**
---
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for test results with a test date between '2024-03-01' and '2024-03-31'.

```sql
select 
p.patient_id,
p.first_name,
p.last_name,
p.date_of_birth,
p.admission_date,
p.discharge_date,
p.doctor_id
from patients as p
inner join test_results as t
on p.patient_id=t.patient_id
where t.test_date between '2024-03-01' and '2024-03-31';
```

**Output:**

<img width="1112" height="238" alt="image" src="https://github.com/user-attachments/assets/388bb8f0-acad-4774-9021-239cfb0d91f6" />

**Question 4**
---
 From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission.

```sql
select
c.cust_name as 'Customer Name',
c.city,
s.name as 'Salesman',
s.commission
from customer as c
join salesman as s
on c.salesman_id=s.salesman_id;
```

**Output:**

<img width="688" height="508" alt="image" src="https://github.com/user-attachments/assets/2e54f316-f259-41ad-982f-4b21b2ea3342" />

**Question 5**
---
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for appointments with an appointment date between '2024-02-01' and '2024-02-28'.

```sql
select 
p.patient_id,
p.first_name,
p.last_name,
p.date_of_birth,
p.admission_date,
p.discharge_date,
p.doctor_id
from patients as p
inner join appointments as a
on p.patient_id=a.patient_id
where a.appointment_date between '2024-02-01' and '2024-02-28';
```

**Output:**

<img width="1073" height="233" alt="image" src="https://github.com/user-attachments/assets/3bc70cca-2c11-4048-9dba-c313059c918d" />

**Question 6**
---
From the following tables write a SQL query to find salespeople who received commissions of more than 12 percent from the company. Return Customer Name, customer city, Salesman, commission.  

```sql
SELECT 
    c.cust_name AS "Customer Name",
    c.city ,
    s.name AS Salesman,
    s.commission
FROM 
    customer AS c
JOIN 
    salesman AS s
ON 
    c.salesman_id = s.salesman_id
WHERE 
    s.commission > 0.12;
```

**Output:**

<img width="689" height="428" alt="image" src="https://github.com/user-attachments/assets/32ee56f7-6108-42a0-8b8f-31953a4fdb4f" />

**Question 7**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the test name from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column.

```sql
SELECT 
    p.first_name AS patient_name,
    t.test_name
FROM 
    patients AS p
INNER JOIN 
    test_results AS t
ON 
    p.patient_id = t.patient_id;
```

**Output:**

<img width="460" height="315" alt="image" src="https://github.com/user-attachments/assets/1a4457bb-4245-4f04-90c9-b8fc62027968" />

**Question 8**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), the "cust_name," "city," "grade," and "salesman_id" columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for salesman_id values that have more than one associated customer.

```sql
SELECT 
    s.name,
    c.cust_name,
    c.city,
    c.grade,
    c.salesman_id
FROM salesman AS s
LEFT JOIN customer AS c
ON s.salesman_id = c.salesman_id
WHERE c.salesman_id IN (
        SELECT c.salesman_id
        FROM customer as c
        GROUP BY salesman_id
        HAVING COUNT(customer_id) > 1)
ORDER BY s.name, c.grade;    
```

**Output:**

<img width="838" height="353" alt="image" src="https://github.com/user-attachments/assets/54e3bd63-01a0-42c3-8e4d-f76ba9e62bdb" />

**Question 9**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), the "cust_name," "city," "grade," and "salesman_id" columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for customers with a grade less than or equal to 100.

```sql
SELECT 
    s.name,
    c.cust_name,
    c.city,
    c.grade,
    c.salesman_id
FROM salesman AS s
LEFT JOIN customer AS c
ON s.salesman_id = c.salesman_id
WHERE c.grade <= 100;
```

**Output:**

<img width="867" height="326" alt="image" src="https://github.com/user-attachments/assets/e35fb265-27b1-43dd-aaa6-7a1e25203b01" />

**Question 10**
---
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.  

```sql
SELECT 
    c.cust_name,
    c.city,
    c.grade,
    s.name AS Salesman,
    s.city 
FROM customer AS c
JOIN salesman AS s
ON c.salesman_id = s.salesman_id
ORDER BY c.customer_id ASC;
```

**Output:**

<img width="833" height="504" alt="image" src="https://github.com/user-attachments/assets/4a7ddb60-9fe9-40c6-8fd8-8cb3362ce49c" />

## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
