# ERD Symbols

> **Database Design — Conceptual Design | Lesson 02**

## 1. What Are ERD Symbols?

**ERD (Entity–Relationship Diagram) symbols** are visual shapes used to represent **entities**, **attributes**, and **relationships** when designing a database.

The course uses **Chen-style ER notation**, where the shape tells us the role of an element in the diagram.

## 2. Main ERD Symbols

| Symbol | Name | Meaning | Example |
|---|---|---|---|
| Rectangle | **Entity** | Represents an entity type about which we store information. | `Student`, `Course`, `Professor` |
| Double rectangle | **Weak Entity** | Represents an entity that depends on another entity for its identification. | An order item identified together with its order |
| Oval / Ellipse | **Attribute** | Represents a property of an entity or relationship. | `Name`, `Gender`, `Birth Date` |
| Double oval | **Multivalued Attribute** | Represents an attribute that can hold multiple values for one entity. | A student's phone numbers |
| Dashed oval | **Derived Attribute** | Represents an attribute calculated from other data. | `Age` derived from `Birth Date` |
| Diamond | **Relationship** | Represents an association between entities. | `Enrolled`, `Mentor`, `Teaches` |
| Line | **Connection** | Connects attributes to entities and entities to relationships. | `Student` connected to `Name` |
| Underlined attribute name | **Key Attribute** | Marks an identifying attribute in the ER model. | Underlined `ID` for `Student` |

## 3. Additional Symbol: Composite Attribute

A **Composite Attribute** is an attribute that can be divided into smaller, meaningful parts.

For example, the `Student` entity may have a `Name` attribute composed of:

- `First`
- `Mid`
- `Last`

In an ERD, draw a **main oval** labeled `Name` and connect it to three **smaller ovals** labeled `First`, `Mid`, and `Last`.

This is different from a **Multivalued Attribute**:

- **Composite:** one value has parts, such as a full name made of first, middle, and last names.
- **Multivalued:** one entity can have several separate values of the same property, such as multiple phone numbers.

## 4. Reading the University ERD Example

The course diagram contains three entities:

| Entity | Attributes shown in the example |
|---|---|
| **Student** | Underlined `ID`, `Gender`, `Birth Date`, `Age` (derived), and `Name` (composite: `First`, `Mid`, `Last`) |
| **Course** | Underlined `ID`, `Name`, `Credit Hours` |
| **Professor** | Underlined `ID`, `Name`, `Salary` |

### Relationships in the Example

| Relationship | Connected entities | Meaning |
|---|---|---|
| **Enrolled** | `Student` and `Course` | A student enrolls in a course. |
| **Mentor** | `Student` and `Professor` | A professor mentors a student. |
| **Teaches** | `Professor` and `Course` | A professor teaches a course. |

The `Enrolled` relationship also has an attribute named **`Enroll. Date`**, which describes when the enrollment occurred. This illustrates that **relationships can have attributes**, not only entities.

### Recognizing the Symbols in This Example

1. The **rectangles** labeled `Student`, `Course`, and `Professor` are entities.
2. The **diamonds** labeled `Enrolled`, `Mentor`, and `Teaches` are relationships.
3. The **ovals** connected to each entity show its attributes.
4. The **underlined `ID`** attributes represent identifying keys.
5. The **dashed oval `Age`** represents a derived attribute.
6. The **`Name` oval with `First`, `Mid`, and `Last`** represents a composite attribute.
7. The **lines** show which attributes and relationships belong together.

## 5. Quick Comparison: Attribute Types

| Attribute type | How it appears | Example |
|---|---|---|
| Simple | Single oval | `Gender` |
| Composite | Main oval connected to component ovals | `Name` → `First`, `Mid`, `Last` |
| Multivalued | Double oval | `Phone Number` (multiple numbers) |
| Derived | Dashed oval | `Age` from `Birth Date` |
| Key | Attribute name underlined | `Student.ID` |

## 6. Quick Review

- **Rectangle** → Entity
- **Double rectangle** → Weak Entity
- **Oval** → Attribute
- **Double oval** → Multivalued Attribute
- **Dashed oval** → Derived Attribute
- **Diamond** → Relationship
- **Line** → Connection
- **Underlined attribute** → Key Attribute
- **Oval divided into connected sub-ovals** → Composite Attribute

### Key Idea

**ERD symbols help us read and design a database conceptually before creating its actual tables in SQL Server.**

---

*Study notes based on the course slides: “ERD Symbols” and “Symbols Used in ER Diagrams.”*
