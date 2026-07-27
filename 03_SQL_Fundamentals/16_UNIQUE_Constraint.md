# UNIQUE Constraint

# Introduction

In many database applications, certain values must be unique. For example:

* Every employee should have a unique Employee ID.
* Every customer should have a unique email address.
* Every vehicle should have a unique registration number.
* Every user should have a unique username.

If duplicate values are allowed in these fields, it can lead to incorrect records, login issues, and data inconsistencies.

The **`UNIQUE`** constraint ensures that all values in a column (or a combination of columns) are **unique**, preventing duplicate entries while maintaining data integrity.

In this chapter, you will learn what the `UNIQUE` constraint is, why it is important, how to use it, and the difference between `UNIQUE` and `PRIMARY KEY`.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand the purpose of the `UNIQUE` constraint.
* Create tables using the `UNIQUE` constraint.
* Add a `UNIQUE` constraint to an existing table.
* Create composite `UNIQUE` constraints.
* Compare `UNIQUE` and `PRIMARY KEY`.
* Follow best practices when using the `UNIQUE` constraint.

---

# Problem Statement

Suppose the following **Student** table is created.

```sql id="7n7qzq"
CREATE TABLE Student (
    StudentID INT,
    Name VARCHAR(100),
    Email VARCHAR(100)
);
```

Now consider the following records.

| StudentID | Name  | Email                                         |
| --------- | ----- | --------------------------------------------- |
| 101       | Rahul | [rahul@example.com](mailto:rahul@example.com) |
| 102       | Priya | [priya@example.com](mailto:priya@example.com) |
| 103       | Arun  | [rahul@example.com](mailto:rahul@example.com) |

The same email address appears twice.

This can create problems because each student should have a unique email address.

The solution is the **`UNIQUE`** constraint.

---

# Why Do We Need UNIQUE?

The `UNIQUE` constraint helps to:

* Prevent duplicate values.
* Maintain data integrity.
* Enforce business rules.
* Improve data quality.
* Ensure reliable searching and identification.

Without this constraint, duplicate values may lead to incorrect reports and inconsistent data.

---

# What is the UNIQUE Constraint?

The **`UNIQUE`** constraint ensures that every value in a column (or a combination of columns) is unique.

Whenever data is inserted or updated, the database checks whether the new value already exists.

If a duplicate value is found, the operation is rejected.

---

# Syntax

## During Table Creation

```sql id="mgh2zi"
CREATE TABLE table_name (
    column_name data_type UNIQUE
);
```

---

## Example

```sql id="aj1rmz"
CREATE TABLE Student (
    StudentID INT,
    Name VARCHAR(100),
    Email VARCHAR(100) UNIQUE
);
```

---

# Table Structure

| Column    | Constraint |
| --------- | ---------- |
| StudentID | None       |
| Name      | None       |
| Email     | UNIQUE     |

---

# Example 1 – Valid Insert

```sql id="em0wxy"
INSERT INTO Student
VALUES (
    101,
    'Rahul',
    'rahul@example.com'
);
```

```sql id="4y2zgv"
INSERT INTO Student
VALUES (
    102,
    'Priya',
    'priya@example.com'
);
```

### Result

Both records are inserted successfully because the email addresses are different.

---

# Example 2 – Invalid Insert

```sql id="1iwz9j"
INSERT INTO Student
VALUES (
    103,
    'Arun',
    'rahul@example.com'
);
```

### Result

❌ Error

Reason:

The email address already exists, violating the `UNIQUE` constraint.

---

# UNIQUE on Multiple Columns (Composite UNIQUE)

Sometimes a single column does not need to be unique, but a combination of columns must be unique.

## Example

```sql id="3q9j8m"
CREATE TABLE Student (
    StudentID INT,
    Name VARCHAR(100),
    Department VARCHAR(50),
    UNIQUE (Name, Department)
);
```

This allows:

| Name  | Department |
| ----- | ---------- |
| Rahul | CSE        |
| Rahul | AI         |

But it does **not** allow:

| Name  | Department |
| ----- | ---------- |
| Rahul | CSE        |
| Rahul | CSE        |

because the combination is duplicated.

---

# Adding UNIQUE to an Existing Table

## MySQL

```sql id="8jlwmc"
ALTER TABLE Student
ADD CONSTRAINT UQ_Student_Email
UNIQUE (Email);
```

---

## PostgreSQL

```sql id="lo6nwc"
ALTER TABLE Student
ADD CONSTRAINT UQ_Student_Email
UNIQUE (Email);
```

---

## SQL Server

```sql id="vxg14m"
ALTER TABLE Student
ADD CONSTRAINT UQ_Student_Email
UNIQUE (Email);
```

---

## SQLite

```sql id="v2tbmp"
CREATE UNIQUE INDEX UQ_Student_Email
ON Student (Email);
```

---

# Internal Working

```text id="56v3qi"
User
   │
   ▼
INSERT / UPDATE
   │
   ▼
Database Checks
UNIQUE Constraint
   │
   ▼
Duplicate Value?
 │
 ├── No → Store Data
 │
 └── Yes → Reject Operation
```

---

# UNIQUE vs PRIMARY KEY

| UNIQUE                                                  | PRIMARY KEY                                 |
| ------------------------------------------------------- | ------------------------------------------- |
| Prevents duplicate values                               | Prevents duplicate values                   |
| Can allow `NULL` values (database-specific rules apply) | Does not allow `NULL` values                |
| Multiple `UNIQUE` constraints can exist in a table      | Only one `PRIMARY KEY` is allowed per table |
| Used for alternate unique fields                        | Used as the main identifier for each row    |

> **Note:** Some database systems allow multiple `NULL` values in a `UNIQUE` column, while others have different behaviour. Always check your DBMS documentation.

---

# Real-World Applications

| Industry   | Example                     |
| ---------- | --------------------------- |
| School     | Student Email               |
| Banking    | Account Number              |
| Hospital   | Patient Registration Number |
| E-Commerce | Product SKU                 |
| HR         | Employee Email              |
| Library    | ISBN Number                 |

---

# Database Compatibility

| Feature                | MySQL | PostgreSQL | SQL Server |  SQLite  |
| ---------------------- | :---: | :--------: | :--------: | :------: |
| UNIQUE Constraint      |   ✅   |      ✅     |      ✅     |     ✅    |
| Composite UNIQUE       |   ✅   |      ✅     |      ✅     |     ✅    |
| Add with `ALTER TABLE` |   ✅   |      ✅     |      ✅     | Limited* |

> *SQLite commonly uses a unique index or table recreation for some schema modifications.

---

# Advantages

* Prevents duplicate data.
* Improves data consistency.
* Enforces business rules.
* Supports one or multiple columns.
* Improves search reliability.

---

# Limitations

* Existing duplicate values must be removed before adding the constraint.
* Does not replace a `PRIMARY KEY`.
* Database systems differ in how they treat `NULL` values.

---

# Common Mistakes

* Confusing `UNIQUE` with `PRIMARY KEY`.
* Assuming `UNIQUE` prevents all `NULL` values.
* Adding the constraint when duplicate data already exists.
* Using `UNIQUE` where a `PRIMARY KEY` is more appropriate.
* Forgetting to check existing data before creating the constraint.

---

# Best Practices

* Use `UNIQUE` for alternate identifiers such as email addresses and usernames.
* Use `PRIMARY KEY` for the main identifier of a table.
* Remove duplicate data before adding a `UNIQUE` constraint.
* Give constraints meaningful names.
* Test inserts and updates after creating the constraint.

---

# Interview Questions

### 1. What is the purpose of the `UNIQUE` constraint?

**Answer:** It ensures that duplicate values cannot be stored in a column or a combination of columns.

---

### 2. Can a table have multiple `UNIQUE` constraints?

**Answer:** Yes. A table can have multiple `UNIQUE` constraints on different columns or combinations of columns.

---

### 3. What is the difference between `UNIQUE` and `PRIMARY KEY`?

**Answer:**

| UNIQUE                                        | PRIMARY KEY                                          |
| --------------------------------------------- | ---------------------------------------------------- |
| Prevents duplicate values                     | Prevents duplicates and uniquely identifies each row |
| May allow `NULL` values depending on the DBMS | Does not allow `NULL` values                         |
| Multiple constraints allowed                  | Only one per table                                   |

---

### 4. Can `UNIQUE` be applied to multiple columns?

**Answer:** Yes. This is called a **composite `UNIQUE` constraint**.

---

### 5. What happens if duplicate values are inserted into a `UNIQUE` column?

**Answer:** The database rejects the operation and returns a constraint violation error.

---

# Practice Questions

## Easy

1. What is the purpose of the `UNIQUE` constraint?
2. Write the syntax for creating a `UNIQUE` column.
3. Can a table have more than one `UNIQUE` constraint?
4. Can a `UNIQUE` constraint be applied to multiple columns?
5. Give two real-world examples where `UNIQUE` should be used.

---

## Medium

1. Create a `Student` table with a `UNIQUE` email column.
2. Add a `UNIQUE` constraint to an existing table.
3. Explain how the database validates a `UNIQUE` constraint.
4. Compare `UNIQUE` and `PRIMARY KEY`.
5. Explain composite `UNIQUE` constraints with an example.

---

## Hard

1. Explain the internal working of the `UNIQUE` constraint.
2. Compare `UNIQUE` support across MySQL, PostgreSQL, SQL Server, and SQLite.
3. Design a database schema using multiple `UNIQUE` constraints.
4. Explain the advantages and limitations of the `UNIQUE` constraint.
5. Discuss best practices for using `UNIQUE` in production databases.

---

# Key Takeaways

* The `UNIQUE` constraint prevents duplicate values.
* It can be applied to one or multiple columns.
* It helps maintain data integrity and consistency.
* It is commonly used for email addresses, usernames, account numbers, and product codes.
* `UNIQUE` complements, but does not replace, the `PRIMARY KEY`.

---

# Conclusion

The `UNIQUE` constraint is an essential tool for ensuring that important values remain distinct within a database. By preventing duplicate entries, it improves data quality, supports business rules, and enhances application reliability. In the next chapter, you will learn about the **`PRIMARY KEY` constraint**, which uniquely identifies every row in a table and forms the foundation of relational database design.
