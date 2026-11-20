# What Is a Constraint, and Why Is It Important?

## 1. What Is a Constraint?

In a database, a **constraint** is a rule or condition applied to a column or a table to restrict which data can be stored.

Constraints help maintain **data integrity** and **consistency** by preventing values that violate defined rules.

They can apply to:
- **A column**, such as requiring an employee's name to be present.
- **A table**, such as requiring a combination of columns to be unique.

> **Key idea:** Constraints are rules enforced by the database, rather than checks that depend only on the application interface.

## 2. Why Are Constraints Important?

Constraints help:
- Prevent duplicate values where uniqueness is required.
- Prevent missing values in required fields.
- Maintain valid relationships between related tables.
- Reject values that do not satisfy specified conditions.
- Keep stored data more consistent and easier to manage.

Constraints support data integrity, but they cannot guarantee that every accepted value is factually correct. For example, a valid-looking name can still be misspelled.

## 3. Common Types of Constraints

### 3.1 PRIMARY KEY

A **PRIMARY KEY** uniquely identifies each row in a table.

- Values must be **unique**.
- Values **cannot be `NULL`**.
- A primary key can consist of one column or multiple columns.

**Example:** `Employees.EmployeeID` uniquely identifies each employee.

### 3.2 FOREIGN KEY

A **FOREIGN KEY** creates and enforces a reference from one table to a key in another table (or, in some designs, the same table).

- Helps maintain **referential integrity**.
- Prevents a non-`NULL` reference to a record that does not exist in the referenced table.
- A foreign key value may be `NULL` if the column allows it.

**Example:** `Employees.DepartmentID` refers to `Departments.ID`.

If the departments are numbered `1`, `2`, and `3`, a new employee cannot use `DepartmentID = 99` when the foreign key constraint is enforced.

### 3.3 UNIQUE

A **UNIQUE** constraint prevents duplicate values in a specified column or combination of columns.

**Example:** An employee email address must not be reused by another employee.

**How is it different from PRIMARY KEY?**

| Feature | PRIMARY KEY | UNIQUE |
|---|---|---|
| Ensures uniqueness | Yes | Yes |
| Accepts `NULL` | No | Depends on the DBMS and column settings |
| Main purpose | Identify each row | Prevent duplicate values |
| Number of constraints per table | One primary-key constraint | Multiple unique constraints are possible |

**Important SQL Server note:** For a single-column `UNIQUE` constraint, SQL Server permits `NULL` if the column is nullable, but ordinarily allows **only one** `NULL` under that constraint. This detail differs among database systems. The course's short interview answer—“PRIMARY KEY does not allow NULL, while UNIQUE allows NULL”—is a useful starting distinction, but it needs this qualification for SQL Server.

### 3.4 NOT NULL

A **NOT NULL** constraint requires a column to have a value instead of `NULL`.

**Example:** `FirstName` must be supplied for each employee.

> `NOT NULL` rejects `NULL`; it does **not** necessarily reject an empty string (`''`).

### 3.5 CHECK

A **CHECK** constraint requires values to satisfy a condition.

**Examples:**
- Salary must be zero or greater: `Salary >= 0`.
- Age must be within an allowed range.

**SQL Server note:** A `CHECK` condition does not itself prohibit `NULL`; use `NOT NULL` as well if the value is required.

## 4. Practical Example: Employees and Departments

**Departments**

| ID (PRIMARY KEY) | Name |
|---|---|
| 1 | IT |
| 2 | Finance |

**Employees**

| EmployeeID (PRIMARY KEY) | FirstName (NOT NULL) | Email (UNIQUE) | Salary (CHECK) | DepartmentID (FOREIGN KEY) |
|---|---|---|---|---|
| 101 | Ahmed | ahmed@example.com | 5000 | 1 |
| 102 | Ali | ali@example.com | 3000 | 2 |

The constraints protect different aspects of the data:

- A second employee cannot use `EmployeeID = 101` (**PRIMARY KEY**).
- An employee cannot use `DepartmentID = 99` unless department `99` exists (**FOREIGN KEY**).
- Two employees cannot use the same non-`NULL` email (**UNIQUE**).
- `FirstName` cannot be `NULL` (**NOT NULL**).
- `Salary = -400` is rejected (**CHECK**, when defined as `Salary >= 0`).

## 5. Basic SQL Server Example

```sql
CREATE TABLE Departments
(
    ID INT PRIMARY KEY,
    Name NVARCHAR(100) NOT NULL
);

CREATE TABLE Employees
(
    EmployeeID INT PRIMARY KEY,
    FirstName NVARCHAR(100) NOT NULL,
    Email NVARCHAR(255) UNIQUE,
    Salary DECIMAL(10, 2) NOT NULL CHECK (Salary >= 0),
    DepartmentID INT,
    FOREIGN KEY (DepartmentID) REFERENCES Departments(ID)
);
```

We will practice creating and changing constraints later when studying **SQL DDL** in SQL Server Management Studio (**SSMS**).

## 6. Interview Question

**Q: What is the difference between a PRIMARY KEY constraint and a UNIQUE constraint?**

**Short answer:** Both enforce uniqueness. A **PRIMARY KEY** also identifies each row and never permits `NULL`; a **UNIQUE** constraint is used to prevent duplicate values in other columns and can be defined on a nullable column, with `NULL` handling dependent on the database system.

## 7. Quick Review

| Constraint | Main role |
|---|---|
| `PRIMARY KEY` | Unique identifier for a row; no `NULL` |
| `FOREIGN KEY` | Enforces valid references between tables |
| `UNIQUE` | Prevents duplicate values |
| `NOT NULL` | Requires a non-`NULL` value |
| `CHECK` | Enforces a specified condition |

**Summary:** Constraints are database rules that help protect the **integrity** and **consistency** of stored data.

---

*Study notes based on the course slides: “What Is Constraint? and Why Is It Important?” Additional SQL Server-specific notes are explicitly labeled above.*
