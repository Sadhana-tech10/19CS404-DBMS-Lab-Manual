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
write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
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
```sql
select s.name as Salesman,c.cust_name,c.city from salesman s
join customer c on s.city=c.city
```

**Output:**
<img width="1137" height="780" alt="image" src="https://github.com/user-attachments/assets/9b39be9b-b47c-40dc-b55d-72410651f085" />


**Question 2**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the city 'London'.
```sql
select s.name from salesman AS s left join
customer on s.salesman_id=customer.salesman_id where customer.city='London'
```

**Output:**

<img width="481" height="552" alt="image" src="https://github.com/user-attachments/assets/e9b4249f-b081-49e0-91a7-85143af77c64" />

**Question 3**
---
Write the SQL query that achieves the selection of all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.
```sql
select t.* from TEST_RESULTS as t
inner join patients as p on t.patient_id=p.patient_id
where p.first_name='Alice'
```

**Output:**

<img width="1222" height="490" alt="image" src="https://github.com/user-attachments/assets/47451570-3447-42eb-a548-40e5185151a8" />

**Question 4**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.

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
Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
```sql
SELECT o.ord_no,o.purch_amt,c.cust_name,c.city from orders o
join customer c on o.customer_id=c.customer_id where o.purch_amt between 500 and 2000;
```

**Output:**

<img width="1217" height="565" alt="image" src="https://github.com/user-attachments/assets/2317185b-73c0-46c8-8818-2d12fa53bc3c" />

**Question 5**
---
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for test results with a test date between '2024-03-01' and '2024-03-31'.
```sql
select p.* from patients as p inner join TEST_RESULTS as t on p.patient_id=t.patient_id
where t.test_date  between '2024-03-01' and '2024-03-31'
```

**Output:**

<img width="1202" height="502" alt="image" src="https://github.com/user-attachments/assets/e73d898e-9040-4af8-96fa-3a14760742d3" />

**Question 6**
---
Write the SQL query that achieves the selection of all columns from the "patients" table and the specialization from the "doctors" table (aliased as "doctor_specialization"), with an inner join on the "doctor_id" column.

PATIENTS TABLE:
name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

DOCTORS TABLE:

name             type
---------------  ---------------
doctor_id        INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
specialization   VARCHAR(100)
```sql
select p.*,d.specialization as doctor_specialization from patients p 
inner join doctors d on p.doctor_id=d.doctor_id
```

**Output:**
<img width="1221" height="632" alt="image" src="https://github.com/user-attachments/assets/fdff4497-b8eb-43cb-9c66-0e9325b25f82" />

**Question 7**
---
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with an order date between '2012-08-01' and '2012-08-30'.
```sql
select c.* from customer c left join orders o on c.customer_id=o.customer_id
where o.ord_date between '2012-08-01' and '2012-08-30'
```

**Output:**

<img width="1223" height="560" alt="image" src="https://github.com/user-attachments/assets/faf8eb68-15aa-4ab4-b6fa-9b6325183195" />

**Question 8**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for patients admitted between '2024-01-01' and '2024-01-31'.
```sql
select p.first_name as patient_name,t.* from PATIENTS p  
inner join TEST_RESULTS t on p.patient_id=t.patient_id
where p.admission_date between '2024-01-01' and '2024-01-31'
```

**Output:**

<img width="1238" height="498" alt="image" src="https://github.com/user-attachments/assets/baedcfb7-416a-40b8-8f27-37bb9d03e274" />

**Question 9**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with a purchase amount less than 100.
```sql
select c.cust_name from customer c
left join orders o on c.customer_id=o.customer_id where o.purch_amt<100;
```

**Output:**

<img width="508" height="552" alt="image" src="https://github.com/user-attachments/assets/9e192c24-383c-47c5-85a5-9ef66f4e581c" />

**Question 10**
---
Write the SQL query that accomplishes the selection of the first name and last name from the "patients" table, with an inner join on the "patient_id" column and a condition filtering for surgeries with a surgery date between '2024-01-01' and '2024-01-31'.

PATIENTS TABLE:

name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

SURGERIES TABLE:

name             type
---------------  ---------------
surgery_id       INT
patient_id       INT
surgeon_id       INT
surgery_date     DATE
```sql
select p.first_name,p.last_name from patients p inner join surgeries s on p.patient_id = s.patient_id
where s.surgery_date  between '2024-01-01' and '2024-01-31';
```

**Output:**

<img width="760" height="457" alt="image" src="https://github.com/user-attachments/assets/50154ce1-2a77-4822-818f-78bd2bfc50b9" />


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
