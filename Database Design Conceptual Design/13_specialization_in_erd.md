# 13 - Specialization in ERD

## 1. What Is Specialization?

**Specialization** is the process of dividing a **higher-level entity (supertype)** into more specific **lower-level entities (subtypes)** based on their characteristics.

It follows a **top-down approach**:

1. Start with a general entity.
2. Identify groups that have additional, specific characteristics.
3. Create specialized sub-entities for those groups.

A specialized entity **IS-A** kind of its parent entity.

---

## 2. Example from the Lecture

Start with a general entity called **Person**.

**Person (supertype)** has common attributes:
- `PersonID` (identifier)
- `Name` — a composite attribute made of `FirstName` and `LastName`
- `BirthDate`
- `Age` — a derived attribute

Specialize **Person** into:

| Subtype | Its specific attributes |
| --- | --- |
| `Student` | `StudentID`, `RegNumber` |
| `Employee` | `EmpID`, `Salary` |

Then specialize **Employee** further into:

| Subtype | Its specific attributes |
| --- | --- |
| `Teacher` | `TeacherID`, `Section` |
| `Developer` | `DevID`, `ProgLang` |
| `Secretary` | `SecID`, `TypingSpeed` |

> **Note:** These identifiers are shown as separate attributes in the lecture's *conceptual* diagram. When mapping the hierarchy to actual database tables, the key and foreign-key structure depends on the chosen mapping strategy; a subtype often uses the parent entity's key as its own primary key and foreign key.

---

## 3. Specialization ER Diagram

![ERD specialization](Diagrams\png\Specialization_erd_teacher_developer_to_employe.png)

### Reading the IS-A Relationships

- `Student` **IS-A** `Person`.
- `Employee` **IS-A** `Person`.
- `Teacher` **IS-A** `Employee`.
- `Developer` **IS-A** `Employee`.
- `Secretary` **IS-A** `Employee`.

For example, a **Teacher** is an **Employee**, and an **Employee** is a **Person**. This creates a multi-level specialization hierarchy.

---

## 4. Why Use Specialization?

- **Organization:** Represent distinct categories clearly.
- **Reusability:** Keep common attributes in the general entity.
- **Less duplication:** Avoid repeating the same attributes for every category.
- **Flexibility:** Add subtype-specific attributes and relationships without placing them in every entity.

---

## 5. Specialization vs. Generalization

| Specialization | Generalization |
| --- | --- |
| **Top-down** approach | **Bottom-up** approach |
| Starts with one general entity | Starts with multiple specific entities |
| Divides it into subtypes | Extracts their common attributes into a supertype |
| Example: `Person` → `Student`, `Employee` | Example: `Student`, `Employee` → `Person` |

Both can lead to the **same final ER diagram**. The difference is the direction used to design it.

---

## 6. Connection to OOP Inheritance

If you studied **inheritance in C#**, the idea will be familiar:

```csharp
class Person
{
    public string Name { get; set; }
    public DateTime BirthDate { get; set; }
}

class Student : Person
{
    public string RegNumber { get; set; }
}

class Employee : Person
{
    public decimal Salary { get; set; }
}

class Teacher : Employee
{
    public string Section { get; set; }
}
```

**Similarity:** Both express **IS-A** relationships and place common features in a parent.

**Difference:**
- **OOP inheritance** defines classes, objects, properties, and behavior (methods).
- **ERD specialization** models entities, attributes, and relationships in a data model.

---

## 7. Key Takeaways

- **Specialization = general entity → more specific entities.**
- It is a **top-down** process.
- Subtypes represent an **IS-A relationship** with their parent entity.
- One subtype can be specialized again, creating multiple levels.
- Specialization and generalization are closely related, but their design directions are opposite.

---

**GitHub image note:** Keep `13_specialization_in_erd.md` and `13_specialization_erd.png` in the same folder. The relative image link above will then work automatically.
