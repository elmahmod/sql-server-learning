# Primary Key vs. Foreign Key / Referential Integrity

## 1. Overview

In a **relational database**, tables can be connected through keys. Two important types are:

- **Primary Key (PK):** identifies each record in a table.
- **Foreign Key (FK):** connects a record in one table to a record in another table.

The lesson uses an **Employees** table and a **Departments** table to illustrate this relationship.

## 2. Primary Key (PK)

A **primary key** is a column or a combination of columns that **uniquely identifies every row (record)** in a table.

Important properties:

- **Unique:** two records cannot have the same primary key value.
- **NOT NULL:** a primary key cannot contain `NULL`.
- **Stable:** a primary key should ideally remain unchanged over time.
- **Reference point:** other tables can refer to the primary key to establish relationships.

### Example: Departments Table

| **ID (PK)** | Name | Location |
|---:|---|---|
| **1** | IT | Amman |
| **2** | Finance | Amman |
| **3** | HR | UAE |
| **4** | Marketing | Qatar |

Here, `ID` is the **primary key** because each department has its own unique ID.

### Example: Employees Table

| **ID (PK)** | FirstName | LastName | DepartmentID (FK) |
|---:|---|---|---:|
| **1** | Mohammed | Abu-Hadhoud | 1 |
| **2** | Ali | Zaher | 2 |
| **3** | Lubna | Aqel | 1 |
| **5** | Fadi | Khalil | 4 |
| **6** | Maha | Majed | 3 |
| **7** | Omar | Ali | 1 |
| **8** | Huda | Omar | 1 |

Here, `Employees.ID` is the **primary key**, uniquely identifying each employee.

## 3. Foreign Key (FK)

A **foreign key** is a column or combination of columns in one table that **refers to a key in another table**. It establishes a relationship between the two tables.

In our example:

- `Departments.ID` is the **primary key** of the `Departments` table.
- `Employees.DepartmentID` is a **foreign key** referring to `Departments.ID`.

```text
Departments
  ID (Primary Key)
       ↑
       │ referenced by
       │
Employees
  DepartmentID (Foreign Key)
```

For example, an employee with `DepartmentID = 1` belongs to the **IT** department because `Departments.ID = 1` identifies IT.

**Note:** A foreign key value can repeat. Several employees can belong to the same department.

## 4. Referential Integrity

**Referential integrity** means that relationships between tables remain valid.

When a foreign key is enforced by the database:

- A **non-NULL** `Employees.DepartmentID` must match an existing `Departments.ID`.
- `DepartmentID = 1` is valid because department `1` exists.
- `DepartmentID = 99` is invalid if no department with ID `99` exists.

This prevents employees from referring to departments that do not exist.

## 5. Primary Key vs. Foreign Key

| Feature | Primary Key (PK) | Foreign Key (FK) |
|---|---|---|
| **Main purpose** | Uniquely identifies a row | Links rows between tables |
| **Must be unique?** | Yes | No; values may repeat |
| **Can contain NULL?** | No | Yes, if the column is defined to allow `NULL` |
| **In the example** | `Departments.ID` or `Employees.ID` | `Employees.DepartmentID` |
| **Main benefit** | Record identification | Relationships and referential integrity |

## 6. SQL Server Example

The following is a small practical illustration of the same idea:

```sql
CREATE TABLE Departments
(
    ID INT PRIMARY KEY,
    Name NVARCHAR(100) NOT NULL,
    Location NVARCHAR(100)
);

CREATE TABLE Employees
(
    ID INT PRIMARY KEY,
    FirstName NVARCHAR(100) NOT NULL,
    LastName NVARCHAR(100),
    DepartmentID INT,

    CONSTRAINT FK_Employees_Departments
        FOREIGN KEY (DepartmentID) REFERENCES Departments(ID)
);
```

The `FOREIGN KEY` constraint tells SQL Server to enforce the relationship between `Employees.DepartmentID` and `Departments.ID`.

## 7. Important Technical Clarifications

The course slides present the beginner-friendly rules. A few details are worth remembering:

- **A table can technically exist without a primary key**, although defining an appropriate one is strongly recommended for most tables.
- **A primary key should usually stay stable**, but SQL does not make it impossible to change its value; changes may be restricted by relationships.
- A foreign key commonly references another table's **primary key**, but it can also reference an eligible **unique key**.
- A foreign key may contain **`NULL` if the column permits it**. Referential integrity applies to its non-NULL references. In this example, `DepartmentID` is optional because it was not declared `NOT NULL`.

## 8. Quick Summary

- **Primary Key:** identifies each record uniquely; no duplicates and no `NULL`.
- **Foreign Key:** refers to a key in another table and connects the tables.
- **Referential Integrity:** prevents invalid references between related records.

**Remember:** `Employees.DepartmentID = 1` points to `Departments.ID = 1`, which represents the **IT** department.

---

*Study notes based on the course slides: “Primary Key vs Foreign Key / Referential Integrity”.*
