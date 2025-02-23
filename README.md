# SQL LEARNING NOTES - MySQL Oriented


## DDL - DATA DEFINITION LANGUAGE

DDL refers to SQL commands that ***define*** and ***manage*** the database structure.
These commands are used to create, modify and delete database objects like tables, indexes, and schemas.

**Examples of common DDL Commands**:

1. **CREATE** - Creates database objects (tables, views, indexes)

```sql

CREATE TABLE Employees (
	id INT PRIMARY KEY,
	name VARCHAR(50),
	salary DECIMAL(10,2)
);

```

2. **ALTER** - Modifies existing database objects

```sql

ALTER TABLE Employees ADD COLUMN department VARCHAR(50);

```

3. **DROP** - Deletes database objects.

```sql

DROP TABLE Employees;

```

4. **TRUNCATE** - Deletes all rows from the table, but keeps the table structure.

```sql

TRUNCATE TABLE Employees;

```

5. **RENAME** - Changes the name of the existing database object.

```sql

RENAME TABLE Employees TO Staff;

```

------


## DML - DATA MANIPULATION LANGUAGE

DML commands deal with the manipulation of data stored in the database tables.
These commands allow you to insert, update, retrieve, and delete records.

**Common DML Commands**:

1. **INSERT** - Adds new record to a table.

```sql

INSERT INTO Employees (id, name, salary) VALUES (1, "John Doe", 50000);

```

2. **UPDATE** - Modifies existing records.

```sql

UPDATE Employees SET salary = 55000 WHERE id = 1;

```

3. **DELETE** - Removes records from a table.

```sql

DELETE FROM Employees WHERE id = 1;

```

4. **SELECT** - Retrieves data from table.

```sql

SELECT * FROM Employees;

```

----

### KEY DIFFERENCES BETWEEN DDL & DML

| Feature | DDL (Data Definition Language) | DML (Data Manipulation Language) |
| --------| -------------------------------| ---------------------------------|
| Purpose | Defines and manages, database structure | Modifies and manages data in tables. |
| Commands | CREATE, ALTER, DROP, TRUNCATE, RENAME | INSERT, UPDATE, DELETE, SELECT |
| Transaction Control | Auto-Commited (Changes are permament) | Can be rolled back (ROLLBACK) |

----

## CLAUSES

Clauses in SQL are built-in keywords used to filter, sort, and limit data retrievel in SELECT statements.
They modify the query results, without modifiying the data.


**Common SQL Clauses**

1. **WHERE** - Filters records based on the condition.

	- Used with **SELECT**, **UPDATE**, **DELETE**
	- Returns only records that match the condition.

```sql

SELECT * FROM Employees WHERE salary > 50000;

```

2. **ORDER BY** - Sorts the result set.

	- Default sorting is **ASC**(Ascending). Use **DESC** (Decending) for reverse order.

```sql

SELECT * FROM Employees ORDER BY salary DESC;

```

3. **GROUP BY** - Groups rows that have same value in specified column.

	- Used with aggregate functions (SUM(), COUNT(), AVG(), etc)

```sql

SELECT department, COUNT(*) AS total_employees FROM Employees GROUP BY department;

```

4. **HAVING** - Filters grouped records.

	- Similar to WHERE, but works with aggregates.

```sql

SELECT department, AVG(salary) AS average_salary
FROM Employees
GROUP BY department
HAVING AVG(salary) > 60000;

```

5. **LIMIT** - Restricts the number of records retured.

```sql

SELECT * FROM Employees LIMIT 5;

```

6. **OFFSET** - Skips the number of records.

	- Used with LIMIT for pagination.

```sql

SELECT * FROM Employees LIMIT 5 OFFSET 10; -- Skips first 10 rows, and fetches next 5 rows.

```

7. **JOIN** - Combines rows from multiple tables.

	- Types:
		1. INNER JOIN
		2. LEFT JOIN/ LEFT OUTER
		3. RIGHT JOIN/ RIGHT OUTER
		4. FULL JOIN / FULL OUTER

```sql

SELECT Employees.name, Departments.department_name
from Employees
INNER JOIN Depratments ON Employees.department_id = Departments.department_id;

```

![JOIN TYPES](https://github.com/nkpythondeveloper/SQL_LEARNING_NOTES/blob/main/joins-venn.png)


8. **DISTINCT** - Removes duplicate values.

```sql

SELECT DISTINCT department FROM Employees;

``` 

9. **IN** - Filter values in a list.

```sql

SELECT * FROM Employees WHERE department IN ["HR", "IT", "Finance"];

```

10. **BETWEEN** - Filters within a list.

```sql

SELECT * FROM Employees WHERE salary BETWEEN 50000 AND 80000;

```

11. **LIKE** - Matches patterns in text (used with wildcards %, _)

```sql

SELECT * FROM Employees WHERE name LIKE '%J';

```

----

### DIFFERENCE BETWEEN "WHERE" & "HAVING"

| Feature | WHERE | HAVING |
|---------|-------|--------|
| Used for | Filter rows before grouping | Filter groups after aggregation |
| Works with | Columns and expressions | Aggregate functions (SUM(), AVG(), etc) |



**Example of using multiple clauses together**:

```sql

SELECT department, AVG(salary) AS average_salary
FROM Employees
WHERE salary > 30000
GROUP BY department
HAVING AVG(salary) > 50000
ORDER BY average_salary DESC
LIMIT 3;

```

----

## SQL OPERATORS

SQL Operators are special symbols or keywords used in queries to perform operations on data.
They help filter, compare, and manipulate values in SQL Queries.

### Types of SQL Operators

1. **ARTIHMETIC OPERATORS**

	Used to perform mathematical operations.

	| Operator | Description | Example |
	|----------|-------------|---------|
	| + | Addition | SELECT 10 + 5; |
	| - | Substraction | SELECT 10 - 5; |
	| * | Multiplication | SELECT 10 * 5; |
	| / | Division | SELECT 10 / 5; |
	| % | Modulus | SELECT 10 % 3; |

----

2. **COMPARISION OPERATORS** 

	Used for filtering data in WHERE clauses.

	| Operator | Description | Example |
	|----------|-------------|---------|
	| = | Equal to | SELECT * FROM Employees WHERE salary = 50000; |
	| != | Not equal to | SELECT * FROM Employees WHERE salary != 50000; |
	| > | Greater than | SELECT * FROM Employees WHERE salary > 40000; |
	| < | Less than | SELECT * FROM Employees WHERE salary < 50000; |
	| >= | Greater than equal to | SELECT * FROM Employees WHERE salary >= 45000; |
	| <= | Less than equal to | SELECT * FROM Employees WHERE salary <= 40000; |
	| BETWEEN | Within a range | SELECT * FROM Employees WHERE salary BETWEEN 30000 AND 50000; |
	| IN | Matches any within a given list | SELECT * FROM Employees WHERE department in ("HR, "IT", "Finance"); |
	| LIKE | Pattern Matching (wildcards %, \_) | SELECT * FROM Employees WHERE name LIKE "S%"; |


---- 

3. **LOGICAL OPERATORS**

	Used to combine conditions in **WHERE** clauses.

	| Operator | Description | Example |
	|----------|-------------|---------|
	| AND | Both conditions should be True | SELECT * FROM Employees WHERE salary > 40000 AND department_id = 1; |
	| OR | At least one condition must be True | SELECT * FROM Employees WHERE salary > 35000 OR department_id in ("HR, "Finances"); |
	| NOT | Negates a condition | SELECT * FROM Employees WHERE NOT department_id = 4; |
	| IS NULL | Checks for NULL values | SELECT * FROM Employees WHERE salary IS NULL; |
	| IS NOT NULL | Checks for non-NULL values | SELECT * FROM Employees WHERE salary IS NOT NULL; |

----

4. **BITWISE OPERATORS**
	
	Used for performing bitwise operations on integers.

	| Operator | Description | Example ( 5= 101, 3 = 011 ) |
	|----------|-------------|-----------------------------|
	| & (AND) | Performs bitwise AND | SELECT 5 & 3; |
	| ` (OR) | Performs bitwise OR | SELECT 5 ` 3; |
	| ^ (XOR) | Performs bitwise XOR | SELECT 5 ^ 3; |
	| ~ (NOT) | Performs bitwise NOT | SELECT ~ 5; |

----

5. **STRING OPERATORS**

	Used for working with string data.

	| Operator | Description | Example |
	|----------|-------------|---------|
	| LIKE | Pattern Matching | SELECT * FROM Employees WHERE name LIKE "J%"; |

----

6. **ASSIGNMENT OPERATOR**

	Used for assigning values to variables in SQL.

	| Operator | Description | Example |
	|----------|-------------|---------|
	| = | Asigns a value | SET @salary = 50000; |

----

7. **SET OPERATORS**

	Used to combine results of multiple queries.

	| Operator | Description | Example |
	|----------|-------------|---------|
	| UNION | Combines results (removes duplicates) | SELECT name FROM Employees UNION SELECT name FROM managers; |
	| UNION ALL | Combines results (keeps duplicates) | SELECT name FROM Employees UNION ALL SELECT name FROM managers; |
	| EXCEPT/MINUS | Returns records from first query, but not in second | SELECT name FROM Employees EXCEPT SELECT name FROM managers; |

----

**Example of using multiple Operators Together**

```sql

SELECT name, salary, department
FROM Employees
WHERE salary BETWEEN (30000 AND 50000)
AND
department IN ("HR", "IT")
ORDER BY salary DESC
LIMIT 5;

```

## SQL JOINS

Joins in SQL are used to combine rows from two or more tables based on a related column.


**Types of Joins**:
	1. INNER JOIN
	2. LEFT JOIN
	3. RIGHT JOIN
	4. FULL JOIN
	5. SELF JOIN
	6. CROSS JOIN



**Employees** 

| emp_id | emp_name | emp_salary | emp_department_id |
|--------|------|--------|---------------|
| 1 | Nitin K | 150000 | IT |
| 2 | Sachin K | 200000 | Management |
| 3 | Swapnil T | 150000 | IT |
| 4 | Ajinkya B | 100000 | IT |
| 5 | Pranay M | 75000 | Operations |
| 6 | Sahil D | 80000 |  Offers |
| 7 | Dipal P | 90000 | Offers |
| 8 | Sudeep A | 80000 | Operations |
| 9 | Maddy S | 65000 | Operations |
| 10 | Amit Y | 55000 | Operations |


**Departments**

| department_id | department_name |
|---------------|-----------------| 
| IT | Information Technology |
| Management | Manage the Company Operation | 
| Operations | Email Operations |
| Offers | Affiliate Management |

----

1. **INNER JOIN**
	
	Returns only matching rows from both the tables.

```sql

SELECT Employees.emp_name, Employees.salary, Departments.department_name
FROM Employees
INNER JOIN Depratments ON Employees.department_id = Departments.department_id;

```

This query will return records from Employees table only who have a matching department_id in Departments Table.


2. **LEFT JOIN**

	Returns all records from Left table, and matching records from the Right table. If no match, NULL is returned.

```sql

SELECT Employees.emp_name, Employees.salary, Departments.department_name
FROM Employees
LEFT JOIN Depratments ON Employees.department_id = Departments.department_id;

```

This query will return all the records from Employees table, and matching records from Departments table.


3. **RIGHT JOIN**

	Returns all records from Right table, and matching records from the Left table. If no match, NULL is returned.

```sql

SELECT Employees.emp_name, Employees.salary, Departments.department_name
FROM Employees
RIGHT JOIN Depratments ON Employees.department_id = Departments.department_id;

```

This query will return all the records from Departments table, and matching records from Employees table.

