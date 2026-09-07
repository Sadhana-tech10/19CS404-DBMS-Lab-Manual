# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is LESS than $2500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000
```sql
select *from CUSTOMERS WHERE SALARY < 2500;
```

**Output:**
<img width="1231" height="533" alt="image" src="https://github.com/user-attachments/assets/f0d2d28f-a4cd-4bf6-a6b5-207db8eb76f1" />


**Question 2**
---
Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
```sql
SELECT name,city from customer where city in (select city from customer where id in (3,7));
```

**Output:**

<img width="605" height="552" alt="image" src="https://github.com/user-attachments/assets/4665a7be-2582-4fd7-a44b-d64012558b89" />

**Question 3**
---
Write a query to display all the customers whose ID is the difference between the salesperson ID of Mc Lyon and 2001.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

customer table

name         type
-----------  ----------
customer_id  int
cust_name    text
city         text
grade        int
salesman_id  int
 
```sql
select *from customer where customer_id=(select salesman_id-2001 from salesman where name = 'Mc Lyon');
```

**Output:**

<img width="1211" height="402" alt="image" src="https://github.com/user-attachments/assets/9fd5a6c8-3233-414f-ad3b-509759151640" />

**Question 4**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose AGE is LESS than $30

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000
```sql
select *from CUSTOMERS WHERE AGE < 30;
```

**Output:**
<img width="1223" height="640" alt="image" src="https://github.com/user-attachments/assets/d7397e05-342d-4796-8a93-b5261015961a" />

**Question 5**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is EQUAL TO $1500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000
```sql
SELECT *FROM CUSTOMERS WHERE SALARY=1500;
```

**Output:**

<img width="1216" height="457" alt="image" src="https://github.com/user-attachments/assets/dd6fd9fe-9591-4f05-8c7f-361b9f43a93c" />


**Question 6**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $4500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000
```sql
SELECT *FROM CUSTOMERS WHERE SALARY > 4500;
```

**Output:**
<img width="1287" height="497" alt="image" src="https://github.com/user-attachments/assets/cd3da581-1ab3-4c10-a42d-8c07e3248815" />

**Question 7**
---
Write a SQL query to Retrieve the medications with dosages equal to the lowest dosage

Medications Table



For example:

Result
medic  medication_name  dosage
-----  ---------------  ---------------
2      Ibuprofen        200mg

```sql
SELECT *FROM Medications WHERE dosage = (select min(dosage) from Medications)
```

**Output:**
<img width="886" height="467" alt="image" src="https://github.com/user-attachments/assets/94427ef2-fd1f-4374-97fd-e46c92a8e72a" />


**Question 8**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES



```sql
select student_name,grade from GRADES g where grade=(select max(grade)
from GRADES where subject=g.subject)
```

**Output:**
<img width="777" height="516" alt="image" src="https://github.com/user-attachments/assets/85971a23-7d14-41d9-9c81-faca8ef24e27" />


**Question 9**
---
Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
```sql
select *from customer where city != (select city from customer where id=(select max(id) from customer));
```

**Output:**
<img width="1225" height="585" alt="image" src="https://github.com/user-attachments/assets/5e81d276-811a-446d-b48d-06220c912dbd" />


**Question 10**
---
Write a SQL query to Retrieve the medications with dosages equal to the highest dosage

Medications Table


```sql
select *from Medications where dosage= (select max(dosage) from Medications);
```

**Output:**

<img width="922" height="496" alt="image" src="https://github.com/user-attachments/assets/c4e68394-8a01-470f-ac98-f3607ce1e461" />


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
