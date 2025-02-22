# SQL LEARNING NOTES

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

``

4. **SELECT** - Retrieves data from table.

```sql

SELECT * FROM Employees;

```

----

## KEY DIFFERENCES BETWEEN DDL & DML

| Feature | DDL (Data Definition Language) | DML (Data Manipulation Language) |
| --------| -------------------------------| ---------------------------------|
| Purpose | Defines and manages, database structure | Modifies and manages data in tables. |
| Commands | CREATE, ALTER, DROP, TRUNCATE, RENAME | INSERT, UPDATE, DELETE, SELECT |
| Transaction Control | Auto-Commited (Changes are permament) | Can be rolled back (ROLLBACK) |

