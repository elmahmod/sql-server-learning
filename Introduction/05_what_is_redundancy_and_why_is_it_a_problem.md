# What Is Redundancy, and Why Is It a Problem?

## 1. What Is Data Redundancy?

**Data redundancy** refers to unnecessary duplication of information in a database. It happens when the same fact is stored multiple times, or when information that can be derived from other data is stored again.

Redundancy is not always harmful, but unnecessary duplication can make a database harder to maintain and more prone to inconsistent data.

## 2. Example: Employees File

Imagine storing employee information and department information in one file or table:

| EmployeeID | FirstName | LastName | DeptID | DeptName | DeptLocation |
|---|---|---|---|---|---|
| 1 | Mohammed | Abu-Hadhoud | 1 | IT | Amman |
| 3 | Lubna | Aqel | 1 | IT | Amman |
| 7 | Omar | Ali | 1 | IT | Amman |
| 8 | Huda | Omar | 1 | IT | Amman |

The values **IT** and **Amman** are repeated for every employee in department **1**. The department's name and location are facts about the *department*, not facts that need to be stored separately for each employee.

### Why can this become a problem?

Suppose the IT department moves from **Amman** to **Irbid**. If the location is stored in every employee record, you must update every row for that department. If you miss a row, some employees will appear to belong to the same department in different locations.

## 3. Problems Caused by Unnecessary Redundancy

The course slides identify these potential problems:

1. **Wasted storage space** — repeated information takes additional space.
2. **Data inconsistency** — copies of the same fact can disagree after an incomplete update.
3. **Data corruption or errors** — conflicting or incorrectly changed copies can make data unreliable.
4. **Missing or incomplete data** — a design that mixes different kinds of information can make insertion and deletion difficult.
5. **Data integrity problems** — it becomes harder to keep stored facts correct and consistent.
6. **Difficult maintenance** — changes may need to be applied in many places.

Three common issues that result from poor table design are often called **update anomalies**, **insertion anomalies**, and **deletion anomalies**.

## 4. Solution: Normalization

**Normalization** is the process of organizing relational database data to reduce unnecessary redundancy and improve data integrity.

One common approach is to separate information about different entities into related tables.

### Employees Table

| EmployeeID (PK) | FirstName | LastName | DepartmentID (FK) |
|---|---|---|---|
| 1 | Mohammed | Abu-Hadhoud | 1 |
| 3 | Lubna | Aqel | 1 |
| 7 | Omar | Ali | 1 |
| 8 | Huda | Omar | 1 |

### Departments Table

| ID (PK) | Name | Location |
|---|---|---|
| 1 | IT | Amman |
| 2 | Finance | Amman |
| 3 | HR | UAE |
| 4 | Marketing | Qatar |

**Relationship:** `Employees.DepartmentID` references `Departments.ID`.

- `Departments.ID` is the **Primary Key** of the departments table.
- `Employees.DepartmentID` is the **Foreign Key** linking an employee to a department.
- The name and location of each department are stored **once** in the `Departments` table.

Now, if the IT department changes location, you update **one department row** instead of every employee row.

## 5. What Does Normalization Do?

Normalization typically:

- Organizes data into appropriately related tables.
- Reduces unnecessary duplication.
- Makes updates and maintenance easier.
- Helps prevent inconsistencies and improve data integrity.
- Works together with constraints such as **Primary Keys**, **Foreign Keys**, and **UNIQUE** constraints.

Normalization has several levels called **normal forms** (such as 1NF, 2NF, and 3NF), which can be studied later.

## 6. Important Clarifications

- **Not every repeated value is a design problem.** Repeating `DepartmentID = 1` for employees who belong to the same department is expected and necessary for the relationship.
- **Normalization does not remove every repeated value.** Its goal is to reduce *unnecessary* redundancy and improve consistency.
- **Redundancy can sometimes be intentional**, for example for performance or reporting, but it introduces additional maintenance considerations.
- **Constraints support data integrity**, but they do not automatically eliminate every kind of redundancy.

## 7. Quick Summary

| Term | Meaning |
|---|---|
| **Redundancy** | Unnecessary duplication of stored information |
| **Data inconsistency** | Different copies of the same fact do not agree |
| **Normalization** | Organizing related tables to reduce unnecessary duplication and improve integrity |
| **Primary Key** | Uniquely identifies a row in a table |
| **Foreign Key** | Links a row to a key in a related table |

**Main idea:** Store facts about employees in **Employees**, facts about departments in **Departments**, and connect them through **DepartmentID** rather than repeating department names and locations for every employee.

---

*Study notes based on the course slides: “What Is Redundancy, and Why Is It a Problem?”*
