# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
-- Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
--
CREATE TABLE Shipments (
    ShipmentID INTEGER PRIMARY KEY,
    ShipmentDate DATE,
    SupplierID INTEGER,
    OrderID INTEGER,
    FOREIGN KEY (SupplierID) REFERENCES Suppliers(SupplierID),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);

```

**Output:**

<img width="1288" height="258" alt="image" src="https://github.com/user-attachments/assets/d89dbc40-c50f-4ec2-8514-1ae6a5042034" />

**Question 2**
---
-- Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.

```sql
--
CREATE TABLE Products (
    ProductID INTEGER PRIMARY KEY,
    ProductName TEXT NOT NULL,
    Price REAL CHECK (Price > 0),
    Stock INTEGER CHECK (Stock >= 0)
);

```

**Output:**

<img width="1296" height="298" alt="image" src="https://github.com/user-attachments/assets/eaaeae94-c104-4720-91ef-493f10a79d0b" />

**Question 3**
---
-- Create a table named Products with the following constraints:
ProductID as INTEGER should be the primary key.
ProductName as TEXT should be unique and not NULL.
Price as REAL should be greater than 0.
StockQuantity as INTEGER should be non-negative.

```sql
-- CREATE TABLE Products (
    ProductID INTEGER PRIMARY KEY,
    ProductName TEXT UNIQUE NOT NULL,
    Price REAL CHECK (Price > 0),
    StockQuantity INTEGER CHECK (StockQuantity >= 0)
);

```

**Output:**

<img width="1288" height="300" alt="image" src="https://github.com/user-attachments/assets/cd56f0a8-af19-4e2c-89b1-c377e11da662" />

**Question 4**
---
-- In the Employee table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

EmployeeID  Name          Position    Department  Salary
----------  ------------  ----------  ----------  ----------
5           George Clark  Consultant
7           Noah Davis    Manager     HR          60000
8           Ava Miller    Consultant  IT
 

```sql
-- INSERT INTO Employee (EmployeeID, Name, Position, Department, Salary)
VALUES (5, 'George Clark', 'Consultant', NULL, NULL);

INSERT INTO Employee (EmployeeID, Name, Position, Department, Salary)
VALUES (7, 'Noah Davis', 'Manager', 'HR', 60000);

INSERT INTO Employee (EmployeeID, Name, Position, Department, Salary)
VALUES (8, 'Ava Miller', 'Consultant', 'IT', NULL);
```

**Output:**

<img width="1289" height="294" alt="image" src="https://github.com/user-attachments/assets/e2ed2dba-dec3-4528-bb8a-22e77ee2798e" />


**Question 5**
---
-- Write an SQL query to add two new columns, first_name and last_name, to the table employee. Both columns should have a data type of varchar(50).

For example:

Test	Result
pragma table_info('employee');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           salary      number      0                       0
2           first_name  varchar(50  0                       0
3           last_name   varchar(50  0                       0


```sql
-- ALTER TABLE employee
ADD COLUMN first_name varchar(50);

ALTER TABLE employee
ADD COLUMN last_name varchar(50);
```

**Output:**

<img width="1315" height="338" alt="image" src="https://github.com/user-attachments/assets/9520fbbc-79f2-44dc-893a-629580c96fac" />


**Question 6**
---
-- Insert the following customers into the Customers table:

CustomerID  Name         Address     City        ZipCode
----------  -----------  ----------  ----------  ----------
302         Laura Croft  456 Elm St  Seattle     98101
303         Bruce Wayne  789 Oak St  Gotham      10001
For example:

Test	Result
SELECT * FROM Customers;

CustomerID  Name         Address     City        ZipCode
----------  -----------  ----------  ----------  ----------
302         Laura Croft  456 Elm St  Seattle     98101
303         Bruce Wayne  789 Oak St  Gotham      10001

```sql
-- INSERT INTO Customers (CustomerID, Name, Address, City, ZipCode)
VALUES
(302, 'Laura Croft', '456 Elm St', 'Seattle', 98101),
(303, 'Bruce Wayne', '789 Oak St', 'Gotham', 10001);
```

**Output:**
L<img width="1286" height="362" alt="image" src="https://github.com/user-attachments/assets/f95fb1c3-59b3-4cce-9f9e-317a2c13d6a6" />


**Question 7**
---
--Create a new table named products with the following specifications:
product_id as INTEGER and primary key.
product_name as TEXT and not NULL.
list_price as DECIMAL (10, 2) and not NULL.
discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
A CHECK constraint at the table level to ensure:
list_price is greater than or equal to discount
discount is greater than or equal to 0
list_price is greater than or equal to 0
For example:

Test	Result
INSERT INTO products (product_id, product_name, list_price) VALUES (2, 'Product B', 50.00);
SELECT * FROM products;
product_id  product_name  list_price  discount
----------  ------------  ----------  ----------
2           Product B     50          0


```sql
-- CREATE TABLE products (
    product_id INTEGER PRIMARY KEY,
    product_name TEXT NOT NULL,
    list_price DECIMAL(10, 2) NOT NULL,
    discount DECIMAL(10, 2) NOT NULL DEFAULT 0,
    CHECK (
        list_price >= discount
        AND discount >= 0
        AND list_price >= 0
    )
);
```

**Output:**

<img width="1299" height="285" alt="image" src="https://github.com/user-attachments/assets/b9c7fa9e-5c9e-4da8-ad6c-62a390b589e2" />


**Question 8**
---
-- Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.

```sql
-- CREATE TABLE item (
    item_id TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate INTEGER NOT NULL,
    icom_id TEXT(4),
    FOREIGN KEY (icom_id)
        REFERENCES company(com_id)
        ON UPDATE SET NULL
        ON DELETE SET NULL
);
```

**Output:**

<img width="1302" height="340" alt="image" src="https://github.com/user-attachments/assets/2cfd4165-927b-40db-92f8-ab2614a123df" />


**Question 9**
---
-- Write a SQL query to Add a new column mobilenumber as number in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
For example:

Test	Result
pragma table_info('Student_details');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      int         0                       1
1           Name        VARCHAR(10  1                       0
2           Gender      TEXT        1                       0
3           Subject     VARCHAR(30  0                       0
4           MARKS       INT (3)     0                       0
5           mobilenumb  number      0                       0


```sql
--
ALTER TABLE Student_details
ADD COLUMN mobilenumber number;
```

**Output:**

<img width="1293" height="370" alt="image" src="https://github.com/user-attachments/assets/489b29c1-707e-4f66-9298-9b7a985b33a2" />


**Question 10**
---
-- Insert the below data into the Books table, allowing the Publisher and Year columns to take their default values.

ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

Note: The Publisher and Year columns will use their default values.
 
 
For example:

Test	Result
SELECT ISBN, Title, Author
FROM Books 


ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

```sql
--
INSERT INTO Books (ISBN, Title, Author)
VALUES ('978-6655443321', 'Big Data Analytics', 'Karen Adams');
```

**Output:**

<img width="1288" height="315" alt="image" src="https://github.com/user-attachments/assets/3b1006af-1d0a-4eb0-9574-305e98b1d3d3" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
