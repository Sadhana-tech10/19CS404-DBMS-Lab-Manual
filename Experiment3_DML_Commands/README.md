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
Write a SQL query to calculate the discount amount for each product. Return product_id, original_price, discount_percentage, and discount_amount.

Sample table: Products

product_id | original_price | discount_percentage
------------+----------------+---------------------
101 | 50.00 | 0.10
102 | 75.00 | 0.15
103 | 100.00 | 0.20

For example:

Result
product_id  original_price  discount_percentage  discount_amount
----------  --------------  -------------------  ---------------
101         50.0            0.1                  5.0
102         75.0            0.15                 11.25
103         100.0           0.2                  20.0

```sql
SELECT product_id,original_price,discount_percentage,(original_price* discount_percentage) AS discount_amount
FROM Products;
```

**Output:**
<img width="1238" height="367" alt="image" src="https://github.com/user-attachments/assets/d5c55e5a-9cd3-469a-9f8e-18ed8067457d" />


**Question 2**
---
Write a SQL query to Delete customers from 'customer' table where 'CUST_NAME' contains the substring 'Holmes'.

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
CUST_CODE   CUST_NAME   CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE
----------  ----------  ----------  ------------  ------------  ----------  -----------  -----------  -----------  ---------------  ----------  ----------
C00013      Holmes      London      London        UK            2           6000         5000         7000         4000             BBBBBBB     A003
changes()
----------
1
```sql
DELETE FROM customer
WHERE CUST_NAME LIKE '%Holmes%';
```

**Output:**

<img width="1232" height="633" alt="image" src="https://github.com/user-attachments/assets/0e2e91b1-a1a5-424b-bb26-f164265e2e9d" />

**Question 3**
---
Write a SQL statement to Increase the selling price by 15% in the products table where quantity in stock is less than 50 and supplier ID is 10.

Products Table 

name          type       
----------    ---------- 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lv     INT        
quantity       INT        
supplier_id    INT           
For example:

Test	Result
select changes();
changes()
----------
4

```sql
UPDATE Products
SET sell_price=sell_price*1.15
WHERE quantity < 50  AND supplier_id = 10;
```

**Output:**
<img width="1226" height="570" alt="image" src="https://github.com/user-attachments/assets/f70ea735-e834-4f71-b848-a5538b2e4201" />


**Question 4**
---
Write a SQL query to identify the top 3 most expensive discounted products. Return product_id, original_price, discount_percentage, and discounted_price.

Sample table: Products

product_id | original_price | discount_percentage

 ------------+----------------+--------------------- 

101 | 50.00 | 0.10 

102 | 150.00 | 0.15 

103 | 200.00 | 0.20 

104 | 300.00 | 0.25

 

 

For example:

Result
product_id  original_price  discount_percentage  discounted_price
----------  --------------  -------------------  ----------------
103         100.0           0.2                  80.0
102         75.0            0.15                 63.75
101         50.0            0.1                  45.0
```sql
SELECT product_id,original_price,discount_percentage,(original_price*(1-discount_percentage)) AS discounted_price
From Products
ORDER BY discounted_price DESC
LIMIT 3;
```

**Output:**

<img width="1218" height="367" alt="image" src="https://github.com/user-attachments/assets/a7a925a5-5b32-4f05-91dd-3ebbdce36859" />

**Question 5**
---
Write a SQL query to delete a doctor from Doctors table whose Specialization is 'Pediatrics' and First name is 'Michael'.

Sample table: Doctors

attributes: doctor_id, first_name, last_name, specialization
```sql
DELETE FROM Doctors WHERE specialization = 'Pediatrics' AND first_name ='Michael';
```

**Output:**

<img width="1217" height="447" alt="image" src="https://github.com/user-attachments/assets/a5d46c70-9f33-4ec2-9f88-6c0e28826379" />

**Question 6**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is exactly 2.

 
Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select distinct(grade)from customer;
GRADE
----------
2
3
1
0
GRADE
----------
3
1
0

```sql
DELETE FROM Customer WHERE GRADE = 2;
```

**Output:**

<img width="717" height="656" alt="image" src="https://github.com/user-attachments/assets/b8e64f7a-e16b-41ca-ba2c-1b93967cf63d" />

**Question 7**
---
Write a SQL query to find all employees who were hired in the last 6 months from the emp table. 

Note: Assume current date as '01-09-2024'

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
empno       ename       job         mgr         hiredate    sal         comm        deptno
----------  ----------  ----------  ----------  ----------  ----------  ----------  ----------
7369        SMITH       CLERK       7902        2024-06-01  800                     20
7499        ALLEN       SALESMAN    7698        2024-06-01  1600        300         30
7521        WARD        SALESMAN    7698        2024-06-01  1250        500         30
7900        JAMES       CLERK       7698        2024-06-01  950                     30
7902        FORD        ANALYST     7566        2024-06-01  3000                    20
7934        MILLER      CLERK       7782        2024-06-01  1300                    10
```sql
SELECT *FROM emp WHERE hiredate >= '2024-03-01' AND hiredate <= '2024-09-01';
```

**Output:**

<img width="1225" height="428" alt="image" src="https://github.com/user-attachments/assets/5e9406fd-d2b1-4f3e-8120-205020203a4b" />

**Question 8**
---
Write a SQL query to Delete customers from 'customer' table where 'CUST_NAME' has exactly 6 characters.

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
CUST_CODE   CUST_NAME   CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE
----------  ----------  ----------  ------------  ------------  ----------  -----------  -----------  -----------  ---------------  ----------  ----------
C00013      Holmes      London      London        UK            2           6000         5000         7000         4000             BBBBBBB     A003
C00020      Albert      New York    New York      USA           3           5000         7000         6000         6000             BBBBSBB     A008
C00015      Stuart      London      London        UK            1           6000         8000         3000         11000            GFSGERS     A003
C00012      Steven      San Jose    San Jose      USA           1           5000         7000         9000         3000             KRFYGJK     A012
C00003      Martin      Torento     Torento       Canada        2           8000         7000         7000         8000             MJYURFD     A004
C00009      Ramesh      Mumbai      Mumbai        India         3           8000         7000         3000         12000            Phone No    A002
changes()
----------
6
```sql
DELEte from Customer
Where length(CUST_NAME)=6;
```

**Output:**
<img width="1220" height="813" alt="image" src="https://github.com/user-attachments/assets/ec058ce9-e05a-49a2-9340-d175803f5239" />

**Question 9**
---
Write a SQL statement to Update the reorder level to 20 where the quantity in stock is less than 10 and product category is 'Snacks' in the products table.

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
update products set reorder_lvl = 20 where quantity <10 and category = 'Snacks';
```

**Output:**

<img width="1222" height="656" alt="image" src="https://github.com/user-attachments/assets/edb0aa77-74d6-403a-a54b-daac9872dd43" />

**Question 10**
---
Write a SQL query to classify value2 in the Calculations table as 'Small', 'Medium', or 'Large' based on whether it is less than 10, between 10 and 50, or greater than 50, respectively.

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
id          value2      size_category
----------  ----------  -------------
1           2.0         Small
2           5.0         Small
3           7.0         Small
4           9.0         Small

```sql
select id,value2,
case
when value2<10 then 'Small'
when value2>= 10 and value2<=50 then 'Medium'
when value2>50 then 'Large'
end as size_category
from Calculations;
```

**Output:**

<img width="882" height="562" alt="image" src="https://github.com/user-attachments/assets/6bb5ca68-4c49-40a9-bdfa-0d2204dc7436" />

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
