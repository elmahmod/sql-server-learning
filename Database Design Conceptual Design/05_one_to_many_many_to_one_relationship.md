# One-to-Many / Many-to-One Relationship

## 1. What Is a One-to-Many Relationship?

A **one-to-many relationship (`1:M`)** exists when **one instance of an entity can be related to many instances of another entity**, while each instance on the “many” side is related to only **one** instance on the other side.

In a Chen-style ERD, it is commonly shown like this:

```text
[Entity A] -- 1 -- <Relationship> -- M -- [Entity B]
```

### Simple idea

- **One customer** can place **many orders**.
- But **each order** belongs to **one customer**.

So from **Customer → Order** the relationship is **one-to-many**.

---

## 2. What Is a Many-to-One Relationship?

A **many-to-one relationship (`M:1`)** is the same relationship viewed from the opposite direction.

```text
[Entity A] -- M -- <Relationship> -- 1 -- [Entity B]
```

### Simple idea

- **Many orders** can belong to **one customer**.

So from **Order → Customer** the relationship is **many-to-one**.

> **Important:** `1:M` and `M:1` usually describe the **same business rule**, but from different directions.

---

## 3. Main Idea of the Lesson

The lesson explains:

- If **one entity instance** is associated with **many instances** of another entity, it is **one-to-many**.
- If **many instances** of one entity are associated with **one instance** of another entity, it is **many-to-one**.

They are not two completely different kinds of relationships. They are **two views of the same relationship**.

---

## 4. Examples from the Lesson

### Example 1: Customer and Order

#### One-to-Many view

- **Entities:** `Customer`, `Order`
- **Relationship:** `Place`
- **Cardinality:** `1:M`

```text
[Customer] -- 1 -- <Place> -- M -- [Order]
```

**Meaning:** One customer can place many orders, but each order cannot be placed by many customers.

#### Many-to-One view

- **Entities:** `Order`, `Customer`
- **Relationship:** `Ordered By`
- **Cardinality:** `M:1`

```text
[Order] -- M -- <Ordered By> -- 1 -- [Customer]
```

**Meaning:** Many orders can be ordered by one customer.

---

### Example 2: Employee and Project

#### Many-to-One view

- **Entities:** `Employee`, `Project`
- **Relationship:** `Works on`
- **Cardinality:** `M:1`

```text
[Employee] -- M -- <Works on> -- 1 -- [Project]
```

**Meaning in the slide:** Many employees can work on one project.

#### One-to-Many view

- **Entities:** `Project`, `Employee`
- **Relationship:** `Workers`
- **Cardinality:** `1:M`

```text
[Project] -- 1 -- <Workers> -- M -- [Employee]
```

**Meaning:** One project can have many employees.

---

### Example 3: Member and Book

- **Entities:** `Member`, `Book`
- **Relationship:** `Borrow`
- **Cardinality:** `1:M`

```text
[Member] -- 1 -- <Borrow> -- M -- [Book]
```

**Meaning in the lesson:** One member can borrow many books, and each book can be borrowed by one member.

> **Modeling note:** This is a simplified business rule used for explanation. In real systems, borrowing is often modeled with a separate transaction entity such as `Loan`.

---

### Example 4: Customer and Mobile Line

- **Entities:** `Customer`, `MobileLine`
- **Relationship:** `Subscribe`
- **Cardinality:** `1:M`

```text
[Customer] -- 1 -- <Subscribe> -- M -- [MobileLine]
```

**Meaning:** One customer can subscribe to many mobile lines, but each line belongs to one customer.

---

### Example 5: Citizen and Car

- **Entities:** `Citizen`, `Car`
- **Relationship:** `Own`
- **Cardinality:** `1:M`

```text
[Citizen] -- 1 -- <Own> -- M -- [Car]
```

**Meaning:** One citizen can own many cars, while each car is owned by one citizen.

---

## 5. Self Relationship (Recursive Relationship)

The last slide also shows a **self relationship**.

A **self relationship** happens when an entity is related to **itself**.

### Example: Employee managed by Employee

- **Entity:** `Employee`
- **Relationship:** `Managed By`
- **Cardinality shown:** `M:1`

```text
[Employee] -- M -- <Managed By> -- 1 -- [Employee]
```

**Meaning:**

- One employee has only one manager.
- One manager can manage many employees.

This is still a **one-to-many / many-to-one** relationship, but both sides refer to the **same entity type**.

### Database implementation idea

This is often implemented using a foreign key inside the same table:

| EmployeeID | Name | Salary | ManagerID |
|---|---|---:|---:|
| 1 | Ahmed | 5000 | NULL |
| 2 | Amjad | 1500 | 1 |
| 3 | Maher | 1300 | 2 |
| 4 | Alia | 500 | 2 |

Here:

- `EmployeeID` is the primary key.
- `ManagerID` is a foreign key that points to another row in the **same** `Employees` table.

---

## 6. How to Recognize 1:M and M:1

Ask these questions:

1. Can **one A** be related to **many B**?
2. Can **one B** be related to **many A**?

If the answers are:

- **Yes** for A → B
- **No** for B → A

then the relationship is:

- **One-to-Many (`1:M`)** from A to B
- **Many-to-One (`M:1`)** from B to A

### Example

For `Customer` and `Order`:

- One customer → many orders ✅
- One order → many customers ❌

Therefore:

- `Customer → Order` is `1:M`
- `Order → Customer` is `M:1`

---

## 7. Why This Relationship Is Important

One-to-many relationships are very common in database design because many real-world systems work this way.

Examples:

- One **department** has many **employees**.
- One **teacher** teaches many **students**.
- One **customer** places many **orders**.
- One **manager** manages many **employees**.

Understanding this relationship helps you:

- design tables correctly,
- place foreign keys in the correct table,
- avoid data duplication,
- and understand the business rules clearly.

---

## 8. Where Does the Foreign Key Go?

In most relational database designs, the **foreign key is placed on the many side**.

### Example: Customer and Order

- `Customers(CustomerID, Name, ... )`
- `Orders(OrderID, OrderDate, CustomerID, ... )`

Here, `CustomerID` is stored in `Orders` because:

- one customer can have many orders,
- so each order needs to remember **which customer it belongs to**.

---

## 9. Quick Comparison

| View | Meaning | Example |
|---|---|---|
| **One-to-Many (`1:M`)** | One instance on the left can relate to many on the right. | One customer places many orders. |
| **Many-to-One (`M:1`)** | Many instances on the left relate to one on the right. | Many orders belong to one customer. |
| **Self Relationship** | An entity relates to itself. | One manager manages many employees. |

---

## 10. Important Terms

| Term | Meaning |
|---|---|
| **One-to-Many Relationship** | One instance is related to many instances on the other side. |
| **Many-to-One Relationship** | Many instances are related to one instance on the other side. |
| **Cardinality** | The maximum number of related instances allowed. |
| **Entity** | An object or concept about which data is stored. |
| **Relationship** | An association between entities. |
| **Foreign Key** | An attribute that refers to a primary key in another table (or the same table in a self relationship). |
| **Self Relationship / Recursive Relationship** | A relationship where an entity is related to itself. |

---

## 11. Key Takeaway

A **one-to-many relationship** means:

- one instance on one side can be associated with many instances on the other side,
- but each instance on the many side is associated with only one instance on the one side.

And **many-to-one** is simply the same relationship viewed from the opposite direction.

---

*Study notes based on the course slides: “One-to-Many / Many-to-One Relationship.”*
