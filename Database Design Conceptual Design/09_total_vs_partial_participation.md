# Total vs Partial Participation

**Database Design — Conceptual Design | Lesson 09**

## 1. What Is Participation in an ERD?

**Participation** describes whether an entity instance **must** take part in a relationship or **may** exist without taking part.

It answers an important question:

> **Is this relationship mandatory or optional for every instance of this entity?**

Participation concerns the **minimum** number of related instances, not the maximum.

- **Total participation** → mandatory → minimum **1**.
- **Partial participation** → optional → minimum **0**.

> Participation is related to **ordinality (minimum cardinality)** from the previous lesson.

---

## 2. Total Participation (Mandatory)

**Total participation** means **every instance** of an entity **must participate** in the specified relationship **at least once**.

### Chen ERD symbol

A **double line** connects the entity to the relationship diamond.

```text
[Entity] ═════ <Relationship>
```

### Example

Suppose every **Order** must belong to a **Customer**.

- An order cannot exist without a customer.
- The minimum number of customers for each order is **1**.
- Therefore, **Order has total participation** in the `Places` relationship.

**Important:** Total participation does **not** mean that an instance can participate only once. It means **at least once**. The maximum is decided separately.

---

## 3. Partial Participation (Optional)

**Partial participation** means an instance of an entity **can exist without participating** in the specified relationship.

### Chen ERD symbol

A **single line** connects the entity to the relationship diamond.

```text
[Entity] ───── <Relationship>
```

### Example

A **Customer** can register an account before placing any **Order**.

- A customer can exist with **zero orders**.
- The minimum number of orders for a customer is **0**.
- Therefore, **Customer has partial participation** in the `Places` relationship.

**Important:** Partial participation does **not** mean an entity never participates. It means participation is **not required**.

---

## 4. Example from the Slides: Student and Course

**Entities:** `Student`, `Course`  
**Relationship:** `Enrolled`

In the first slide:

- The **Student** side has a **double line**: **total participation**.
- The **Course** side has a **single line**: **partial participation**.

### Business rules represented by this diagram

1. **Every student must be enrolled in at least one course.**
2. **A course can exist without any enrolled students.**

The slide therefore distinguishes **required participation for students** from **optional participation for courses**.

### Min–max meaning

| Entity instance | Minimum related instances | Participation |
|---|---:|---|
| Student | **1 course** | **Total** |
| Course | **0 students** | **Partial** |

If there is no additional restriction on the maximum, this example can be expressed as:

- **For each Student:** `(1, M)` Courses.
- **For each Course:** `(0, M)` Students.

> These are the assumptions of this example. A different university could allow students with no current enrollment, changing the participation rule.

---

## 5. Example from the Slides: Customer and Order

**Entities:** `Customer`, `Order`  
**Relationship:** `Places`

In the second slide:

- The **Customer** side has a **single line**: **partial participation**.
- The **Order** side has a **double line**: **total participation**.

### Business rules represented by this diagram

1. **A customer can exist without placing an order.**
2. **Every order must be placed by a customer.**
3. **A customer can place many orders.**
4. **Each order belongs to exactly one customer.**

### Min–max meaning

| Entity instance | Minimum | Maximum | Participation |
|---|---:|---:|---|
| Customer → Orders | 0 | Many | Partial |
| Order → Customers | 1 | 1 | Total |

In words:

- **One Customer → `(0, M)` Orders**.
- **One Order → `(1, 1)` Customer**.

This is a **one-to-many** relationship with different participation requirements on each side.

---

## 6. Total vs Partial Participation: Quick Comparison

| Feature | Total Participation | Partial Participation |
|---|---|---|
| Meaning | Every entity instance must participate | Participation is optional |
| Minimum | `1` | `0` |
| Chen ERD notation | Double line | Single line |
| Also called | Mandatory / Required | Optional |
| Example | Every order belongs to a customer | A customer may have no orders |

---

## 7. Relationship to Crow's Foot Notation

The slides also show equivalent diagrams using **Crow's Foot notation**.

In Crow's Foot notation, the symbols at each end of a relationship express the **minimum and maximum number of related instances**.

| Symbols at an end | Meaning | Min–max |
|---|---|---|
| `○` + bar | Zero or one | `(0, 1)` |
| Two bars | Exactly one | `(1, 1)` |
| `○` + crow's foot | Zero or many | `(0, M)` |
| Bar + crow's foot | One or many | `(1, M)` |

### How to read the ends correctly

Look at **one entity instance** and read the symbols **at the other entity's end**.

For example, in `Customer — Places — Order`:

- The symbols **near Order** tell you how many **orders one customer** can place: **zero or many**.
- The symbols **near Customer** tell you how many **customers one order** can belong to: **exactly one**.

This is why a symbol that looks like “many” near `Order` does **not** mean “many customers per order.”

### The same business rules in two notations

**Chen notation:**

- Customer — *single line* — Places → **partial for Customer**.
- Order ═ *double line* ═ Places → **total for Order**.

**Crow's Foot notation:**

- At the **Order** end: `0..M` orders per customer.
- At the **Customer** end: `1..1` customers per order.

---

## 8. Participation vs Cardinality

These two ideas answer **different questions**:

- **Participation / Ordinality (minimum):** *Must there be at least one related instance?*
- **Cardinality (maximum):** *How many related instances are allowed at most?*

### Example

For **Customer → Order**:

- **Minimum = 0:** a customer is allowed to have no orders.
- **Maximum = M:** a customer may have many orders.

Together they form **`(0, M)`**.

For **Order → Customer**:

- **Minimum = 1:** every order must belong to a customer.
- **Maximum = 1:** an order cannot belong to multiple customers.

Together they form **`(1, 1)`**.

> A **many-to-many** relationship can have total participation on one side, partial participation on both sides, or another combination. **Maximum cardinality alone does not determine participation.**

---

## 9. A Simple Trick to Identify Participation

For each entity, ask:

> **Can one instance of this entity exist without being connected through this relationship?**

- **Yes** → **Partial participation** (minimum `0`).
- **No** → **Total participation** (minimum `1`).

Then ask a *different* question for maximum cardinality:

> **If it participates, how many instances on the other side may it connect to?**

- At most **one** → maximum `1`.
- Potentially **many** → maximum `M`.

### Important reminder

The answer depends on the **business rules**, not just on names like `Student`, `Course`, `Customer`, and `Order`.

---

## 10. Practice Questions

Try answering before checking the suggested solutions.

**Q1.** A school allows a course to exist before any student enrolls. Is the `Course` participation in `Enrolled` total or partial?

**Q2.** Every order must be associated with one customer. Is the `Order` participation in `Places` total or partial?

**Q3.** Can a relationship be `M:M` and still have total participation on the `Student` side?

**Q4.** A customer may place no orders or many orders. What is the min–max pair for **orders per customer**?

**Q5.** An order must belong to exactly one customer. What is the min–max pair for **customers per order**?

<details>
<summary>Answers</summary>

1. **Partial** (minimum `0`).
2. **Total** (minimum `1`).
3. **Yes.** `M:M` describes maximum multiplicities; total describes minimum participation.
4. **`(0, M)`**.
5. **`(1, 1)`**.

</details>

---

## 11. Key Terms

| Term | Definition |
|---|---|
| **Participation Constraint** | A rule specifying whether every entity instance must participate in a relationship. |
| **Total Participation** | Every entity instance must participate at least once. |
| **Partial Participation** | An entity instance may participate zero times. |
| **Mandatory Participation** | Another name for total participation. |
| **Optional Participation** | Another name for partial participation. |
| **Minimum Cardinality / Ordinality** | The smallest number of related instances allowed. |
| **Maximum Cardinality** | The largest number of related instances allowed. |
| **Chen Notation** | ERD notation using entities as rectangles, relationships as diamonds, and single/double participation lines. |
| **Crow's Foot Notation** | ERD notation using circles, bars, and crow's feet to show min–max multiplicities. |

---

## 12. Final Summary

- **Total = mandatory = minimum `1` = double line in Chen notation.**
- **Partial = optional = minimum `0` = single line in Chen notation.**
- **Student–Course slide:** Students participate totally; courses participate partially.
- **Customer–Order slide:** Orders participate totally; customers participate partially.
- **Participation tells you the minimum; maximum cardinality tells you the upper limit.**
- Always determine the rule **for each side separately**.

*Notes based on the provided “Total vs Partial Participation” lecture slides.*
