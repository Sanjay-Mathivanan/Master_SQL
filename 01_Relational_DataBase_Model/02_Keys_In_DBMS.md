# Keys in DBMS

# Introduction

In a relational database, data is stored in multiple tables. To uniquely identify records and establish relationships between tables, we use **Keys**.

Keys are one of the most important concepts in database design because they help maintain **data integrity**, **prevent duplicate records**, and **connect related tables**.

Every well-designed database uses one or more types of keys.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand what a key is.
* Learn why keys are required in a database.
* Differentiate between different types of keys.
* Understand how keys establish relationships between tables.
* Solve interview questions related to DBMS keys.

---

# Problem Statement

Consider a student database.

| StudentID | Name    | Department |
| --------- | ------- | ---------- |
| 101       | Alice   | CSE        |
| 102       | Bob     | ECE        |
| 101       | Charlie | IT         |

Here, two students have the same **StudentID**, making it impossible to uniquely identify a student.

To solve this problem, databases use **Keys**.

---

# Why Do We Need Keys?

Without keys:

* Duplicate records may exist.
* Data retrieval becomes unreliable.
* Relationships between tables cannot be maintained.
* Data integrity is lost.

Keys solve these problems by ensuring every record can be uniquely identified.

---

# Definition

A **Key** is one or more columns used to uniquely identify a row in a table or establish relationships between tables.

---

# Types of Keys

* Super Key
* Candidate Key
* Primary Key
* Alternate Key
* Composite Key
* Foreign Key
* Unique Key
* Surrogate Key
* Natural Key

---

# Sample Tables

## Student

| StudentID | Name    | DepartmentID |
| --------- | ------- | ------------ |
| 101       | Alice   | D01          |
| 102       | Bob     | D02          |
| 103       | Charlie | D01          |

## Department

| DepartmentID | DepartmentName   |
| ------------ | ---------------- |
| D01          | Computer Science |
| D02          | Electronics      |

---

# ASCII Diagram

```text
Department
+-------------------+
| DepartmentID (PK) |
+-------------------+
          ▲
          │
          │
Student
+---------------------+
| StudentID (PK)      |
| DepartmentID (FK)   |
+---------------------+
```

---

# 1. Super Key

## Definition

A **Super Key** is any column or combination of columns that can uniquely identify a record.

### Example

Student Table

| StudentID | Email                                     | Name  |
| --------- | ----------------------------------------- | ----- |
| 101       | [alice@gmail.com](mailto:alice@gmail.com) | Alice |
| 102       | [bob@gmail.com](mailto:bob@gmail.com)     | Bob   |

Possible Super Keys:

* StudentID
* Email
* StudentID + Name
* StudentID + Email

### Important Point

A Super Key may contain **extra unnecessary columns**.

---

# 2. Candidate Key

## Definition

A **Candidate Key** is the smallest possible Super Key.

It contains **only the required columns** to uniquely identify a row.

### Example

Candidate Keys:

* StudentID
* Email

Both uniquely identify a student.

---

# Comparison

| Super Key                      | Candidate Key      |
| ------------------------------ | ------------------ |
| May contain extra columns      | No extra columns   |
| Multiple possible combinations | Minimal unique key |
| Not necessarily minimal        | Always minimal     |

---

# 3. Primary Key

## Definition

A **Primary Key** is the Candidate Key selected to uniquely identify every row.

### Rules

* Cannot contain NULL values.
* Must be unique.
* Only one Primary Key per table.

### Example

| StudentID (Primary Key) | Name  |
| ----------------------- | ----- |
| 101                     | Alice |
| 102                     | Bob   |

---

# 4. Alternate Key

## Definition

Candidate Keys that are **not selected** as the Primary Key are called Alternate Keys.

### Example

Candidate Keys:

* StudentID ✅ Primary Key
* Email ✅ Alternate Key

---

# 5. Composite Key

## Definition

A Composite Key consists of **two or more columns** that together uniquely identify a record.

### Example

Attendance Table

| StudentID | SubjectID | Attendance |
| --------- | --------- | ---------- |
| 101       | CS101     | Present    |
| 101       | CS102     | Absent     |

Here,

**StudentID + SubjectID** forms the Composite Key.

---

# 6. Foreign Key

## Definition

A **Foreign Key** is a column that references the Primary Key of another table.

It creates a relationship between tables.

### Example

Department Table

| DepartmentID | DepartmentName   |
| ------------ | ---------------- |
| D01          | Computer Science |
| D02          | Electronics      |

Student Table

| StudentID | Name  | DepartmentID |
| --------- | ----- | ------------ |
| 101       | Alice | D01          |
| 102       | Bob   | D02          |

Here,

**DepartmentID** in the Student table is the Foreign Key.

---

# Relationship Flow

```text
Department Table
      │
Primary Key
      │
      ▼
Foreign Key
      │
Student Table
```

---

# 7. Unique Key

## Definition

A **Unique Key** ensures that all values in a column are unique.

Unlike a Primary Key, a Unique Key may allow NULL values (behavior depends on the database system).

### Example

| EmployeeID | Email (Unique)                    |
| ---------- | --------------------------------- |
| 1          | [a@gmail.com](mailto:a@gmail.com) |
| 2          | [b@gmail.com](mailto:b@gmail.com) |

---

# 8. Surrogate Key

## Definition

A Surrogate Key is an **artificially generated key** that has no business meaning.

### Example

| CustomerID | Name  |
| ---------- | ----- |
| 1          | Alice |
| 2          | Bob   |

CustomerID is generated automatically.

Examples include:

* AUTO_INCREMENT (MySQL)
* IDENTITY (SQL Server)
* SERIAL / IDENTITY (PostgreSQL)

---

# 9. Natural Key

## Definition

A Natural Key is a real-world attribute that naturally identifies a record.

### Examples

* Passport Number
* Aadhaar Number
* Email Address
* Vehicle Registration Number

---

# Comparison Table

| Key Type      | Unique | NULL Allowed  | Purpose                     |
| ------------- | ------ | ------------- | --------------------------- |
| Super Key     | Yes    | Depends       | Uniquely identifies rows    |
| Candidate Key | Yes    | No            | Minimal Super Key           |
| Primary Key   | Yes    | No            | Main identifier             |
| Alternate Key | Yes    | No            | Candidate Key not chosen    |
| Composite Key | Yes    | No            | Multiple columns together   |
| Foreign Key   | No     | Yes (depends) | Creates relationships       |
| Unique Key    | Yes    | Depends       | Prevents duplicates         |
| Surrogate Key | Yes    | No            | System-generated identifier |
| Natural Key   | Yes    | Depends       | Real-world identifier       |

---

# Real-World Example

**Online Shopping Database**

| Table      | Primary Key | Foreign Key        |
| ---------- | ----------- | ------------------ |
| Customer   | CustomerID  | —                  |
| Product    | ProductID   | —                  |
| Orders     | OrderID     | CustomerID         |
| OrderItems | OrderItemID | OrderID, ProductID |

---

# Common Mistakes

* Confusing Primary Key with Unique Key.
* Assuming every unique column is a Primary Key.
* Using unnecessary columns in a Composite Key.
* Forgetting to create Foreign Keys between related tables.
* Using business data that frequently changes as a Primary Key.

---

# Best Practices

* Use simple Primary Keys.
* Define Foreign Keys to maintain referential integrity.
* Avoid updating Primary Key values.
* Prefer Surrogate Keys when Natural Keys are long or change frequently.
* Choose meaningful Candidate Keys during database design.

---

# Interview Questions

### 1. What is the difference between a Super Key and a Candidate Key?

**Answer:** A Super Key uniquely identifies a row but may contain extra columns. A Candidate Key is the minimal Super Key.

---

### 2. Can a table have multiple Candidate Keys?

**Answer:** Yes.

---

### 3. Can a table have multiple Primary Keys?

**Answer:** No. A table can have only one Primary Key.

---

### 4. What is the purpose of a Foreign Key?

**Answer:** It establishes relationships between tables and maintains referential integrity.

---

### 5. What is the difference between a Natural Key and a Surrogate Key?

**Answer:** A Natural Key comes from real-world data, while a Surrogate Key is generated by the system.

---

# Practice Questions

## Easy

1. Define a Primary Key.
2. What is a Candidate Key?
3. Can a Primary Key contain NULL values?
4. What is a Foreign Key?
5. Give two examples of Natural Keys.

## Medium

1. Differentiate between Super Key and Candidate Key.
2. Explain Composite Key with an example.
3. Compare Primary Key and Unique Key.
4. Why are Foreign Keys important?
5. What are Alternate Keys?

## Hard

1. Design keys for a Library Management System.
2. Explain when to use a Surrogate Key instead of a Natural Key.
3. Compare all key types with suitable examples.
4. How do keys improve database performance and integrity?
5. Explain the role of keys in database normalization.

---

# Key Takeaways

* Keys uniquely identify records and connect related tables.
* Every relational database relies on keys for data integrity.
* Primary Keys identify records, while Foreign Keys establish relationships.
* Candidate Keys are minimal Super Keys.
* Choosing the correct key type leads to a well-designed and maintainable database.

---

# Conclusion

Keys are the foundation of relational database design. They ensure uniqueness, maintain relationships, and preserve data integrity across tables. A clear understanding of the different key types is essential for writing efficient SQL queries, designing scalable databases, and succeeding in technical interviews.
