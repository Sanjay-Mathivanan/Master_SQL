# NOT NULL Constraint

# Introduction

In every database, certain pieces of information are mandatory. For example:

* Every student must have a Student ID.
* Every employee must have a name.
* Every customer must have an email address (depending on business requirements).

If these important fields are left empty, the database becomes incomplete and unreliable.

The **`NOT NULL`** constraint ensures that a column **cannot store `NULL` values**. It is one of the simplest and most commonly used SQL constraints for maintaining data integrity.

In this chapter, you will learn what the `NOT NULL` constraint is, why it is important, how to use it, and best practices for designing reliable database tables.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand the purpose of the `NOT NULL` constraint.
* Differentiate between `NULL` and an empty string.
* Create tables with `NOT NULL` columns.
* Add a `NOT NULL` constraint to an existing table.
* Understand common errors related to `NOT NULL`.
* Follow best practices when designing database tables.

---

# Problem Statement

Suppose the following **Student** table is created without any constraints.

```sql
CREATE TABLE Student (
    StudentID INT,
    Name VARCHAR(100),
    Department VARCHAR(50)
);
```

Now consider the following data.

| StudentID | Name  | Department |
| --------- | ----- | ---------- |
| 101       | Rahul | CSE        |
| 102       | NULL  | AI         |
| NULL      | Priya | IT         |

Problems:

* Student name is missing.
* Student ID is missing.

These records reduce the quality of the database.

The solution is to use the **`NOT NULL`** constraint.

---

# Why Do We Need NOT NULL?

The `NOT NULL` constraint helps to:

* Prevent missing values.
* Ensure mandatory information is always stored.
* Improve data quality.
* Reduce application errors.
* Maintain database consistency.

Without this constraint, important information can be omitted accidentally.

---

# What is the NOT NULL Constraint?

The **`NOT NULL`** constraint specifies that a column **must always contain a value**.

Whenever a new row is inserted or an existing row is updated, the database checks the column.

If the value is `NULL`, the operation is rejected.

---

# NULL vs Empty String

Many beginners confuse `NULL` with an empty string.

| NULL                               | Empty String (`''`)                     |
| ---------------------------------- | --------------------------------------- |
| Represents missing or unknown data | Represents a value with zero characters |
| No actual value is stored          | A valid string value is stored          |
| Cannot be compared using `=`       | Can be compared like any other string   |

Example:

```sql
NULL
```

```sql
''
```

These are **not the same**.

---

# Syntax

## During Table Creation

```sql
CREATE TABLE table_name (
    column_name data_type NOT NULL
);
```

---

## Example

```sql
CREATE TABLE Student (
    StudentID INT NOT NULL,
    Name VARCHAR(100) NOT NULL,
    Department VARCHAR(50)
);
```

---

# Table Structure

| Column     | Constraint    |
| ---------- | ------------- |
| StudentID  | NOT NULL      |
| Name       | NOT NULL      |
| Department | No constraint |

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

### Result

The row is inserted successfully because all `NOT NULL` columns contain values.

---

# Example 2 – Invalid Insert

```sql
INSERT INTO Student
VALUES (
    NULL,
    'Rahul',
    'CSE'
);
```

### Result

❌ Error

Reason:

`StudentID` cannot contain a `NULL` value.

---

# Example 3 – Another Invalid Insert

```sql
INSERT INTO Student
VALUES (
    102,
    NULL,
    'AI'
);
```

### Result

❌ Error

Reason:

`Name` is defined as `NOT NULL`.

---

# Adding NOT NULL to an Existing Table

Sometimes the table already exists.

## MySQL

```sql
ALTER TABLE Student
MODIFY Name VARCHAR(100) NOT NULL;
```

---

## PostgreSQL

```sql
ALTER TABLE Student
ALTER COLUMN Name SET NOT NULL;
```

---

## SQL Server

```sql
ALTER TABLE Student
ALTER COLUMN Name VARCHAR(100) NOT NULL;
```

---

## SQLite

SQLite has limited support for altering existing column constraints. In many cases, the recommended approach is to create a new table with the required constraint, copy the data, and then replace the original table.

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
NOT NULL Constraint
   │
   ▼
Value Present?
 │
 ├── Yes → Store Data
 │
 └── No → Reject Operation
```

---

# Real-World Applications

| Industry   | Example                       |
| ---------- | ----------------------------- |
| School     | Student ID must always exist  |
| Banking    | Account Number cannot be NULL |
| Hospital   | Patient Name is mandatory     |
| E-Commerce | Product Name cannot be NULL   |
| HR         | Employee ID must be provided  |
| Library    | Book Title is mandatory       |

---

# Database Compatibility

| Feature                 | MySQL | PostgreSQL | SQL Server |  SQLite  |
| ----------------------- | :---: | :--------: | :--------: | :------: |
| NOT NULL                |   ✅   |      ✅     |      ✅     |     ✅    |
| During `CREATE TABLE`   |   ✅   |      ✅     |      ✅     |     ✅    |
| Add Using `ALTER TABLE` |   ✅   |      ✅     |      ✅     | Limited* |

> *SQLite generally requires recreating the table to add a `NOT NULL` constraint to an existing column.

---

# Advantages

* Prevents missing data.
* Improves data quality.
* Enforces mandatory fields.
* Reduces application validation.
* Improves database consistency.

---

# Limitations

* Reduces flexibility for optional fields.
* Existing `NULL` values must be removed before adding the constraint to an existing column.
* Syntax for modifying existing columns differs across database systems.

---

# Common Mistakes

* Confusing `NULL` with an empty string.
* Applying `NOT NULL` to optional fields.
* Forgetting to provide values during `INSERT`.
* Attempting to add the constraint when existing rows contain `NULL` values.
* Assuming every column should be `NOT NULL`.

---

# Best Practices

* Use `NOT NULL` only for mandatory information.
* Combine `NOT NULL` with `PRIMARY KEY` where appropriate.
* Validate existing data before adding the constraint.
* Use descriptive column names.
* Document mandatory fields clearly.

---

# Interview Questions

### 1. What is the purpose of the `NOT NULL` constraint?

**Answer:** It ensures that a column cannot contain `NULL` values.

---

### 2. What is the difference between `NULL` and an empty string?

**Answer:**

| NULL                     | Empty String                  |
| ------------------------ | ----------------------------- |
| Missing or unknown value | Zero-length string            |
| Represents no value      | Represents a valid text value |

---

### 3. Can a `NOT NULL` column contain an empty string?

**Answer:** Yes. An empty string (`''`) is a valid value and is different from `NULL`.

---

### 4. Can `NOT NULL` be added after table creation?

**Answer:** Yes. It can usually be added using `ALTER TABLE`, provided existing data satisfies the constraint.

---

### 5. Which columns are commonly defined as `NOT NULL`?

**Answer:**

* Primary Keys
* Employee Names
* Student IDs
* Account Numbers
* Product Names

---

# Practice Questions

## Easy

1. What is the purpose of the `NOT NULL` constraint?
2. What is the difference between `NULL` and an empty string?
3. Can a `NOT NULL` column store `NULL`?
4. Write the syntax for a `NOT NULL` column.
5. Give two examples of mandatory fields.

---

## Medium

1. Create a `Student` table using `NOT NULL`.
2. Add a `NOT NULL` constraint to an existing table.
3. Explain how the database validates `NOT NULL`.
4. Compare `NULL` and an empty string.
5. Explain common errors related to `NOT NULL`.

---

## Hard

1. Explain the internal working of the `NOT NULL` constraint.
2. Compare `NOT NULL` support across MySQL, PostgreSQL, SQL Server, and SQLite.
3. Design a database schema that uses `NOT NULL` appropriately.
4. Explain the advantages and limitations of the `NOT NULL` constraint.
5. Discuss best practices for using `NOT NULL` in production databases.

---

# Key Takeaways

* `NOT NULL` ensures that mandatory columns always contain a value.
* `NULL` and an empty string are different.
* The database automatically validates `NOT NULL` during `INSERT` and `UPDATE`.
* `NOT NULL` improves data integrity and consistency.
* Use `NOT NULL` only for fields that are truly mandatory.

---

# Conclusion

The `NOT NULL` constraint is one of the most fundamental mechanisms for ensuring data quality in relational databases. By preventing missing values in important columns, it helps maintain accurate, consistent, and reliable information. In the next chapter, you will learn about the **`UNIQUE` constraint**, which ensures that duplicate values are not stored in specific columns.
