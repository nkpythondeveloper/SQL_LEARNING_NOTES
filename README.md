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

