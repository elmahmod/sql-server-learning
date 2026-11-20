# What Is SQL?

## 1. Introduction

**SQL** stands for **Structured Query Language**. It is a language used to communicate with and work with relational database management systems (RDBMSs).

SQL is commonly pronounced either **“S-Q-L”** (letter by letter) or **“sequel.”**

With SQL, we can access, retrieve, insert, update, delete, and organize data. We can also define database objects and manage certain permissions.

Examples of database management systems that support SQL or a SQL dialect include:

- Microsoft SQL Server
- Oracle Database
- MySQL
- Sybase / SAP Adaptive Server Enterprise
- Microsoft Access
- Ingres

> **Important distinction:** SQL is the **language**; SQL Server is a **database management system**; and SQL Server Management Studio (SSMS) is a **tool** for connecting to and working with SQL Server.

## 2. Why Use SQL Instead of Searching a File Manually?

Imagine a file containing employee records. To find all female employees, a program might need to read the file and use code and loops to check each record.

A relational database lets us express the request directly with a SQL query:

```sql
SELECT *
FROM Employees
WHERE Gender = 'F';
```

- `SELECT *` — return all columns.
- `FROM Employees` — read from the `Employees` table.
- `WHERE Gender = 'F'` — return only employees whose gender value is `F`.

This is **simpler to express** and allows the DBMS to choose how to execute the query efficiently.

> **Clarification:** SQL queries are not automatically faster than every file-based program. Performance depends on indexing, database design, query design, and data size.

## 3. What Can You Do with SQL?

SQL can be used to:

1. Execute queries against a database.
2. Retrieve data from tables.
3. Insert new records.
4. Update existing records.
5. Delete records.
6. Create and delete databases.
7. Create and modify tables.
8. Create views and stored procedures.
9. Set or revoke permissions on database objects.

## 4. Examples of SQL Statements

The following examples use an `Employees` table.

### 4.1 Retrieve employees earning less than 1,000

```sql
SELECT *
FROM Employees
WHERE Salary < 1000;
```

### 4.2 Retrieve first and last names of male employees earning less than 1,000

```sql
SELECT FirstName, LastName
FROM Employees
WHERE Salary < 1000 AND Gender = 'M';
```

### 4.3 Retrieve employees with salaries between 500 and 1,000

```sql
SELECT *
FROM Employees
WHERE Salary BETWEEN 500 AND 1000;
```

`BETWEEN` includes **both** 500 and 1,000.

### 4.4 Count employees

```sql
SELECT COUNT(*)
FROM Employees;
```

### 4.5 Calculate the total salary

```sql
SELECT SUM(Salary)
FROM Employees;
```

### 4.6 Calculate the average salary

```sql
SELECT AVG(Salary)
FROM Employees;
```

`SUM` and `AVG` ignore `NULL` salary values. If `Salary` has an integer data type in SQL Server, consider converting it to a decimal type when you want a fractional average.

### 4.7 Delete a specific employee

```sql
DELETE FROM Employees
WHERE ID = 10;
```

### 4.8 Update a specific employee's first name

```sql
UPDATE Employees
SET FirstName = 'Amjad'
WHERE ID = 10;
```

> **Safety reminder:** Always check the `WHERE` condition before running `UPDATE` or `DELETE`. Without a `WHERE` clause, these statements may affect **all rows** in the table.

## 5. Creating Database Objects

### Create a database

```sql
CREATE DATABASE MyDatabase;
```

### Delete a database

```sql
DROP DATABASE MyDatabase;
```

**Warning:** `DROP DATABASE` removes the database. Do not run it against a database containing data you need.

### Create a table

```sql
CREATE TABLE Employees
(
    ID INT,
    FirstName VARCHAR(255),
    LastName VARCHAR(255),
    Address VARCHAR(255),
    City VARCHAR(255)
);
```

This creates an `Employees` table with five columns. Constraints such as `PRIMARY KEY` or `NOT NULL` can be added as needed; the slide's example focuses on the basic syntax.

## 6. Types of SQL Statements

The lesson groups SQL statements into five commonly taught categories:

| Category | Full name | Main purpose | Examples |
|---|---|---|---|
| **DDL** | Data Definition Language | Define or change database structures | `CREATE`, `DROP`, `ALTER`, `TRUNCATE` |
| **DML** | Data Manipulation Language | Add or modify table records | `INSERT`, `UPDATE`, `DELETE` |
| **DCL** | Data Control Language | Control access and permissions | `GRANT`, `REVOKE` |
| **TCL** | Transaction Control Language | Control database transactions | `COMMIT`, `ROLLBACK`, `SAVEPOINT` |
| **DQL** | Data Query Language | Retrieve data | `SELECT` |

### DDL — Data Definition Language

Used for database structures:

- `CREATE` — create a database object.
- `DROP` — remove a database object.
- `ALTER` — modify an existing object.
- `TRUNCATE` — remove all rows from a table while keeping its structure (subject to restrictions).

### DML — Data Manipulation Language

Used for table records:

- `INSERT` — add records.
- `UPDATE` — change existing records.
- `DELETE` — remove records.

### DCL — Data Control Language

Used for permissions:

- `GRANT` — grant permission.
- `REVOKE` — revoke permission.

### TCL — Transaction Control Language

Used to manage transactions:

- `COMMIT` — save the changes of a transaction.
- `ROLLBACK` — undo changes in a transaction, subject to its state.
- `SAVEPOINT` — mark a point within a transaction for partial rollback (the name and syntax depend on the DBMS).

### DQL — Data Query Language

Used for retrieving data:

- `SELECT` — query records from one or more tables.

> **Notes for Microsoft SQL Server:** This five-category grouping is useful for learning, but classifications vary among textbooks. In SQL Server, a transaction savepoint is written with `SAVE TRANSACTION`, rather than the standalone `SAVEPOINT` statement used by some other database systems. SQL Server's version of SQL is called **T-SQL (Transact-SQL)**.

## 7. Quick Review

| Term | Meaning |
|---|---|
| **SQL** | Structured Query Language |
| **Query** | A request sent to a database, often to retrieve or change data |
| **Statement** | An SQL instruction such as `SELECT` or `CREATE` |
| **Retrieve** | Get data from the database |
| **Manipulate** | Insert, update, or delete data |
| **DDL** | Database structure commands |
| **DML** | Data-changing commands |
| **DCL** | Permission-control commands |
| **TCL** | Transaction-control commands |
| **DQL** | Data-retrieval commands |

**Key takeaway:** SQL lets us describe **what data we want** or **what database operation we want performed**. The database management system processes the SQL statement and carries out the request.

---

*Study notes based on the course slides: “What Is SQL?”*
