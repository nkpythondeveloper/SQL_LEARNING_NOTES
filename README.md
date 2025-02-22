# SQL_LEARNING_NOTES

# SQL LEARNING NOTES

## DDL - DATA DEFINITION LANGUAGE

DDL refers to SQL commands that ***define*** and ***manage*** the database structure.
These commands are used to create, modify and delete database objects like tables, indexes, and schemas.

**Examples of common DDL Commands**:

1. CREATE - Creates database objects (tables, views, indexes)

```sql

CREATE TABLE Employees (
	id INT PRIMARY KEY,
	name VARCHAR(50),
	salary DECIMAL(10,2)
);

```

2. ALTER - Modifies existing database objects

```sql

ALTER TABLE Employees ADD COLUMN department VARCHAR(50);

```

3. DROP - Deletes database objects.

```sql

DROP TABLE Employees;

```

4. TRUNCATE - Deletes all rows from the table, but keeps the table structure.

```sql

TRUNCATE TABLE Employees;

```

5. RENAME - Changes the name of the existing database object.

```sql

RENAME TABLE Employees TO Staff;

```

------



