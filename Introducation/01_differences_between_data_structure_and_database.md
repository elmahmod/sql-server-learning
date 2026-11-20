# Differences Between Data Structures and Databases

## 1. What Is a Data Structure?

A **data structure** is a way of organizing and storing data in a program so that it can be accessed and modified efficiently.

Common examples of data structures include:

- Array
- Linked List
- Stack
- Queue
- Heap
- Binary Tree
- Graph

Data structures help programmers work with data efficiently and reduce the complexity of certain operations.

## 2. What Is a Database?

A **database** is an organized collection of data that can be stored, accessed, and managed.

In a **relational database**, data is usually organized into **tables** consisting of **rows** and **columns**.

A **Database Management System (DBMS)** is software used to define, store, modify, retrieve, and manage data in a database.

Examples of database management systems include:

- Microsoft SQL Server
- MySQL
- Oracle Database
- Microsoft Access

## 3. Data Structures vs. Databases

| Comparison | Data Structures | Databases |
|---|---|---|
| **Where data is stored** | Typically in the program's memory (RAM) while it runs | Commonly stored persistently on a disk or other storage system |
| **Data lifetime** | Often temporary; in-memory data is lost when the program ends unless saved | Usually persistent; data remains available after the program ends |
| **Organization** | Specific structures used to organize data, such as arrays, lists, and trees | An organized collection of related data; relational databases use tables with rows and columns |
| **Main purpose** | Enable efficient access, modification, and processing of data | Enable reliable storage, retrieval, updating, and management of data |
| **How data is handled** | Through programming-language operations and algorithms (e.g., C++, Java, Python) | Through a DBMS; relational databases commonly use SQL |
| **Examples** | Array, Linked List, Stack, Queue, Tree, Graph | MySQL, Oracle Database, Microsoft SQL Server, MongoDB* |

## 4. Simple Example

Imagine a **Student Management System**:

- A **data structure**, such as a list or array, can hold students in memory while the application is running.
- A **database** can store the students' records so they remain available when the application is closed and reopened.

**In short:** A data structure describes **how data is organized for processing**, while a database is designed to **store and manage a collection of data**.

## 5. Important Clarifications

The comparison above describes common use cases, not absolute rules:

- Data structures are **not limited to RAM**; they can also be used in persistent storage systems.
- Databases are **not always relational tables**; non-relational databases exist too.
- SQL is primarily used with **relational databases**. **MongoDB**, for example, is a document database and does not use SQL as its default query language.
- Products such as MySQL and Microsoft SQL Server are **DBMSs**, rather than individual databases.

---

*Study notes based on the course slides: “Data Structure vs Database”.*
