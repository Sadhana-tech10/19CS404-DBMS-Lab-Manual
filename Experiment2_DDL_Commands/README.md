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
Write a SQL query to Add a new column Mobilenumber as number in the Student_details table.

Sample table: Student_details

 cid              name             type             notnu  dflt_value  pk
---------------  ---------------  ---------------  -----  ----------  ----------
0                RollNo           int              0                  1
1                Name             VARCHAR(100)     1                  0
2                Gender           TEXT             1                  0
3                Subject          VARCHAR(30)      0                  0
4                MARKS            INT (3)          0                  0

```
ALTER TABLE Student_details
ADD Mobilenumber number;
```
**Output:**
<img width="1217" height="409" alt="image" src="https://github.com/user-attachments/assets/809a21d7-1525-41a6-8fa7-053b7f4705a7" />


**Question 2**
Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock

```
INSERT INTO Products(ProductID,ProductName,Price,Stock)
SELECT ProductID,ProductName,Price,Stock
FROM Discontinued_products;
```

**Output:**
<img width="1221" height="349" alt="image" src="https://github.com/user-attachments/assets/2fb14ab4-c32a-43c4-baca-4cf61f9f58db" />

**Question 3**
Write a SQL query to add birth_date attribute as timestamp (datatype) in the table customer 

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
 



```
ALTER TABLE customer
ADD COLUMN birth_date timestamp;
```

**Output:**
<img width="1222" height="438" alt="image" src="https://github.com/user-attachments/assets/198a47be-db0b-4fad-897e-9d2702c9ba3f" />


**Question 4**
Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary



```
INSERT INTO Employee(EmployeeID,Name,Department,Salary)
SELECT EmployeeID,Name,Department,Salary
FROM Former_employees;
```

**Output:**
<img width="1220" height="338" alt="image" src="https://github.com/user-attachments/assets/fdddf334-553f-4544-9db5-c2ae1fb9938c" />

**Question 5**
Insert the following customers into the Customers table:

CustomerID  Name         Address     City        ZipCode
----------  -----------  ----------  ----------  ----------
302         Laura Croft  456 Elm St  Seattle     98101
303         Bruce Wayne  789 Oak St  Gotham      10001

```
INSERT INTO Customers(CustomerID,Name,Address,City,Zipcode)
VALUES
(302,'Laura Croft','456 Elm St','Seattle',98101),
(303,'Bruce Wayne','789 Oak St','Gotham',10001);
```

**Output:**
<img width="1280" height="442" alt="image" src="https://github.com/user-attachments/assets/536c8c67-0165-4d74-a3ba-1c63cee9e05b" />


**Question 6**
Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.
```
CREATE TABLE Employees(
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(50) NOT NULL,
    LastName VARCHAR(50) NOT NULL,
    Email VARCHAR(100) UNIQUE NOT NULL,
    Salary DECIMAL(10,2) CHECK (salary > 0),
    DepartmentID INT NOT NULL,
    FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
);
```
**Output:**
<img width="1214" height="503" alt="image" src="https://github.com/user-attachments/assets/0ba8d14b-457c-43af-bf57-2216e03aacbc" />



**Question 7**
Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.

```
CREATE TABLE Invoices (
    InvoiceID INTEGER PRIMARY KEY,
    InvoiceDate DATE,
    DueDate DATE,
    Amount REAL,
    
    CHECK (DueDate > InvoiceDate),
    CHECK (Amount > 0)
);
```
**Output:**

<img width="1215" height="354" alt="image" src="https://github.com/user-attachments/assets/ddc309a5-16ac-4750-9b2a-9c2f14db9e84" />


**Question 8**
Create a table named Orders with the following columns:

OrderID as INTEGER
OrderDate as TEXT
CustomerID as INTEGER
```
CREATE TABLE Orders(
    OrderID INTEGER ,
    OrderDate TEXT,
    CustomerID INTEGER
);
```

**Output:**
<img width="1227" height="440" alt="image" src="https://github.com/user-attachments/assets/184507f7-e83a-4ad0-8977-697a0b39e745" />

**Question 9**
Create a table named Customers with the following columns:

CustomerID as INTEGER
Name as TEXT
Email as TEXT
JoinDate as DATETIME
```
CREATE TABLE Customers(
    CustomerID INTEGER,
    Name TEXT,
    Email TEXT,
    JoinDate DATETIME
);
```

**Output:**
<img width="1242" height="475" alt="image" src="https://github.com/user-attachments/assets/7e2b82d5-fa25-461f-9656-a28a7abd6032" />


**Question 10**
Create a table named Events with the following columns:

EventID as INTEGER
EventName as TEXT
EventDate as DATE

```
CREATE TABLE Events(
    EventID INTEGER,
    EventName TEXT,
    EventDate DATE
);

```
**Output:**
<img width="1251" height="438" alt="image" src="https://github.com/user-attachments/assets/9cd91459-003d-413d-8c99-18671ea51822" />




## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
