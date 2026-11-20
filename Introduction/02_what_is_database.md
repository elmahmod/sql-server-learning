# What Is a Database?

## 1. Definition

A **database** is an organized collection of data that can be easily **accessed, managed, and updated**.

A **Database Management System (DBMS)** is software used to create, store, retrieve, modify, and manage databases.

## 2. Types of Database Systems

The course introduces two broad approaches:

| Type | Description | Examples |
|---|---|---|
| **Non-relational** | Does not organize all data using the relational table-and-relationship model. | Document-oriented databases, key-value databases |
| **Relational (RDBMS)** | Organizes data in tables containing rows and columns and can establish relationships between tables. | Microsoft SQL Server, Oracle Database, MySQL |

**DBMS vs. RDBMS:** An **RDBMS** (Relational Database Management System) is a **type of DBMS** designed for relational databases.

> **Clarification about the slide:** The slide mentions a **file system** and **XML** under non-relational systems. A file system is a way to store files, and XML is a data format; neither is, by itself, a non-relational DBMS. They are useful examples of ways to store or represent data outside a relational database.

## 3. Example: Employees Stored in One File

The course first shows employee and department information together in an **Employees File**:

| ID | FirstName | LastName | Gender | Birthdate | Salary | DeptID | DeptName | DeptLocation |
|---|---|---|---|---|---:|---:|---|---|
| 1 | Mohammed | Abu-Hadhoud | M | 6/11/1977 | 5000 | 1 | IT | Amman |
| 2 | Ali | Zaher | M | 5/7/1990 | 3000 | 2 | Finance | Amman |
| 3 | Lubna | Aqel | F | 5/5/2000 | 500 | 1 | IT | Amman |

Notice that **IT** and **Amman** are repeated for employees in the same department. This is an example of **data redundancy** (repeated information).

## 4. The Same Information in an RDBMS

A relational design can organize the data into two related tables.

### Employees Table

| ID | FirstName | LastName | Gender | Birthdate | Salary | DepartmentID |
|---|---|---|---|---|---:|---:|
| 1 | Mohammed | Abu-Hadhoud | M | 6/11/1977 | 5000 | 1 |
| 2 | Ali | Zaher | M | 5/7/1990 | 3000 | 2 |
| 3 | Lubna | Aqel | F | 5/5/2000 | 500 | 1 |

### Departments Table

| ID | Name | Location |
|---|---|---|
| 1 | IT | Amman |
| 2 | Finance | Amman |
| 3 | HR | UAE |
| 4 | Marketing | Qatar |

### Relationship Between the Tables

- **Employees.DepartmentID** identifies the department to which an employee belongs.
- **Departments.ID** uniquely identifies each department.
- These columns can be linked using a **foreign key** relationship.
- For example, the employee with `DepartmentID = 1` belongs to the **IT** department.

This separation reduces unnecessary repetition of department names and locations in employee records.

## 5. Basic Relational Database Terminology

| Term | Meaning | Example |
|---|---|---|
| **Table** | A set of related records organized in rows and columns | `Employees` |
| **Column / Field / Attribute** | A named property of the data | `FirstName`, `Salary`, `DepartmentID` |
| **Row / Record** | One complete entry in a table | The employee with `ID = 1` |
| **Primary Key** | A column (or set of columns) that uniquely identifies a row | `Departments.ID` |
| **Foreign Key** | A column (or set of columns) that refers to a key in another table | `Employees.DepartmentID` |

In conceptual modeling, a table is often associated with an **entity set**, and a row represents an individual **entity**. In relational database terminology, **table**, **column**, and **row** are the clearest terms.

## 6. Quick Summary

- A **database** is an organized collection of data.
- A **DBMS** is software that manages databases.
- An **RDBMS** is a DBMS that works with relational tables.
- Relational tables contain **rows (records)** and **columns (fields/attributes)**.
- **Relationships** connect related tables, such as `Employees` and `Departments`.

---

*Study notes based on the course slides: “What Is Database?” and “In RDBMS.”*
