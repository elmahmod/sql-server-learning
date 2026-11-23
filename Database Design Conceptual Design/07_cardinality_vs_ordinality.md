# Cardinality vs. Ordinality

> **Database Design — Conceptual Design | Lesson 07**  
> Topic: Understanding the maximum and minimum participation in ERD relationships.

## 1. Introduction

An Entity–Relationship Diagram (ERD) describes how entities are connected. Two important concepts help us describe those connections more precisely:

- **Cardinality:** the **maximum** number of relationships allowed.
- **Ordinality:** the **minimum** number of relationships required.

Together, they tell us **how many** related records are allowed and **whether the relationship is optional or mandatory**.

In the slides, these are shown using the notation **`(Min, Max)`**.

---

## 2. Cardinality — Maximum

**Cardinality** specifies the **maximum number of times** an instance of one entity can be associated with instances of another entity.

The slides use:

| Symbol | Meaning |
|---|---|
| `1` | At most **one** related instance |
| `M` | Potentially **many** related instances |

### Example: Student and Course

A student may enroll in many courses, and one course may have many students.

```text
Student -- M -- <Enrolled> -- M -- Course
```

This is a **many-to-many (`M:M`)** relationship.

### Example: Customer and Order

A customer may place many orders, but each order is placed by one customer.

```text
Customer -- 1 -- <Place> -- M -- Order
```

This is a **one-to-many (`1:M`)** relationship, as presented in the lesson.

---

## 3. Ordinality — Minimum

**Ordinality**, as used in this course, specifies the **minimum number of times** an instance must participate in a relationship.

It answers this question:

**Is participation optional, or is it required?**

| Minimum | Meaning | Participation |
|---|---|---|
| `0` | Participation is not required | **Optional** |
| `1` | At least one related instance is required | **Mandatory / Required** |

### Example: Optional participation

A newly registered student might not be enrolled in any course yet.

- Minimum number of courses: `0`
- Enrollment is **optional** for that student.

### Example: Mandatory participation

An order must belong to a customer under the business rule in the course example.

- Minimum number of customers for an order: `1`
- Having a customer is **mandatory** for that order.

---

## 4. Min–Max Notation: `(Min, Max)`

We can combine **ordinality** and **cardinality** into a single pair:

```text
(Min, Max)
```

The first number is the **minimum**; the second is the **maximum**.

| Notation | Name | Meaning |
|---|---|---|
| `(0,1)` | Optional one | Zero or one related instance |
| `(1,1)` | Mandatory one | Exactly one related instance |
| `(0,M)` | Optional many | Zero, one, or many related instances |
| `(1,M)` | Mandatory many | One or many related instances |

### Reading examples

- **`(0,1)`**: The relationship is optional, but if it exists, there can be only one.
- **`(1,1)`**: The relationship is required and must involve exactly one.
- **`(0,M)`**: The relationship is optional and can involve many.
- **`(1,M)`**: The relationship is required and can involve many.

> **Key rule:** The minimum tells us whether participation is **optional or mandatory**. The maximum tells us whether it is **one or many**.

---

## 5. Slide Example 1: Student and Course

### Relationship: `Enrolled`

The lesson shows:

```text
Student -- (0,M) -- <Enrolled> -- (0,M) -- Course
```

**Business rules:**

1. A student can enroll in many courses.
2. A course can include many students.
3. A student can initially have **zero** course enrollments.
4. A course can initially have **zero** enrolled students.

**Explanation:**

- From a **student's perspective**, the number of courses can be **`(0,M)`**.
- From a **course's perspective**, the number of students can be **`(0,M)`**.

Both sides allow multiple related instances, and both sides permit zero.

**Relationship type:** `M:M` — **Many-to-Many**.

---

## 6. Slide Example 2: Customer and Order

### Relationship: `Place`

The slide displays:

```text
Customer -- (1,1) -- <Place> -- (0,M) -- Order
```

The labels shown near **Customer** and **Order** are **`(1,1)`** and **`(0,M)`**, respectively.

### Intended business rules of the example

1. A **customer** can place **zero or many orders**.
2. An **order** is placed by **exactly one customer**.

Read by asking about each individual instance:

| Starting from one... | How many of the other entity? | Min–Max |
|---|---|---|
| **Customer** | Orders | `(0,M)` |
| **Order** | Customers | `(1,1)` |

**Relationship type:** `1:M` — **One-to-Many** from Customer to Order.

### Important reading note

In this slide, the pair **`(1,1)` next to Customer** describes **the number of customers per order**, while **`(0,M)` next to Order** describes **the number of orders per customer**. This is a possible way of labeling multiplicities at the opposite ends of a relationship.

Other ERD conventions attach a pair beside an entity to describe **that entity's own participation**. Under that convention, the same intended rules would place the pairs on the opposite sides. **Always confirm which labeling convention a diagram uses before interpreting it.**

---

## 7. How to Determine Cardinality and Ordinality

For **any two entities** A and B, use this method:

### Step 1 — Find the maximum

Take **one A** and ask:

> How many B instances can it be associated with at most?

Answer: **one** (`1`) or **many** (`M`).

### Step 2 — Find the minimum

Take that **same A** and ask:

> Must it be associated with at least one B, or can it be associated with none?

Answer: **required** (`1`) or **optional** (`0`).

### Step 3 — Write the result

Combine the answers into **`(Min, Max)`**.

### Step 4 — Reverse the direction

Now take **one B** and repeat the same two questions about A.

> **Reminder:** Do not assume the rules are the same in both directions.

---

## 8. Additional Practice Examples

These are **extra examples for practice**, not diagrams from the slides.

| Business rule | Starting instance | Related instances | Min–Max |
|---|---|---|---|
| An employee may have no assigned parking spot, but at most one | Employee | ParkingSpot | `(0,1)` |
| Each order must belong to exactly one customer | Order | Customer | `(1,1)` |
| A customer may have no orders or many orders | Customer | Order | `(0,M)` |
| Each department must have at least one employee and can have many | Department | Employee | `(1,M)` |

---

## 9. Cardinality vs. Ordinality — Quick Comparison

| Feature | Cardinality | Ordinality |
|---|---|---|
| Main idea | **Maximum** participation | **Minimum** participation |
| Question | “How many at most?” | “Is at least one required?” |
| Common values | `1`, `M` | `0`, `1` |
| Describes | One vs. many | Optional vs. mandatory |
| Position in `(Min, Max)` | Second | First |

---

## 10. Important Terms

| Term | Meaning |
|---|---|
| **Cardinality** | Maximum number of related instances, in this course's terminology |
| **Ordinality** | Minimum number of related instances, in this course's terminology |
| **Minimum Participation** | Smallest allowed number of related instances |
| **Maximum Participation** | Largest allowed number of related instances |
| **Optional Participation** | Minimum is `0` |
| **Mandatory Participation** | Minimum is `1` |
| **Min–Max Notation** | A pair such as `(0,M)` or `(1,1)` |
| **One-to-Many (`1:M`)** | One instance on one side may relate to many on the other |
| **Many-to-Many (`M:M`)** | Instances on both sides may relate to many |
| **Business Rule** | A condition or requirement that determines how the relationship works |

---

## 11. Quick Review Questions

1. What is the difference between **cardinality** and **ordinality**?
2. What does **`(0,M)`** mean?
3. What does **`(1,1)`** mean?
4. Can a student have **zero** course enrollments in the slide's example?
5. Can an order belong to **two customers** under the lesson's business rule?
6. Why must we read a relationship **from both directions**?

---

## 12. Key Takeaway

**Cardinality = Maximum**  
**Ordinality = Minimum**

```text
(Min, Max)
```

- `(0,1)` = Optional One
- `(1,1)` = Mandatory One
- `(0,M)` = Optional Many
- `(1,M)` = Mandatory Many

**Think in questions rather than memorized diagrams:** For one instance, *how many related instances are allowed at most, and how many are required at minimum?*

---

*Based on the course slides: “Cardinality vs. Ordinality.”*
