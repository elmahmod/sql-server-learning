# University ERD Example

This example illustrates a conceptual **Entity–Relationship Diagram (ERD)** for a university system.

## ER Diagram

[Edit University ERD](drawio%20extensions/UniversityERD.drawio)

## Main Entities

- **Student** — represents a student at the university.
- **Course** — represents a course offered by the university.
- **Professor** — represents a university professor.

## Relationships

| Relationship | Entities | Description |
|---|---|---|
| **Enrolled** | Student ↔ Course | A student can enroll in multiple courses, and a course can have multiple students. |
| **Mentor** | Student ↔ Professor | Each student has one mentor; a professor can mentor multiple students. |
| **Teaches** | Professor ↔ Course | A professor can teach at most one course, and a course can have at most one professor, according to the example's requirements. |

> **Note:** The descriptions above follow the university requirements from the lesson. Refer to the diagram for the precise notation, attributes, and minimum participation constraints.

## Diagram Files

- [UniversityERD.png](UniversityERD.png) — diagram preview on GitHub.
- [UniversityERD.drawio](UniversityERD.drawio) — editable source for [draw.io](https://app.diagrams.net/).

Keep this Markdown file in the **same folder** as `UniversityERD.png` so the image renders on GitHub.
