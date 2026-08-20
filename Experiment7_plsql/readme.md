# Experiment 7: PL/SQL – Variables, Control Structures and Loops

## AIM
To write and execute simple PL/SQL programs using variables, loops, and conditional statements.


## THEORY

PL/SQL, which stands for Procedural Language extensions to the Structured Query Language (SQL). It is a combination of SQL along with the procedural features of programming languages.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:
- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

# PL/SQL Programs – Steps and Expected Output

## 1. Write a PL/SQL program to find the Greatest of Two Numbers

### Steps:
- Declare two numeric variables and initialize them.
- Use an `IF` statement to compare the values.
- Display the greater number using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Greater number is: 80

## PROGRAM:
```
DECLARE
    num1 NUMBER := 60;
    num2 NUMBER := 80;
BEGIN
    IF num1 > num2 THEN
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num1);
    ELSE
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num2);
    END IF;
END;
/
```

## OUTPUT:
<img width="698" height="305" alt="image" src="https://github.com/user-attachments/assets/b19b0fa0-9cc7-4338-b747-546e9ae90cb1" />


---

## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Sum of first 10 natural numbers is: 55

## PROGRAM:
```
DECLARE
    n NUMBER := 10;
    sum NUMBER := 0;
    i NUMBER := 1;
BEGIN
    WHILE i <= n LOOP
        sum := sum + i;
        i := i + 1;
    END LOOP;

    DBMS_OUTPUT.PUT_LINE('Sum of first ' || n || ' natural numbers is: ' || sum);
END;
/
```

## OUTPUT:
<img width="697" height="305" alt="image" src="https://github.com/user-attachments/assets/b4ff8807-9ab9-40a0-b3d2-ec69d3e9ee47" />

---

## 3. Write a PL/SQL program to generate Fibonacci series

### Steps:
- Declare the variable `n` to indicate how many terms to generate.
- Initialize the first two Fibonacci numbers (0 and 1).
- Use a loop to generate the next terms using the formula `c = a + b`.
- Print each term in the series.

**Expected Output:**  
n = 7  
Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8
## PROGRAM:

```
DECLARE
    n NUMBER := 7;
    a NUMBER := 0;
    b NUMBER := 1;
    c NUMBER;
BEGIN
    DBMS_OUTPUT.PUT('Fibonacci sequence: ');
    FOR i IN 1..n LOOP
        DBMS_OUTPUT.PUT(a || ' ');
        c := a + b;
        a := b;
        b := c;
    END LOOP;
    DBMS_OUTPUT.NEW_LINE;
END;
/
```

## OUTPUT:
<img width="703" height="287" alt="image" src="https://github.com/user-attachments/assets/82fab98e-0c79-4e80-a0b5-5f20c9a92e28" />

---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.

**Expected Output:**  
n = 1535  
Reversed number is 5351


## PROGRAM:
```
DECLARE
    n NUMBER := 7;
    a NUMBER := 0;
    b NUMBER := 1;
    c NUMBER;
BEGIN
    DBMS_OUTPUT.PUT('Fibonacci sequence: ');
    FOR i IN 1..n LOOP
        DBMS_OUTPUT.PUT(a || ' ');
        c := a + b;
        a := b;
        b := c;
    END LOOP;
    DBMS_OUTPUT.NEW_LINE;
END;
/
```
## OUTPUT:
<img width="701" height="284" alt="image" src="https://github.com/user-attachments/assets/85a14d2b-0d2e-4f27-88d6-3933f8d0c81a" />

---

## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.

**Expected Output:**  
a = 10, b = 9, c = 15  
Largest of three number is 15

## PROGRAM:
```
DECLARE
    a NUMBER := 10;
    b NUMBER := 9;
    c NUMBER := 15;
    largest NUMBER;
BEGIN
    IF a > b AND a > c THEN
        largest := a;
    ELSIF b > a AND b > c THEN
        largest := b;
    ELSE
        largest := c;
    END IF;

    DBMS_OUTPUT.PUT_LINE('Largest of three numbers is: ' || largest);
END;
/
```

## OUTPUT:
<img width="686" height="255" alt="image" src="https://github.com/user-attachments/assets/c8821ac9-5cf6-4434-a0e5-c8b67a18afa4" />



## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.

