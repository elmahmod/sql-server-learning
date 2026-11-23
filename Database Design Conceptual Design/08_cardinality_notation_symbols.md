# Cardinality Notation Symbols

> **Course:** Database Design — Conceptual Design  
> **Lesson:** Cardinality Notation Symbols (Crow's Foot, Min–Max, and Bachman Notation)

## 1. What Is Cardinality Notation?

**Cardinality notation** is a way to show **how many instances of one entity can be related to an instance of another entity** in an Entity–Relationship Diagram (ERD).

A relationship should tell us **two things**:

- **Minimum participation (Min):** Is the connection optional (`0`) or required (`1`)?
- **Maximum participation (Max):** Can there be only one connection (`1`) or many (`M` / `N` / `*`)?

Together, they describe the **minimum and maximum** number of related instances permitted by the system's business rules.

> **Important lesson note:** Some diagrams presented in class are intentionally questionable or incorrect. **Do not memorize a diagram as a universal fact.** First read the notation, then check whether its relationships match the real-world or system rules. The slides alone do not reveal the instructor's exact spoken critique of every example.

---

## 2. Cardinality vs. Ordinality — Quick Review

| Concept | Meaning | Typical values |
|---|---|---|
| **Cardinality (Max)** | Maximum number of related instances | `1`, `M` |
| **Ordinality (Min)** | Minimum number of required related instances | `0`, `1` |
| **Optional** | A relationship is not required | Minimum `0` |
| **Mandatory** | At least one relationship is required | Minimum `1` |

### Min–Max pairs

| Notation | Meaning | Participation |
|---|---|---|
| `(0,1)` | Zero or one | Optional, at most one |
| `(1,1)` | Exactly one | Mandatory, exactly one |
| `(0,M)` | Zero or many | Optional, many allowed |
| `(1,M)` | One or many | Mandatory, many allowed |

**Read the pair as `(Minimum, Maximum)`.**

---

## 3. Common ERD Notation Styles

The lesson illustrates three styles:

1. **Crow's Foot Notation:** Uses circles, straight bars, and three-pronged ends on relationship lines.
2. **Min–Max Notation:** Uses numeric ranges such as `(0,1)` and `(1,M)`.
3. **Bachman Notation:** Another graphical relationship notation shown on the slides, using distinct endpoint markers.

These are **different visual conventions** for expressing relationship constraints. Symbols must be interpreted according to the notation being used; **do not mix styles without explanation**.

---

## 4. Crow's Foot Notation — The Three Basic Symbols

| Symbol | Meaning | Used for |
|---|---|---|
| Circle `o` | **Zero** | Optional participation |
| Bar `|` | **One** | One / mandatory participation |
| Crow's foot `<` | **Many** | Multiple related instances |

A complete endpoint uses **two markers**: one for the **minimum** and one for the **maximum**.

### Four common endpoint combinations

| Endpoint (illustrative) | Min–Max | Explanation |
|---|---|---|
| `||` | `(1,1)` | One and only one |
| `o|` | `(0,1)` | Zero or one |
| `|<` | `(1,M)` | One or many |
| `o<` | `(0,M)` | Zero or many |

*The `<` character in these text representations stands for the three-pronged crow's-foot shape in a real diagram.*

### A memory trick

- **Circle** answers: *Can it be zero?* → Yes.
- **Bar** answers: *Must it be at least one?* → Yes.
- **Crow's foot** answers: *Can there be many?* → Yes.

---

## 5. How to Read a Crow's Foot Diagram Correctly

**Key rule:** The symbols near an entity tell you **how many instances of that entity can be related to one instance on the opposite side**.

### Example: Customer and Order

Assume these business rules:

- A customer may place **zero or many orders**.
- Every order must belong to **exactly one customer**.

```text
[Customer] || ---------------- o< [Order]
             places
```

Read it **in both directions**:

1. **One customer → how many orders?** `0..M` (look at the symbols near **Order**).
2. **One order → how many customers?** `1..1` (look at the symbols near **Customer**).

Therefore:

- From **Customer to Order**, the maximum cardinality is **1:M**.
- Participation on the **Order** side is optional for a customer (`0..M`).
- The order must have exactly one customer (`1..1`).

> **Avoid this common mistake:** The `(1,1)` shown near `Customer` in a Crow's Foot view describes **how many customers an order has**. It does **not** mean a customer can place only one order.

---

## 6. Example: Student and Course

Assume:

- A student may enroll in **zero or many courses**.
- A course may have **zero or many students**.

```text
[Student] >o ---------------- o< [Course]
            enrolled in
```

Both endpoints mean `(0,M)`:

- One student → zero or many courses.
- One course → zero or many students.

The maximum cardinality is **Many-to-Many (`M:M`)**, with **optional participation on both sides**.

If the university requires each student to enroll in **at least one** course, the minimum for courses per student would change from `0` to `1`. **The maximum can remain `M`.**

---

## 7. Mini Reference: Different Cardinality Combinations

| Business rule | What to draw near Entity B | What to draw near Entity A |
|---|---|---|
| Each A is related to **exactly one B**, and each B to **exactly one A** | `||` | `||` |
| Each A may relate to **zero or many B**, but each B must relate to **exactly one A** | `o<` | `||` |
| Each A must relate to **one or many B**, but each B must relate to **exactly one A** | `|<` | `||` |
| Each A may relate to **zero or many B**, and each B may relate to **zero or many A** | `o<` | `o<` |

Remember: **The marker near B is read when starting from one A**, and vice versa.

---

## 8. Examples from the Slides: Read the Symbols, Then Test the Rules

The slides show several examples. Some may be used to **test whether students can identify incorrect assumptions**. Do not automatically classify a business scenario as correct just because it appears in a diagram.

| Diagram shown | Meaning of the shown notation | What to check |
|---|---|---|
| **Student — Seat** (`||` at both ends) | Every student has exactly one seat; every seat is assigned to exactly one student. | Is this for a specific class/flight/session? Can seats be empty? Can students attend different sessions? |
| **Lecturer — Course** (`||` near Lecturer; `o<` near Course) | One lecturer can teach zero or many courses; every course has exactly one lecturer. | Can a course be taught by multiple lecturers? Can a course exist before an instructor is assigned? |
| **Student — Course** (`o<` at both ends) | A student can take zero or many courses; a course can have zero or many students. | Does the institution require minimum enrollment or a minimum class size? |
| **Teacher — Course** (many/mandatory near Teacher; exactly one near Course) | Under the shown symbols, a course has one or many teachers, while a teacher teaches exactly one course. | Is this really the intended rule? Many schools instead allow one teacher to teach many courses. |
| **Customer — Pizza** (optional many at both ends) | Many-to-many, optional on both sides. | Does `Pizza` mean a *pizza product/type* or a *specific physical pizza*? Should purchases be modeled through `Order` / `OrderItem`? |
| **Painter — Painting** (`1:M` in the slide) | One painter may be associated with many paintings; each painting with one painter under the shown rule. | Can paintings have co-authors? Must every painter have created a painting already? |
| **Employee — Skill** (mandatory many-to-many in the slide) | Every employee has at least one skill, and every skill is associated with at least one employee. | Can a new employee have no recorded skills? Can a skill exist in the catalog even if no employee has it? |
| **Employee — Store** (`1:1` mandatory in the slide) | Every employee manages exactly one store, and every store has exactly one employee manager. | Are *all* employees managers? Can a store temporarily have no manager? Can a manager oversee several stores? |

### Important: “Unrealistic” does not always mean “incorrect”

A relationship is **correct only relative to the business requirements**.

For example:

- **Student — Seat (`1:1`)** can make sense for *assigned seats on one specific trip*.
- But it may be incorrect for *all students and all seats across multiple trips*.

The ERD alone does not tell us the full set of business rules. **Ask what the system is supposed to model.**

---

## 9. Special Discussion: Employee and Store

The slide shows a **mandatory one-to-one** `Employee — manages — Store` relationship.

Read this carefully:

- **One employee manages exactly one store.**
- **One store is managed by exactly one employee.**

Now ask:

1. Does **every employee** have to manage a store?
2. Can a store exist **temporarily without a manager**?
3. Can a manager supervise **more than one store**?

If the real rules say **only some employees are managers**, then making management mandatory for *every* employee is too restrictive.

A possible alternative is:

- An employee manages **zero or one** store.
- Every store has **exactly one** manager.

The correct diagram must reflect the actual requirements, **not a familiar example**.

---

## 10. Special Discussion: Teacher and Course

One screenshot has the **many marker at the Teacher endpoint** and **exactly-one at the Course endpoint**.

That means:

- One **course** can be linked to **one or many teachers**.
- One **teacher** is linked to **exactly one course**.

This may be an intentional example for checking if students can read the diagram correctly.

Do not replace the symbols just because the entity names look familiar. First **read what is drawn**, then ask whether the university's actual rules support it.

---

## 11. How to Detect a Wrong ERD — Four Questions

For any relationship between entities **A** and **B**, ask:

1. **One A → how many B at most?** One or many? (**Max**)
2. **One A → how many B at minimum?** Zero or one? (**Min**)
3. **One B → how many A at most?** One or many? (**Max**)
4. **One B → how many A at minimum?** Zero or one? (**Min**)

Then compare the answers with the **Crow's Foot markers** on **both** ends.

If the diagram conflicts with a business rule, it needs to be corrected.

---

## 12. Practice Questions

For each case, decide the allowed `(Min, Max)` **on both sides**.

### Question A

A customer may create no orders yet, but every order must belong to one customer.

- Orders per customer: `?`
- Customers per order: `?`

### Question B

Every employee must belong to exactly one department. A department may have zero employees.

- Departments per employee: `?`
- Employees per department: `?`

### Question C

Every store must have exactly one manager. An employee may manage zero or one store.

- Managers per store: `?`
- Stores per employee: `?`

### Question D

A course can exist with no enrollments yet, but every student must register for at least one course.

- Courses per student: `?`
- Students per course: `?`

<details>
<summary>Answers — check after trying</summary>

- **A:** Orders per customer `(0,M)`; customers per order `(1,1)`.
- **B:** Departments per employee `(1,1)`; employees per department `(0,M)`.
- **C:** Managers per store `(1,1)`; stores per employee `(0,1)`.
- **D:** Courses per student `(1,M)`; students per course `(0,M)`.

</details>

---

## 13. Important Terms

| Term | Short definition |
|---|---|
| **Cardinality** | Maximum number of related entity instances. |
| **Ordinality** | Minimum required participation, as used in this course. |
| **Crow's Foot Notation** | ERD notation using circles, bars, and crow's-foot markers. |
| **Min–Max Notation** | Numeric notation such as `(0,1)` and `(1,M)`. |
| **Bachman Notation** | Another graphical relationship notation. |
| **Optional Relationship** | Minimum participation is zero. |
| **Mandatory Relationship** | Minimum participation is one. |
| **Business Rule** | A requirement that defines what relationships are allowed. |
| **One-to-One (`1:1`)** | Maximum one on both sides. |
| **One-to-Many (`1:M`)** | Maximum one on one side, many on the other. |
| **Many-to-Many (`M:M`)** | Maximum many on both sides. |

---

## 14. Final Summary

**Crow's Foot symbols:**

- `o` = optional / zero.
- `|` = one.
- Crow's foot = many.

**Min–Max:**

- `(0,1)` = zero or one.
- `(1,1)` = exactly one.
- `(0,M)` = zero or many.
- `(1,M)` = one or many.

**Most important skill:**

> **Do not memorize the relationship by its name. Read both endpoints, then test both directions against the real business rules.**

---

*Study notes based on the provided slides about Cardinality Notation Symbols and Crow's Foot Notation. Some examples may have been used as deliberate mistakes in the video; without the instructor's spoken explanation, the exact intentionally incorrect examples cannot be identified with certainty.*
