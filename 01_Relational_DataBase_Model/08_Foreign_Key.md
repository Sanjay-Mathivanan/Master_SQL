# Foreign Key

# Introduction

In the previous chapter, you learned about the **Primary Key** and **Composite Key**. While a Primary Key uniquely identifies records within a table, a **Foreign Key** is used to **connect two or more tables**.

A Foreign Key creates relationships between tables and ensures that the data remains consistent. It is one of the most important concepts in relational databases because real-world applications rarely store all information in a single table.

For example:

* A student belongs to a department.
* An employee works in a department.
* An order belongs to a customer.

These relationships are created using **Foreign Keys**.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand what a Foreign Key is.
* Learn why Foreign Keys are required.
* Create Foreign Keys using SQL.
* Understand referential integrity.
* Differentiate Foreign Key from Primary Key.
* Answer interview questions related to Foreign Keys.

---

# Problem Statement

Consider the following two tables.

## Department Table

| DepartmentID | DepartmentName   |
| ------------ | ---------------- |
| D101         | Computer Science |
| D102         | Electronics      |
| D103         | Mechanical       |

## Student Table

| StudentID | Name    | DepartmentID |
| --------- | ------- | ------------ |
| 101       | Alice   | D101         |
| 102       | Bob     | D102         |
| 103       | Charlie | D101         |

How does the database know which department each student belongs to?

The answer is the **DepartmentID** column in the **Student** table.

This column references the **Primary Key** of the **Department** table and is called the **Foreign Key**.

---

# Why Do We Need a Foreign Key?

Without Foreign Keys:

* Invalid relationships may be created.
* Data inconsistency can occur.
* Duplicate information increases.
* Orphan records may exist.
* Data integrity cannot be maintained.

Foreign Keys solve these problems by ensuring that related records exist in the parent table.

---

# Definition

A **Foreign Key** is a column or a combination of columns in one table that **references the Primary Key (or a UNIQUE Key) of another table**.

It creates a relationship between two tables and enforces **Referential Integrity**.

---

# Characteristics of a Foreign Key

* Creates relationships between tables.
* References a Primary Key or UNIQUE Key.
* Prevents invalid references.
* Can contain duplicate values.
* May contain NULL values (unless restricted).
* A table can have multiple Foreign Keys.

---

# SQL Syntax

## Creating Tables with a Foreign Key

```sql
CREATE TABLE Department (
    DepartmentID VARCHAR(10) PRIMARY KEY,
    DepartmentName VARCHAR(100)
);

CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(100),
    DepartmentID VARCHAR(10),
    FOREIGN KEY (DepartmentID)
    REFERENCES Department(DepartmentID)
);
```

---

## Adding a Foreign Key to an Existing Table

```sql
ALTER TABLE Student
ADD CONSTRAINT FK_Department
FOREIGN KEY (DepartmentID)
REFERENCES Department(DepartmentID);
```

---

# Example

## Department Table

| DepartmentID | DepartmentName   |
| ------------ | ---------------- |
| D101         | Computer Science |
| D102         | Electronics      |
| D103         | Mechanical       |

## Student Table

| StudentID | Name    | DepartmentID |
| --------- | ------- | ------------ |
| 101       | Alice   | D101         |
| 102       | Bob     | D102         |
| 103       | Charlie | D101         |

Relationship:

* Student **101** belongs to **Computer Science**.
* Student **102** belongs to **Electronics**.
* Student **103** belongs to **Computer Science**.

---

# Internal Working

```text
Department Table
(Parent Table)

DepartmentID
      │
      │ Referenced By
      ▼
Student Table
(Child Table)

DepartmentID
```

When inserting a new student:

```text
Insert Student
      │
      ▼
Check DepartmentID
      │
      ├── Exists in Department Table?
      │          │
      │          ├── Yes → Insert Record
      │          │
      │          └── No → Reject Record
```

---

# Referential Integrity

**Referential Integrity** ensures that every Foreign Key value must exist in the referenced table.

### Valid Example

## Department Table

| DepartmentID |
| ------------ |
| D101         |
| D102         |

## Student Table

| StudentID | DepartmentID |
| --------- | ------------ |
| 101       | D101         |
| 102       | D102         |

The relationship is valid because every DepartmentID exists.

---

### Invalid Example

## Student Table

| StudentID | DepartmentID |
| --------- | ------------ |
| 101       | D999         |

The value **D999** does not exist in the Department table.

The database rejects this record.

---

# Parent Table and Child Table

| Parent Table               | Child Table              |
| -------------------------- | ------------------------ |
| Contains the Primary Key   | Contains the Foreign Key |
| Referenced by other tables | References another table |
| Example: Department        | Example: Student         |

---

# Foreign Key vs Primary Key

| Primary Key                    | Foreign Key                            |
| ------------------------------ | -------------------------------------- |
| Uniquely identifies each row   | References a Primary Key or UNIQUE Key |
| Cannot contain NULL values     | May contain NULL values                |
| Only one Primary Key per table | Multiple Foreign Keys can exist        |
| Prevents duplicate rows        | Creates relationships between tables   |

---

# Real-World Examples

| Application         | Parent Table | Child Table | Foreign Key  |
| ------------------- | ------------ | ----------- | ------------ |
| Student Management  | Department   | Student     | DepartmentID |
| Banking System      | Customer     | Account     | CustomerID   |
| Online Shopping     | Customer     | Orders      | CustomerID   |
| Library Management  | Member       | Borrow      | MemberID     |
| Hospital Management | Doctor       | Appointment | DoctorID     |

---

# Advantages

* Maintains referential integrity.
* Prevents invalid data.
* Reduces data redundancy.
* Connects related tables.
* Improves database consistency.

---

# Limitations

* Inserts depend on parent records.
* Deleting parent records may require additional handling.
* Too many relationships can make database design more complex.

---

# Common Mistakes

* Referencing a column that is not a Primary Key or UNIQUE Key.
* Inserting a Foreign Key value that does not exist.
* Deleting parent records without considering child records.
* Confusing Primary Key with Foreign Key.

---

# Best Practices

* Always define Foreign Keys for related tables.
* Use meaningful column names.
* Choose appropriate actions such as `ON DELETE CASCADE` or `ON DELETE SET NULL` when required.
* Index Foreign Key columns in large tables for better query performance.
* Maintain referential integrity at the database level instead of relying only on application code.

---

# Interview Questions

### 1. What is a Foreign Key?

**Answer:** A Foreign Key is a column or combination of columns that references the Primary Key or UNIQUE Key of another table.

---

### 2. Can a table have multiple Foreign Keys?

**Answer:** Yes. A table can have multiple Foreign Keys.

---

### 3. Can a Foreign Key contain duplicate values?

**Answer:** Yes. Multiple rows can reference the same parent record.

---

### 4. Can a Foreign Key contain NULL values?

**Answer:** Yes, unless the column is defined as `NOT NULL`.

---

### 5. What is Referential Integrity?

**Answer:** Referential Integrity ensures that every Foreign Key value refers to an existing record in the parent table.

---

# Practice Questions

## Easy

1. Define a Foreign Key.
2. Why do we use a Foreign Key?
3. Can a Foreign Key contain duplicate values?
4. Can a table have multiple Foreign Keys?
5. What is a parent table?

## Medium

1. Differentiate Primary Key and Foreign Key.
2. Explain Referential Integrity with an example.
3. Create a Student and Department table using a Foreign Key.
4. What happens if a Foreign Key references a non-existing value?
5. Explain parent and child tables.

## Hard

1. Design Foreign Key relationships for a Hospital Management System.
2. Explain `ON DELETE CASCADE` and `ON DELETE SET NULL`.
3. Compare Foreign Key and Composite Key.
4. Design relationships for an Online Shopping database.
5. Explain how Foreign Keys help database normalization.

---

# Key Takeaways

* A Foreign Key creates relationships between tables.
* It references the Primary Key or UNIQUE Key of another table.
* Foreign Keys enforce Referential Integrity.
* They prevent invalid references and improve data consistency.
* Foreign Keys are fundamental to relational database design.

---

# Conclusion

A Foreign Key is the foundation of relationships in a relational database. By connecting related tables and enforcing referential integrity, it ensures that data remains accurate, consistent, and reliable. Mastering Foreign Keys is essential for designing normalized databases, writing effective SQL queries, and building real-world database applications.
