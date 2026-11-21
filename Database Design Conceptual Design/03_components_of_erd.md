# Components of ERD

## Overview

An **Entity–Relationship Diagram (ERD)** is based on three main concepts:

1. **Entities**
2. **Attributes**
3. **Relationships**

These components help describe what information a database should represent and how its parts are connected before implementation.

## 1. Entities

An **entity** is a person, object, event, or concept about which we want to store information.

The lesson identifies two types:

| Type | Description | Example |
|---|---|---|
| **Entity (Strong Entity)** | Can be identified independently using its own key attribute(s). | `Student`, identified by `StudentID` |
| **Weak Entity** | Depends on an owner entity for identification; it cannot be uniquely identified by its own attributes alone. | `OrderItem`, identified using an `Order` and an item number |

## 2. Attributes

An **attribute** describes an entity (and sometimes a relationship).

The lesson introduces the following categories:

| Type | Description | Example |
|---|---|---|
| **Attribute** | A property describing an entity. | Student's `Gender` |
| **Key Attribute** | An attribute used to uniquely identify an entity. | `StudentID` |
| **Composite Attribute** | An attribute divided into meaningful subparts. | `Name` → `First`, `Middle`, `Last` |
| **Multivalued Attribute** | An attribute that can have several values for one entity. | Student's phone numbers |
| **Derived Attribute** | An attribute whose value can be calculated from other information. | `Age` from `BirthDate` |

### Symbols used in the preceding lesson

- **Oval:** attribute
- **Underlined attribute name:** key attribute
- **Oval with connected smaller ovals:** composite attribute
- **Double oval:** multivalued attribute
- **Dashed oval:** derived attribute

## 3. Relationships

A **relationship** describes an association between entities.

The lesson lists four relationship cardinalities:

| Type | Notation | Meaning | Example |
|---|---|---|---|
| **One-to-One** | `1 : 1` | One instance of an entity is associated with at most one instance of another. | A person and a single assigned locker |
| **One-to-Many** | `1 : M` | One instance can be associated with many instances of another. | One department has many employees |
| **Many-to-One** | `M : 1` | Many instances can be associated with one instance of another. | Many employees belong to one department |
| **Many-to-Many** | `M : M` | Many instances on either side can be associated with many on the other side. | Students enroll in courses |

> **Note:** One-to-many and many-to-one describe the same kind of association from opposite directions. The examples illustrate possible business rules, not rules that apply to every system.

## 4. Quick Example: University Database

Consider these entities:

- **Student** — attributes: `StudentID`, `Name`, `BirthDate`
- **Course** — attributes: `CourseID`, `Name`, `CreditHours`
- **Professor** — attributes: `ProfessorID`, `Name`

Possible relationships:

- A **Student** *enrolls in* **Courses** — `M : M`.
- A **Professor** *mentors* **Students** — `1 : M` when viewed from professor to students.

This shows how **entities**, **attributes**, and **relationships** work together in a single ERD.

## 5. Quick Summary

| Component | Main question it answers |
|---|---|
| **Entity** | What things do we need to store data about? |
| **Attribute** | What information describes each thing? |
| **Relationship** | How are those things connected? |
| **Cardinality** | How many instances can participate in a relationship? |

**Key takeaway:** An ERD is built around **entities, attributes, and relationships**. The detailed types help make the conceptual database design precise.

---

*Study notes based on the course slide: “Components of ER Diagram.”*
