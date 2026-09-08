# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.

**Program:**
```
CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    employee_name VARCHAR2(50)
);

CREATE TABLE employee_log (
    employee_id NUMBER,
    employee_name VARCHAR2(50)
);

CREATE OR REPLACE TRIGGER log_employee_insert
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_log (employee_id, employee_name)
    VALUES (:NEW.employee_id, :NEW.employee_name);
END;
/

INSERT INTO employees
VALUES (101, 'Sowmiya');

SELECT * FROM employee_log;
```

**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.
<img width="932" height="353" alt="image" src="https://github.com/user-attachments/assets/67186f95-5259-4ed6-9b15-5c3d4d42ffb0" />


---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

**Program:**
```
CREATE TABLE sensitive_data (
    id NUMBER PRIMARY KEY,
    data VARCHAR2(100)
);

INSERT INTO sensitive_data
VALUES (1, 'Confidential Information');

CREATE OR REPLACE TRIGGER prevent_delete
BEFORE DELETE ON sensitive_data
FOR EACH ROW
BEGIN
    RAISE_APPLICATION_ERROR(
        -20001,
        'Deletion of sensitive data is not allowed!'
    );
END;
/

-- Try to delete a record
DELETE FROM sensitive_data
WHERE id = 1;
```
**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`
<img width="693" height="306" alt="image" src="https://github.com/user-attachments/assets/6912d175-ef44-4e6d-9e8d-3442c8958a01" />


---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

**Program:**
```
CREATE TABLE products (
    product_id NUMBER PRIMARY KEY,
    product_name VARCHAR2(50),
    price NUMBER,
    last_modified TIMESTAMP
);

INSERT INTO products (product_id, product_name, price)
VALUES (101, 'Laptop', 50000);

CREATE OR REPLACE TRIGGER update_last_modified
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
    :NEW.last_modified := SYSTIMESTAMP;
END;
/

UPDATE products
SET price = 55000
WHERE product_id = 101;

SELECT * FROM products;
```

**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.
<img width="954" height="349" alt="image" src="https://github.com/user-attachments/assets/402cff9d-5707-4e4f-9643-641078ef323e" />

---


## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

**Program:**
```
CREATE TABLE customer_orders (
    order_id NUMBER PRIMARY KEY,
    customer_name VARCHAR2(50),
    amount NUMBER
);

CREATE TABLE audit_log (
    update_count NUMBER
);

INSERT INTO audit_log VALUES (0);

CREATE OR REPLACE TRIGGER count_order_updates
AFTER UPDATE ON customer_orders
FOR EACH ROW
BEGIN
    UPDATE audit_log
    SET update_count = update_count + 1;
END;
/

INSERT INTO customer_orders
VALUES (101, 'Sowmiya', 5000);

UPDATE customer_orders
SET amount = 6000
WHERE order_id = 101;

SELECT * FROM audit_log;
```
**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.
<img width="948" height="356" alt="image" src="https://github.com/user-attachments/assets/3e2c3055-bbee-425a-8aa6-8d3367a99fd7" />


---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

**Program:**
```
CREATE TABLE employ (
    employee_id NUMBER PRIMARY KEY,
    employee_name VARCHAR2(50),
    salary NUMBER
);

CREATE OR REPLACE TRIGGER check_employee_salary
BEFORE INSERT ON employ
FOR EACH ROW
BEGIN
    IF :NEW.salary < 3000 THEN
        RAISE_APPLICATION_ERROR(
            -20001,
            'ERROR: Salary below minimum threshold.'
        );
    END IF;
END;
/

INSERT INTO employ (employee_id, employee_name, salary)
VALUES (101, 'Sowmiya', 2000);
```

**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`
<img width="938" height="356" alt="image" src="https://github.com/user-attachments/assets/eb117331-2b37-4e60-92e9-642bdf270a02" />


## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
