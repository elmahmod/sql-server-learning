# What Is NULL?

## 1. Definition

In a database, **`NULL`** is a special marker that indicates the **absence of a value** in a table column.

It may mean that the information is:

- **Missing** — no value has been provided.
- **Unknown** — the value is not currently known.
- **Not applicable** — the field does not apply in this situation.

**Important:** `NULL` is not an ordinary data value. It represents the *absence* of a value.

## 2. Example: Employees Table

Consider an `Employees` table:

| ID | FirstName | LastName | Gender | Birthdate | Salary | DepartmentID |
|---|---|---|---|---|---:|---:|
| 1 | Mohammed | Abu-Hadhoud | M | 6/11/1977 | 5000 | 1 |
| 2 | Ali | Zaher | M | **NULL** | **NULL** | 2 |
| 3 | Lubna | Aqel | F | 5/5/2000 | 500 | 1 |

For the employee **Ali**:

- `Birthdate = NULL`: the employee's birthdate is not recorded or is unknown.
- `Salary = NULL`: the salary is not recorded or is unknown. **It does not mean the salary is 0.**
- `DepartmentID = 2`: this is a known value that identifies the employee's department.

## 3. NULL vs. Zero vs. Empty Text

These are different concepts:

| Example | Meaning |
|---|---|
| `NULL` | No known or applicable value is stored |
| `0` | A known numeric value equal to zero |
| `''` | An empty string (text with zero characters) |
| `' '` | A string containing a space character |

**Example:** A salary of `0` says something different from a salary of `NULL`.

## 4. Why Use NULL?

According to the lesson, `NULL` is useful for:

1. **Missing data** — information has not been entered.
2. **Optional fields** — the field is allowed to have no value.
3. **Not-yet-known information** — the value may become available later.

However, `NULL` must be handled carefully because it can affect the results of **queries and calculations**.

## 5. Quick Summary

- `NULL` means **missing, unknown, or not applicable information**.
- `NULL` is **not** the same as `0`, `''`, or `' '`.
- `NULL` can be useful for optional and incomplete fields.
- Treat it carefully when filtering and calculating data.

> **Remember:** `NULL` means **no value is available**, not that the value is zero.

---

*Study notes based on the course slides: "What Is NULL?". Section 5 contains additional SQL Server examples for practice.*
