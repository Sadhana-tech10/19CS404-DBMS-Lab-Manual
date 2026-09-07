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
Write a SQL query to find Who has the highest income among employee living in California?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
For example:

Result
name        max(income)
----------  -----------
Adam        5000000

```sql
select name,MAX(income) as 'max(income)' from employee where city='California' order by MAX(income) desc 
limit 1;
```

**Output:**
<img width="632" height="387" alt="image" src="https://github.com/user-attachments/assets/4a5cc13e-9314-49a5-887a-629be24cff8b" />


**Question 2**
---
Write a SQL query to find the number of employees who are having the same age removing the duplicate values.

Sample table: employee

id

name

age

address

salary

1

Paul

32

California

20000

4

Mark

25

Richtown

65000

5

David

27

Texas

85000

 

For example:

Result
COUNT
----------
4

```sql
select count(distinct age) as COUNT from employee
```

**Output:**

<img width="457" height="383" alt="image" src="https://github.com/user-attachments/assets/2c1c198d-3758-4889-87c9-37048b67c91d" />

**Question 3**
---
Write a SQL query that counts the number of unique salespeople. Return number of salespeople.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001
```sql
select count(distinct salesman_id) as COUNT from orders;
```

**Output:**

<img width="456" height="406" alt="image" src="https://github.com/user-attachments/assets/f74f9457-4d00-4eeb-b1d5-96da7136e1cb" />

**Question 4**
---
How many medical records are there for each patient?

Sample table:MedicalRecords Table



For example:

Result
PatientID   TotalRecords
----------  ------------
4           4
5           1
6           1
7           1
8           1
10          2

```sql
select PatientID,count(*) as TotalRecords
from MedicalRecords
group by PatientID;
```

**Output:**
<img width="676" height="723" alt="image" src="https://github.com/user-attachments/assets/c1ba3d0d-3c20-4067-ba57-81d984279c39" />


**Question 5**
---
What is the total number of medications prescribed for each patient?

Sample tablePrescriptions Table



For example:

Result
PatientID   TotalMedications
----------  ----------------
1           1
2           1
3           1
4           1
5           1
6           1
7           1
8           1
9           1
10          1

```sql
select PatientID,count(*) as TotalMedications
from Prescriptions
group by PatientID;
```

**Output:**
<img width="737" height="832" alt="image" src="https://github.com/user-attachments/assets/87b0f24a-9e5a-4dae-997f-0d722cf32d5d" />


**Question 6**
---
What is the most common diagnosis among patients?

Sample table:MedicalRecords Table



For example:

Result
Diagnosis              DiagnosisCount
---------------------  --------------
Childhood vaccination  3

```sql
select diagnosis,count(*) as DiagnosisCount
from MedicalRecords
group by Diagnosis
order by count(*) desc
limit 1;
```

**Output:**

<img width="982" height="380" alt="image" src="https://github.com/user-attachments/assets/9088cce7-38bc-4c03-893f-2aeea7215c6c" />

**Question 7**
---
Write the SQL query that accomplishes the selection of average price for each category from the "products" table and includes only those products where the average price falls between 10 and 15.

Sample table: products


```sql
select category_id,avg(price) as 'AVG(Price)' from products
group by category_id
Having avg(price) between 10 and 15;
```

**Output:**
<img width="660" height="402" alt="image" src="https://github.com/user-attachments/assets/7cae56a2-1648-41ac-8b24-3c1b53fdc608" />


**Question 8**
---
Write the SQL query that performs grouping by age groups and displays the maximum salary for each group, excluding groups where the maximum salary is not greater than 8000. 

Note: Calculate the age group as multiples of 5.

Eg., 20,22,23 comes in age group 20. 

25,27,29 comes in age group 25.

Sample table: customer1


```sql
select (age/5)*5 as age_group,max(salary) as 'MAX(salary)'
from customer1
group by (age/5)*5
having max(salary) > 8000;
```

**Output:**
<img width="672" height="455" alt="image" src="https://github.com/user-attachments/assets/d1ff5f58-c345-4df8-a163-7aaacaaebe9a" />


**Question 9**
---
Write the SQL query that achieves the grouping of data by occupation, calculates the total work hours for each occupation, and excludes occupations where the total work hour sum is not greater than 20.

Sample table: employee1



For example:

Result
occupation  SUM(workhour)
----------  -------------
Business    30
Doctor      30
Engineer    24
Teacher     27

```sql
select occupation,sum(workhour) as 'SUM(workhour)' from employee1 group by occupation
having sum(workhour)>20;
```

**Output:**
<img width="632" height="535" alt="image" src="https://github.com/user-attachments/assets/a9497af3-2e1a-409d-9a58-24bd1239691f" />


**Question 10**
---
Write the SQL query that achieves the grouping of data by age groups, displays the minimum salary for each group, and excludes groups where the minimum salary is not less than 2000.

Sample table: customer1
```sql
select (age/5)*5 as age_group,min(salary) as 'MIN(salary)' from customer1
group by (age/5)*5
having min(salary) < 2000;
```

**Output:**
<img width="615" height="420" alt="image" src="https://github.com/user-attachments/assets/b210bf05-5544-4e4f-97a5-f3663b469745" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
