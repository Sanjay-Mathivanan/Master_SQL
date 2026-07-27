# FOREIGN KEY Constraint

# Introduction

In a relational database, data is often divided into multiple tables to reduce duplication and improve organization. However, these tables must be connected to maintain meaningful relationships.

For example:

* An **Order** must belong to an existing **Customer**.
* An **Employee** must work in an existing **Department**.
* A **Student** must enroll in an existing **Course**.

If these relationships are not enforced, the database may contain invalid records, such as an order belonging to a customer who does not exist.

The **FOREIGN KEY** constraint ensures that relationships between tables remain valid by enforcing **referential integrity**.

In this chapter, you will learn what a `FOREIGN KEY` is, why it is important, how to create it, and how it helps maintain consistent relationships between tables.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand the purpose of the `FOREIGN KEY` constraint.
* Create tables with foreign keys.
* Add foreign keys to existing tables.
* Understand parent and child tables.
* Learn referential integrity.
* Understand `ON DELETE` and `ON UPDATE` actions.
* Follow best practices when designing relational databases.

---

# Problem Statement

Consider the following tables.

## Student Table

| StudentID | Name  |
| --------- | ----- |
| 101       | Rahul |
| 102       | Priya |

## Enrollment Table

| EnrollmentID | StudentID | Course |
| ------------ | --------- | ------ |
| 1            | 101       | SQL    |
| 2            | 999       | Java   |

Problem:

Student **999** does not exist in the **Student** table.

This creates inconsistent data.

The solution is to use a **FOREIGN KEY** constraint.

---

# Why Do We Need a FOREIGN KEY?

A `FOREIGN KEY` helps to:

* Maintain relationships between tables.
* Prevent invalid references.
* Enforce referential integrity.
* Reduce inconsistent data.
* Improve database reliability.

Without foreign keys, related tables can easily become inconsistent.

---

# What is a FOREIGN KEY?

A **FOREIGN KEY** is a column (or combination of columns) in one table that references the **PRIMARY KEY** or a **UNIQUE** key in another table.

The referenced table is called the **Parent Table**.

The table containing the foreign key is called the **Child Table**.

---

# Parent Table vs Child Table

| Parent Table               | Child Table              |
| -------------------------- | ------------------------ |
| Contains the PRIMARY KEY   | Contains the FOREIGN KEY |
| Stores master data         | Stores related data      |
| Referenced by other tables | References another table |

Example:

| Parent Table | Child Table |
| ------------ | ----------- |
| Student      | Enrollment  |

---

# Syntax

## During Table Creation

```sql
CREATE TABLE ParentTable (
    ParentID INT PRIMARY KEY
);

CREATE TABLE ChildTable (
    ChildID INT PRIMARY KEY,
    ParentID INT,
    FOREIGN KEY (ParentID)
    REFERENCES ParentTable(ParentID)
);
```

---

# Example

## Student Table

```sql
CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(100)
);
```

---

## Enrollment Table

```sql
CREATE TABLE Enrollment (
    EnrollmentID INT PRIMARY KEY,
    StudentID INT,
    Course VARCHAR(50),
    FOREIGN KEY (StudentID)
    REFERENCES Student(StudentID)
);
```

---

# Table Relationship

```text
Student
+-----------+-----------+
| StudentID | Name      |
+-----------+-----------+
| 101       | Rahul     |
| 102       | Priya     |
+-----------+-----------+

        ▲
        │
FOREIGN KEY

Enrollment
+--------------+-----------+--------+
| EnrollmentID | StudentID | Course |
+--------------+-----------+--------+
| 1            | 101       | SQL    |
| 2            | 102       | Java   |
+--------------+-----------+--------+
```

---

# Example 1 – Valid Insert

```sql
INSERT INTO Enrollment
VALUES (
    1,
    101,
    'SQL'
);
```

### Result

The record is inserted successfully because **StudentID 101** exists.

---

# Example 2 – Invalid Insert

```sql
INSERT INTO Enrollment
VALUES (
    2,
    999,
    'Java'
);
```

### Result

❌ Error

Reason:

Student **999** does not exist in the parent table.

---

# Adding FOREIGN KEY to an Existing Table

## MySQL

```sql
ALTER TABLE Enrollment
ADD CONSTRAINT FK_Enrollment_Student
FOREIGN KEY (StudentID)
REFERENCES Student(StudentID);
```

---

## PostgreSQL

```sql
ALTER TABLE Enrollment
ADD CONSTRAINT FK_Enrollment_Student
FOREIGN KEY (StudentID)
REFERENCES Student(StudentID);
```

---

## SQL Server

```sql
ALTER TABLE Enrollment
ADD CONSTRAINT FK_Enrollment_Student
FOREIGN KEY (StudentID)
REFERENCES Student(StudentID);
```

---

## SQLite

SQLite supports foreign keys, but they must be enabled.

```sql
PRAGMA foreign_keys = ON;
```

Foreign keys are typically defined during table creation.

---

# Referential Integrity

Referential integrity means:

Every foreign key value must either:

* Match an existing value in the parent table, or
* Be `NULL` (if the foreign key column allows `NULL`).

Example:

| StudentID in Student | StudentID in Enrollment | Valid |
| -------------------- | ----------------------- | :---: |
| 101                  | 101                     |   ✅   |
| 102                  | 102                     |   ✅   |
| —                    | 999                     |   ❌   |
| —                    | NULL                    |   ✅*  |

> *Only if the foreign key column is allowed to contain `NULL`.

---

# ON DELETE Actions

When a parent row is deleted, different actions can occur.

## CASCADE

Deletes related child rows automatically.

```sql
FOREIGN KEY (StudentID)
REFERENCES Student(StudentID)
ON DELETE CASCADE
```

---

## SET NULL

Sets the foreign key value to `NULL`.

```sql
ON DELETE SET NULL
```

---

## RESTRICT / NO ACTION

Prevents deletion if related child records exist.

```sql
ON DELETE RESTRICT
```

---

# ON UPDATE Actions

If the parent key changes, SQL can:

* CASCADE
* SET NULL
* RESTRICT
* NO ACTION

Example:

```sql
ON UPDATE CASCADE
```

---

# Internal Working

```text
User
   │
   ▼
INSERT / UPDATE
   │
   ▼
Database Checks
FOREIGN KEY
   │
   ▼
Referenced Value Exists?
 │
 ├── Yes → Store Data
 │
 └── No → Reject Operation
```

---

# FOREIGN KEY vs PRIMARY KEY

| PRIMARY KEY                  | FOREIGN KEY                     |
| ---------------------------- | ------------------------------- |
| Uniquely identifies each row | References another table        |
| One per table                | Multiple allowed                |
| No `NULL` values             | May allow `NULL` values         |
| Parent table                 | Child table                     |
| Maintains entity integrity   | Maintains referential integrity |

---

# Real-World Applications

| Industry   | Parent Table | Child Table   |
| ---------- | ------------ | ------------- |
| School     | Student      | Enrollment    |
| Banking    | Customer     | Account       |
| Hospital   | Patient      | Appointment   |
| E-Commerce | Customer     | Orders        |
| HR         | Department   | Employee      |
| Library    | Book         | BorrowHistory |

---

# Database Compatibility

| Feature                 | MySQL | PostgreSQL | SQL Server |  SQLite  |
| ----------------------- | :---: | :--------: | :--------: | :------: |
| FOREIGN KEY             |   ✅   |      ✅     |      ✅     |     ✅    |
| ON DELETE CASCADE       |   ✅   |      ✅     |      ✅     |     ✅    |
| ON UPDATE CASCADE       |   ✅   |      ✅     |      ✅     |     ✅    |
| Add Using `ALTER TABLE` |   ✅   |      ✅     |      ✅     | Limited* |

> *SQLite supports foreign keys but has limited support for altering existing table constraints. Recreating the table is often required.

---

# Advantages

* Maintains relationships between tables.
* Prevents invalid references.
* Enforces referential integrity.
* Reduces inconsistent data.
* Improves database reliability.

---

# Limitations

* Can slightly slow insert, update, and delete operations because relationships must be validated.
* Requires proper database design.
* Modifying parent keys may affect child tables.
* Circular references should be avoided.

---

# Common Mistakes

* Creating child records before parent records.
* Forgetting to create a primary key in the parent table.
* Using mismatched data types for parent and child columns.
* Deleting parent rows without considering child records.
* Disabling foreign key checks during development and forgetting to re-enable them.

---

# Best Practices

* Create primary keys before foreign keys.
* Use matching data types for referenced columns.
* Choose appropriate `ON DELETE` and `ON UPDATE` actions.
* Name constraints clearly.
* Avoid unnecessary cascading deletes.
* Keep foreign key relationships simple and meaningful.

---

# Interview Questions

### 1. What is a FOREIGN KEY?

**Answer:** A foreign key is a column (or group of columns) that references the primary key or a unique key of another table to maintain referential integrity.

---

### 2. What is referential integrity?

**Answer:** Referential integrity ensures that every foreign key value either matches an existing value in the parent table or is `NULL` if permitted.

---

### 3. What is the difference between a parent table and a child table?

**Answer:**

| Parent Table                | Child Table              |
| --------------------------- | ------------------------ |
| Contains the referenced key | Contains the foreign key |
| Stores master data          | Stores related data      |

---

### 4. What is `ON DELETE CASCADE`?

**Answer:** It automatically deletes related rows in the child table when the corresponding parent row is deleted.

---

### 5. Can a table have multiple foreign keys?

**Answer:** Yes. A table can reference multiple parent tables using multiple foreign keys.

---

# Practice Questions

## Easy

1. What is a foreign key?
2. What is referential integrity?
3. What is the difference between a parent table and a child table?
4. Can a foreign key reference a primary key?
5. Can a table contain multiple foreign keys?

---

## Medium

1. Create `Student` and `Enrollment` tables with a foreign key.
2. Explain the internal working of a foreign key.
3. Compare `PRIMARY KEY` and `FOREIGN KEY`.
4. Explain `ON DELETE CASCADE`.
5. Explain `ON UPDATE CASCADE`.

---

## Hard

1. Design a university database using foreign keys.
2. Compare foreign key implementation across MySQL, PostgreSQL, SQL Server, and SQLite.
3. Explain the advantages and limitations of foreign keys.
4. Discuss the impact of cascading operations in production databases.
5. Explain how foreign keys help maintain database consistency.

---

# Key Takeaways

* A `FOREIGN KEY` connects related tables.
* It references a `PRIMARY KEY` or `UNIQUE` key in another table.
* It enforces referential integrity.
* Parent tables store master data; child tables store related data.
* `ON DELETE` and `ON UPDATE` actions control how changes propagate between related tables.

---

# Conclusion

The `FOREIGN KEY` constraint is the foundation of relationships in relational databases. It ensures that child records always reference valid parent records, preventing inconsistent or orphaned data. By enforcing referential integrity and supporting cascading actions, foreign keys help build reliable, maintainable, and scalable database systems. In the next chapter, you will learn about the **`CHECK` constraint**, which restricts column values based on specified conditions.
