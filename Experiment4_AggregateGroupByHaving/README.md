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
-- Write a SQL query to find the average length of names for people living in Chennai?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT   
city        TEXT
email       TEXT
phone       INTEGER

```sql
--
SELECT AVG(LENGTH(name)) AS avg_name_length
FROM customer
WHERE city = 'Chennai';
```

**Output:**

<img width="653" height="328" alt="image" src="https://github.com/user-attachments/assets/4731a9e8-cdf8-44d7-ac68-7f0736ba454e" />

**Question 2**
---
-- Write a SQL query to calculate total available amount of fruits that has a price greater than 0.5 . Return total Count. 

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
--
SELECT SUM(inventory) AS total_available_amount
FROM fruits
WHERE price > 0.5;
```

**Output:**

<img width="595" height="331" alt="image" src="https://github.com/user-attachments/assets/73932851-c879-4342-9b19-002d1e12b063" />


**Question 3**
---
-- What is the average dosage prescribed for each medication?

Sample tablePrescriptions Table
<img width="1082" height="154" alt="image" src="https://github.com/user-attachments/assets/be33ff24-2a55-4ba9-958a-24db921c0ff4" />



```sql
--
 SELECT Medication, AVG(Dosage) AS AvgDosage
FROM Prescriptions
GROUP BY Medication;
```

**Output:**

<img width="761" height="693" alt="image" src="https://github.com/user-attachments/assets/b3c03d33-574f-4ac3-9a07-4a55cc51c4fb" />

**Question 4**
---
-- How many prescriptions were written by each doctor?

Sample tablePrescriptions Table

<img width="1082" height="154" alt="image" src="https://github.com/user-attachments/assets/eed5770c-b9f9-4538-a203-30f9f6873e9c" />


```sql
--
SELECT DoctorID, COUNT(*) AS TotalPrescriptions
FROM Prescriptions
GROUP BY DoctorID;
```

**Output:**

<img width="867" height="712" alt="image" src="https://github.com/user-attachments/assets/3b8e4675-88c7-464a-947e-8517073281b7" />


**Question 5**
---
--
Write the SQL query that achieves the selection of category and calculates the sum of the product of price and category ID as Revenue for each category from the "products" table, and includes only those products where the total revenue is greater than 25.

Sample table: products
<img width="972" height="212" alt="image" src="https://github.com/user-attachments/assets/2d0cd2ec-771f-46d3-a2d2-e7316072e204" />




```sql
--
SELECT category_id,
       SUM(price * category_id) AS Revenue
FROM products
GROUP BY category_id
HAVING SUM(price * category_id) > 25;
```

**Output:**

<img width="738" height="421" alt="image" src="https://github.com/user-attachments/assets/adf2921a-6e99-4d55-bbca-859468c7cb56" />

**Question 6**
---
-- Write the SQL query that achieves the grouping of data by age intervals using the expression (age/5)5, calculates the average age for each group, and excludes groups where the average age is not less than 24.

Sample table: customer1
<img width="992" height="173" alt="image" src="https://github.com/user-attachments/assets/b23ad164-042c-4e87-a2e4-3cf09599c036" />


```sql
--
SELECT (age / 5) * 5 AS age_group,
       AVG(age) AS "AVG(age)"
FROM customer1
GROUP BY (age / 5) * 5
HAVING AVG(age) < 24;
```

**Output:**

<img width="684" height="348" alt="image" src="https://github.com/user-attachments/assets/11838e4a-95a1-4aaa-a6ca-824326a52372" />

**Question 7**
---
-- Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the minimum work hours for each date, and excludes dates where the minimum work hour is not less than 10.

Sample table: employee1
<img width="1031" height="203" alt="image" src="https://github.com/user-attachments/assets/5a6d7266-c1ba-4bbd-935b-a07995e81008" />


```sql
--
SELECT jdate, MIN(workhour) AS "MIN(workhour)"
FROM employee1
GROUP BY jdate
HAVING MIN(workhour) < 10;
```

**Output:**

<img width="945" height="423" alt="image" src="https://github.com/user-attachments/assets/183831cb-3192-44d6-a55c-1a79f78d372d" />

**Question 8**
---
-- Write the SQL query that accomplishes the grouping of data by age, calculates the total income for each age group, and includes only those age groups where the total income sum is greater than 1,000,000.

Sample table: employee
<img width="1011" height="215" alt="image" src="https://github.com/user-attachments/assets/2a27ee65-0a5f-4a0d-a4c7-22f8ba3f3a6b" />


```sql
--
SELECT age, SUM(income) AS "SUM(income)"
FROM employee
GROUP BY age
HAVING SUM(income) > 1000000;
```

**Output:**

<img width="777" height="417" alt="image" src="https://github.com/user-attachments/assets/51e2eaa9-e9f6-4769-8010-144079ffb1ae" />

**Question 9**
---
-- Write a SQL query to return the total number of rows in the 'customer' table where the city is not Noida.

Sample table: customer

<img width="668" height="138" alt="image" src="https://github.com/user-attachments/assets/9e5733c8-cf58-46f3-8b40-732b9ac998b0" />


```sql
--
SELECT COUNT(*) AS COUNT
FROM customer
WHERE city <> 'Noida';
```

**Output:**

<img width="612" height="332" alt="image" src="https://github.com/user-attachments/assets/e7eb0f25-981b-4a36-b402-3d13afc7f36c" />

**Question 10**
---
-- What is the total number of appointments scheduled for each day?

Sample table:Appointments Table
<img width="998" height="163" alt="image" src="https://github.com/user-attachments/assets/fa405fc8-bea6-48fb-869b-0371f5aa16eb" />


```sql
--
select patientid,count(*) as TotalAppointments
from appointments
group by patientid;
```

**Output:**

<img width="780" height="572" alt="image" src="https://github.com/user-attachments/assets/b31b3737-06f2-4104-96ee-9716b7bd9555" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
