# What Is Data Integrity, and Why Is It Important?

## 1. What Is Data Integrity?

**Data integrity** refers to the **accuracy, consistency, and reliability** of data throughout its entire life cycle, from creation to deletion.

In simple terms, data integrity means keeping information **correct, complete when required, consistent, and trustworthy**.

For example, in an employee database, we want to ensure that:

- Each employee can be identified correctly.
- Names and dates are stored in the appropriate fields.
- Salaries follow the organization's rules.
- Every department reference points to an existing department.

## 2. Example: Data Integrity Problems

Imagine a database with two tables: **Employees** and **Departments**.

### Employees (example)

| EmployeeID (PK) | FirstName | LastName | Birthdate | Salary | DepartmentID (FK) |
|---|---|---|---|---:|---:|
| 1 | `U@s#5#Z]9E` | Abu-Hadhoud | 1977-06-11 | -400 | 1 |
| 2 | Ali | Zaher | 1990-05-07 | 3000 | 2 |
| 3 | Lubna | `1/1/2000` | `Hamdi` | 500 | 1 |
| 8 | Huda | Omar | 1990-04-02 | 1000 | 5 |

### Departments (example)

| ID (PK) | Name | Location |
|---|---|---|
| 1 | IT | Amman |
| 2 | Finance | Amman |
| 3 | HR | UAE |
| 4 | Marketing | Qatar |

The highlighted problems from the lesson include:

1. **Unexpected characters in a name:** A name field contains symbols instead of a plausible employee name. Whether such characters are valid depends on the application's naming rules.
2. **Negative salary:** A salary of `-400` may violate the company's salary rules.
3. **Wrong information in a column:** A date has been placed in `LastName`, while a name has been placed in `Birthdate`.
4. **Invalid department reference:** Employee 8 has `DepartmentID = 5`, but no department with `ID = 5` exists in the Departments table.

These are examples of why a database needs validation rules, appropriate data types, and constraints.

> **Note:** The sample above illustrates bad or inconsistent input. If the corresponding SQL data types and constraints are configured correctly, several of these values would be rejected rather than stored.

## 3. What Can Affect Data Integrity?

The lesson identifies several causes of data integrity problems:

- **Human error:** Entering incorrect information or editing the wrong record.
- **Hardware failure:** Storage or hardware problems that damage or lose data.
- **Software failure:** Bugs or crashes that cause incorrect or incomplete changes.
- **Security breaches:** Unauthorized access or modification of data.
- **Data transfer errors:** Problems while importing, exporting, or transmitting data.

Organizations protect data integrity with suitable **policies, procedures, and technical controls**, including validation, database constraints, backups, access controls, and other safeguards.

## 4. Types of Data Integrity

### 4.1. Entity Integrity

**Entity integrity** ensures that each row in a table can be uniquely identified.

It is typically enforced using a **Primary Key (PK)**:

- The primary key must be **unique**.
- The primary key cannot be **NULL**.

**Example:** Two employees cannot share the same `EmployeeID` when it is the primary key.

### 4.2. Referential Integrity

**Referential integrity** ensures that references between related tables remain valid.

It is typically enforced using a **Foreign Key (FK)**.

**Example:** `Employees.DepartmentID` references `Departments.ID`. If no department has `ID = 5`, a foreign key constraint rejects `DepartmentID = 5`.

If the foreign-key column allows `NULL`, that value is also permitted because it does not point to a non-existent record.

### 4.3. Domain Integrity

**Domain integrity** ensures that data values belong to the allowed type, format, or range for a column.

**Examples:**

- `Birthdate` should contain a valid date.
- `Salary` should contain a valid number.
- Other limits can require a value to fall within an acceptable range.

Appropriate SQL **data types** and **constraints** help enforce these rules.

### 4.4. Business Integrity

**Business integrity** ensures that data follows the specific rules and requirements of an organization.

**Examples:**

- A bank may have minimum or maximum balance rules for certain account types.
- A company may require salaries to follow its payroll rules.
- A hospital may have requirements governing the confidentiality and handling of patient information.

Business integrity may require **database constraints, application logic, and organizational policies**, depending on the rule.

## 5. Comparison of the Four Types

| Type | Main question | Typical mechanism | Example |
|---|---|---|---|
| **Entity Integrity** | Can each row be uniquely identified? | Primary Key | No duplicate employee IDs |
| **Referential Integrity** | Does a reference point to a valid record? | Foreign Key | DepartmentID must refer to an existing department |
| **Domain Integrity** | Is this value valid for the column? | Data types, validation, CHECK constraints | Birthdate must be a date |
| **Business Integrity** | Does the data follow the organization's rules? | Business rules, constraints, application checks | Salary follows company policy |

## 6. Why Is Data Integrity Important?

Organizations depend on accurate and trustworthy information when making decisions.

Poor data integrity can cause:

- Incorrect reports and decisions
- Incomplete or unreliable records
- Financial losses
- Operational problems
- Damage to an organization's reputation

Maintaining data integrity reduces these risks and makes database information more dependable.

## 7. How Do We Maintain Data Integrity?

The course introduces **constraints** as a key mechanism. We will study them in more detail in the next lesson.

Common safeguards include:

- **PRIMARY KEY:** Uniquely identifies table rows.
- **FOREIGN KEY:** Protects valid references between tables.
- **NOT NULL:** Requires a column to have a value.
- **UNIQUE:** Prevents duplicate values under a uniqueness rule.
- **CHECK:** Enforces a condition, such as an acceptable salary range.
- **Suitable data types:** Prevent storing incompatible values in columns.
- **Backups and access controls:** Help protect information against accidental loss or unauthorized changes.

## 8. Quick Summary

- **Data Integrity:** Keeping data accurate, consistent, reliable, and trustworthy.
- **Entity Integrity:** Every row has a valid, unique identity — commonly through a **Primary Key**.
- **Referential Integrity:** Relationships refer to valid records — commonly through a **Foreign Key**.
- **Domain Integrity:** Column values follow the correct types and allowed ranges.
- **Business Integrity:** Data follows the organization's specific rules.
- **Constraints:** Database rules that help maintain data integrity.

> **Key takeaway:** Data integrity is not only about storing information. It is about ensuring that the information remains **correct and reliable** throughout its life cycle.

---

*Study notes based on the course slides: “What Is Data Integrity? And Why Is It Important and Critical?”*
