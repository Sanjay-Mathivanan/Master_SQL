# PRIMARY KEY Constraint

# Introduction

Every table in a relational database should have a way to uniquely identify each record. Without a unique identifier, it becomes difficult to retrieve, update, delete, or establish relationships between records.

For example:

* Every student should have a unique Student ID.
* Every employee should have a unique Employee ID.
* Every customer should have a unique Customer ID.
* Every product should have a unique Product ID.

The **PRIMARY KEY** constraint ensures that every row in a table has a **unique and non-NULL identifier**.

In this chapter, you will learn what the `PRIMARY KEY` constraint is, why it is important, how to create it, and how it differs from the `UNIQUE` constraint.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand the purpose of the `PRIMARY KEY` constraint.
* Create tables using a primary key.
* Add a primary key to an existing table.
* Create composite primary keys.
* Compare `PRIMARY KEY` and `UNIQUE`.
* Follow best practices when designing database tables.

---

# Problem Statement

Suppose the following **Student** table is created without a primary key.

```sql
CREATE TABLE Student (
    StudentID INT,
    Name VARCHAR(100),
    Department VARCHAR(50)
);
```

Now consider the following records.

| StudentID | Name  | Department |
| --------- | ----- | ---------- |
| 101       | Rahul | CSE        |
| 101       | Priya | AI         |
| NULL      | Arun  | ECE        |

Problems:

* Duplicate Student IDs.
* Missing Student ID.
* No reliable way to identify each student.

These issues can be prevented by using the **PRIMARY KEY** constraint.

---

# Why Do We Need a PRIMARY KEY?

The `PRIMARY KEY` constraint helps to:

* Uniquely identify every row.
* Prevent duplicate values.
* Prevent `NULL` values.
* Improve query performance through indexing.
* Establish relationships using foreign keys.
* Maintain entity integrity.

Without a primary key, managing and relating data becomes much more difficult.

---

# What is a PRIMARY KEY?

A **PRIMARY KEY** is a column (or combination of columns) whose values uniquely identify every row in a table.

A primary key has two important properties:

* Every value must be **unique**.
* Every value must be **NOT NULL**.

Each table can have **only one primary key**, although that primary key may consist of multiple columns.

---

# Characteristics of a PRIMARY KEY

| Property               | Description                                                  |
| ---------------------- | ------------------------------------------------------------ |
| Unique                 | Duplicate values are not allowed                             |
| NOT NULL               | Missing values are not allowed                               |
| One per Table          | A table can have only one primary key                        |
| Indexed                | Most DBMSs automatically create an index for the primary key |
| Used for Relationships | Frequently referenced by foreign keys                        |

---

# Syntax

## Column-Level PRIMARY KEY

```sql
CREATE TABLE table_name (
    column_name data_type PRIMARY KEY
);
```

---

## Example

```sql
CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(100),
    Department VARCHAR(50)
);
```

---

# Table Structure

| Column     | Constraint  |
| ---------- | ----------- |
| StudentID  | PRIMARY KEY |
| Name       | None        |
| Department | None        |

---

# Example 1 – Valid Insert

```sql
INSERT INTO Student
VALUES (
    101,
    'Rahul',
    'CSE'
);
```

```sql
INSERT INTO Student
VALUES (
    102,
    'Priya',
    'AI'
);
```

### Result

Both rows are inserted successfully because the primary key values are unique.

---

# Example 2 – Duplicate PRIMARY KEY

```sql
INSERT INTO Student
VALUES (
    101,
    'Arun',
    'ECE'
);
```

### Result

❌ Error

Reason:

The value **101** already exists in the primary key column.

---

# Example 3 – NULL PRIMARY KEY

```sql
INSERT INTO Student
VALUES (
    NULL,
    'Sneha',
    'IT'
);
```

### Result

❌ Error

Reason:

A primary key cannot contain `NULL`.

---

# Composite PRIMARY KEY

Sometimes a single column is not enough to uniquely identify a row.

A **Composite Primary Key** uses two or more columns together.

## Example

```sql
CREATE TABLE StudentCourse (
    StudentID INT,
    CourseID INT,
    Grade CHAR(2),
    PRIMARY KEY (StudentID, CourseID)
);
```

In this table:

| StudentID | CourseID | Result                  |
| --------- | -------- | ----------------------- |
| 101       | C101     | ✅ Allowed               |
| 101       | C102     | ✅ Allowed               |
| 101       | C101     | ❌ Duplicate combination |

---

# Adding PRIMARY KEY to an Existing Table

Before adding a primary key:

* All values must be unique.
* No value can be `NULL`.

## MySQL

```sql
ALTER TABLE Student
ADD CONSTRAINT PK_Student
PRIMARY KEY (StudentID);
```

---

## PostgreSQL

```sql
ALTER TABLE Student
ADD CONSTRAINT PK_Student
PRIMARY KEY (StudentID);
```

---

## SQL Server

```sql
ALTER TABLE Student
ADD CONSTRAINT PK_Student
PRIMARY KEY (StudentID);
```

---

## SQLite

SQLite has limited support for adding a primary key to an existing table. In many cases, the recommended approach is to create a new table with the required primary key, copy the data, and replace the original table.

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
PRIMARY KEY
   │
   ├── Duplicate?
   ├── NULL?
   │
   ▼
Valid?
 │
 ├── Yes → Store Data
 │
 └── No → Reject Operation
```

---

# PRIMARY KEY vs UNIQUE

| PRIMARY KEY                         | UNIQUE                                   |
| ----------------------------------- | ---------------------------------------- |
| Uniquely identifies each row        | Prevents duplicate values                |
| Does not allow `NULL` values        | May allow `NULL` values (DBMS dependent) |
| Only one per table                  | Multiple allowed per table               |
| Commonly referenced by foreign keys | Usually used for alternate unique fields |
| Automatically implies `NOT NULL`    | Does not automatically imply `NOT NULL`  |

---

# PRIMARY KEY vs NOT NULL

| PRIMARY KEY                           | NOT NULL                       |
| ------------------------------------- | ------------------------------ |
| Prevents duplicates and `NULL` values | Prevents only `NULL` values    |
| Uniquely identifies rows              | Does not guarantee uniqueness  |
| Only one per table                    | Can be applied to many columns |

---

# Real-World Applications

| Industry   | Primary Key Example |
| ---------- | ------------------- |
| School     | StudentID           |
| Banking    | AccountNumber       |
| Hospital   | PatientID           |
| HR         | EmployeeID          |
| E-Commerce | ProductID           |
| Library    | BookID              |

---

# Database Compatibility

| Feature                 | MySQL | PostgreSQL | SQL Server |  SQLite  |
| ----------------------- | :---: | :--------: | :--------: | :------: |
| PRIMARY KEY             |   ✅   |      ✅     |      ✅     |     ✅    |
| Composite PRIMARY KEY   |   ✅   |      ✅     |      ✅     |     ✅    |
| Auto Index Creation     |   ✅   |      ✅     |      ✅     |     ✅    |
| Add Using `ALTER TABLE` |   ✅   |      ✅     |      ✅     | Limited* |

> *SQLite typically requires recreating the table to add a primary key after creation.

---

# Advantages

* Guarantees unique row identification.
* Prevents duplicate and missing identifiers.
* Improves search performance through indexing.
* Forms the basis for relationships between tables.
* Maintains entity integrity.

---

# Limitations

* Only one primary key is allowed per table.
* Existing duplicate or `NULL` values must be corrected before adding the constraint.
* Changing a primary key later may affect related tables.

---

# Common Mistakes

* Creating tables without a primary key.
* Using columns that frequently change as primary keys.
* Attempting to insert duplicate primary key values.
* Allowing business logic to depend on mutable primary keys.
* Confusing `PRIMARY KEY` with `UNIQUE`.

---

# Best Practices

* Define a primary key for every table whenever possible.
* Choose a stable value that rarely changes.
* Use integer or surrogate keys for large systems when appropriate.
* Give constraints meaningful names.
* Avoid updating primary key values after records are created.

---

# Interview Questions

### 1. What is a PRIMARY KEY?

**Answer:** A primary key is a column or combination of columns that uniquely identifies every row in a table and cannot contain `NULL` values.

---

### 2. Can a table have multiple primary keys?

**Answer:** No. A table can have only one primary key, but it may consist of multiple columns.

---

### 3. Can a PRIMARY KEY contain `NULL` values?

**Answer:** No. A primary key must always contain a valid, non-`NULL` value.

---

### 4. What is a Composite Primary Key?

**Answer:** A primary key made up of two or more columns that together uniquely identify each row.

---

### 5. What is the difference between `PRIMARY KEY` and `UNIQUE`?

**Answer:**

| PRIMARY KEY         | UNIQUE                              |
| ------------------- | ----------------------------------- |
| One per table       | Multiple allowed                    |
| No `NULL` values    | `NULL` handling depends on the DBMS |
| Identifies each row | Prevents duplicate values           |

---

# Practice Questions

## Easy

1. What is a primary key?
2. Can a primary key contain `NULL` values?
3. How many primary keys can a table have?
4. Write the syntax for creating a primary key.
5. Give three examples of primary keys used in real-world applications.

---

## Medium

1. Create a `Student` table with `StudentID` as the primary key.
2. Add a primary key to an existing table.
3. Explain the internal working of the `PRIMARY KEY` constraint.
4. Compare `PRIMARY KEY` and `UNIQUE`.
5. Explain composite primary keys with an example.

---

## Hard

1. Explain the role of the primary key in relational database design.
2. Compare primary key implementation across MySQL, PostgreSQL, SQL Server, and SQLite.
3. Design a database schema using appropriate primary keys.
4. Explain how primary keys improve query performance.
5. Discuss best practices for choosing primary keys in enterprise applications.

---

# Key Takeaways

* A `PRIMARY KEY` uniquely identifies every row in a table.
* Primary key values must be unique and cannot be `NULL`.
* Each table can have only one primary key.
* Composite primary keys use multiple columns together.
* Primary keys form the foundation of relationships in relational databases.

---

# Conclusion

The `PRIMARY KEY` constraint is one of the most important concepts in relational databases. It ensures that every record has a unique identity, supports efficient searching through indexing, and enables relationships between tables using foreign keys. A well-designed primary key improves data integrity, performance, and maintainability, making it a fundamental part of every database design. In the next chapter, you will learn about the **`FOREIGN KEY` constraint**, which connects tables and maintains referential integrity.
