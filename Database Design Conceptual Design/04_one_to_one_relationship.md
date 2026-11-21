# One-to-One Relationship (1:1)

## 1. What Is a One-to-One Relationship?

A **one-to-one relationship (1:1)** is a relationship between two entity types in which **each instance of one entity can be associated with at most one instance of the other entity, and vice versa**.

In a Chen-style Entity–Relationship Diagram (ERD), we draw:

- A **rectangle** for each entity.
- A **diamond** for the relationship.
- A **1** near each entity to indicate **1:1 cardinality**.

```text
[Entity A] -- 1 -- <Relationship> -- 1 -- [Entity B]
```

**Important:** `1:1` describes the **maximum number** of related instances. It does not automatically mean that participation is mandatory. Whether each entity *must* participate depends on additional participation rules.

## 2. Examples from the Lesson

The slides illustrate one-to-one relationships with the following examples. Each example assumes the stated rules for that particular system.

### Example 1: Student and Identification Card

- **Entities:** `Student`, `IdentificationCard`
- **Relationship:** `Has`
- **Cardinality:** `1:1`

```text
[Student] -- 1 -- <Has> -- 1 -- [IdentificationCard]
```

**Rule in the lesson:** Each student has one identification card, and each identification card belongs to one student.

### Example 2: Student and Person

- **Entities:** `Student`, `Person`
- **Label in the slide:** `Is a`

```text
[Student] -- 1 -- <Is a> -- 1 -- [Person]
```

The slide uses this to illustrate a one-to-one association: a particular student corresponds to a particular person.

**Modeling note:** In formal ER modeling, **“Student is a Person”** is typically represented as a **subtype/supertype (`IS-A`) relationship**, not merely an ordinary `1:1` relationship. The same distinction applies to the next example.

### Example 3: Employee and Person

- **Entities:** `Employee`, `Person`
- **Label in the slide:** `Is a`

```text
[Employee] -- 1 -- <Is a> -- 1 -- [Person]
```

**Meaning:** An employee is a person. This is normally a specialization/generalization concept, although the slide includes it among the one-to-one examples.

### Example 4: Member and Book

- **Entities:** `Member`, `Book`
- **Relationship:** `Borrow`
- **Cardinality shown:** `1:1`

```text
[Member] -- 1 -- <Borrow> -- 1 -- [Book]
```

**Rule in the lesson:** A member can borrow only one book, and a book can be borrowed by only one member.

**Modeling note:** This is a simplified rule for this example. A real library may allow members to borrow multiple books over time, so its design could be different.

### Example 5: Traveler and Seat

- **Entities:** `Traveler`, `Seat`
- **Relationship in the slide:** `Set` (seat assignment)
- **Cardinality:** `1:1`

```text
[Traveler] -- 1 -- <Assigned to> -- 1 -- [Seat]
```

**Rule in the lesson:** A traveler is assigned one seat, and that seat is assigned to one traveler. In practice, this should be understood **within a specific trip or booking**.

### Example 6: Employee and Desk

- **Entities:** `Employee`, `Desk`
- **Relationship in the slide:** `Set` (desk assignment)
- **Cardinality:** `1:1`

```text
[Employee] -- 1 -- <Assigned to> -- 1 -- [Desk]
```

**Rule in the lesson:** An employee is assigned one desk, and a desk is assigned to one employee.

### Example 7: Employee and Phone Extension

- **Entities:** `Employee`, `PhoneExtension`
- **Relationship:** `Extension`
- **Cardinality:** `1:1`

```text
[Employee] -- 1 -- <Extension> -- 1 -- [PhoneExtension]
```

**Rule in the lesson:** Each employee has a specific phone extension, and each extension reaches only one employee.

### Example 8: Employee and Task

- **Entities:** `Employee`, `Task`
- **Relationship:** `Assigned`
- **Cardinality:** `1:1`

```text
[Employee] -- 1 -- <Assigned> -- 1 -- [Task]
```

**Rule in the lesson:** An employee works on one task, and that task is assigned to one employee.

**Modeling note:** Many actual task-management systems allow one employee to have several tasks, so this is a hypothetical one-to-one rule rather than a universal fact.

## 3. How to Recognize a 1:1 Relationship

Ask these two questions:

1. Can one instance of **Entity A** be related to **more than one** instance of Entity B?
2. Can one instance of **Entity B** be related to **more than one** instance of Entity A?

If the answer to **both** is **no**, the relationship's maximum cardinality is **one-to-one (1:1)**.

For example, under the identification-card rule:

- One student → at most one card.
- One card → at most one student.

Therefore, the relationship is `1:1`.

## 4. Cardinality vs. Participation

These concepts are related but different:

| Concept | Question | Example |
|---|---|---|
| **Cardinality** | How many related instances are allowed? | At most one card per student (`1:1`). |
| **Participation / Optionality** | Is a related instance required? | Must every student already have a card, or can a new student have none yet? |

A one-to-one relationship may be **optional** on one side or both sides, depending on the business requirements.

## 5. Quick Review of the Lesson Examples

| Entity A | Relationship | Entity B | Stated maximum cardinality |
|---|---|---|---|
| Student | Has | Identification Card | `1:1` |
| Student | Is a | Person | `1:1` in slide; usually modeled as subtype/supertype |
| Employee | Is a | Person | `1:1` in slide; usually modeled as subtype/supertype |
| Member | Borrow | Book | `1:1` (under the given rule) |
| Traveler | Seat assignment | Seat | `1:1` (per trip/booking) |
| Employee | Desk assignment | Desk | `1:1` (under the given rule) |
| Employee | Extension | Phone Extension | `1:1` |
| Employee | Assigned | Task | `1:1` (under the given rule) |

## 6. Important Terms

| Term | Meaning |
|---|---|
| **One-to-One Relationship** | Each entity instance is related to at most one instance on the other side. |
| **1:1 Cardinality** | One-to-one maximum relationship cardinality. |
| **Entity** | An object or concept about which data is stored. |
| **Relationship** | An association between entity types. |
| **Participation** | Whether an entity must participate in a relationship. |
| **Optionality** | Whether a relationship can be absent. |
| **Subtype / Supertype (IS-A)** | A specialization relationship, such as Student **is a** Person. |

## 7. Key Takeaway

**One-to-One (`1:1`) means one instance on either side can be related to no more than one instance on the opposite side.**

Always decide cardinality based on the **business rules of the system**, not just the names of the entities.

---

*Study notes based on the course slides: “One-to-One Relationship.”*
