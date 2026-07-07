# Unique Key

# Introduction

In the previous chapters, you learned about **Primary Keys**, **Candidate Keys**, and **Alternate Keys**. A **Unique Key** is another important database constraint that ensures duplicate values are not allowed in a column.

Unlike a Primary Key, a table can have **multiple Unique Keys**, making it useful for enforcing uniqueness on additional columns such as **Email**, **Phone Number**, or **Passport Number**.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand what a Unique Key is.
* Learn why Unique Keys are important.
* Create a Unique Key using SQL.
* Differentiate Unique Key from Primary Key.
* Answer interview questions related to Unique Keys.

---

# Problem Statement

Consider the following **Employee** table.

| EmployeeID | Name    | Email                                         |
| ---------- | ------- | --------------------------------------------- |
| E101       | Alice   | [alice@company.com](mailto:alice@company.com) |
| E102       | Bob     | [bob@company.com](mailto:bob@company.com)     |
| E103       | Charlie | [alice@company.com](mailto:alice@company.com) |

Here, two employees have the same email address.

Since every employee should have a unique email, duplicate values must be prevented.

A **Unique Key** solves this problem.

---

# Why Do We Need a Unique Key?

Without a Unique Key:

* Duplicate business data may exist.
* Email addresses may repeat.
* Phone numbers may be duplicated.
* Passport numbers may not remain unique.
* Data integrity is reduced.

A Unique Key ensures that important business attributes remain unique.

---

# Definition

A **Unique Key** is a database constraint that ensures all values in a column (or combination of columns) are unique.

Unlike a Primary Key, a table can have **multiple Unique Keys**.

> **Note:** The handling of `NULL` values in a Unique Key depends on the database system. Many databases allow one or more `NULL` values, while others have different behaviors.

---

# Characteristics of Unique Key

* Prevents duplicate values.
* Can be applied to one or more columns.
* A table can have multiple Unique Keys.
* Can be referenced by a Foreign Key (DBMS-dependent).
* May allow `NULL` values depending on the database system.

---

# SQL Syntax

## Creating a Unique Key During Table Creation

```sql
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(100),
    Email VARCHAR(100) UNIQUE
);
```

---

## Creating a Composite Unique Key

```sql
CREATE TABLE Student (
    StudentID INT,
    CourseID INT,
    Email VARCHAR(100),
    UNIQUE (StudentID, CourseID)
);
```

---

## Adding a Unique Key to an Existing Table

```sql
ALTER TABLE Employee
ADD CONSTRAINT UK_Employee_Email
UNIQUE (Email);
```

---

# Example

## Employee Table

| EmployeeID | Name    | Email                                             |
| ---------- | ------- | ------------------------------------------------- |
| E101       | Alice   | [alice@company.com](mailto:alice@company.com)     |
| E102       | Bob     | [bob@company.com](mailto:bob@company.com)         |
| E103       | Charlie | [charlie@company.com](mailto:charlie@company.com) |

The **Email** column has a Unique Key.

No two employees can have the same email address.

---

# Invalid Example

Attempting to insert the following record:

| EmployeeID | Name  | Email                                         |
| ---------- | ----- | --------------------------------------------- |
| E104       | David | [alice@company.com](mailto:alice@company.com) |

Result:

* ❌ Insert rejected because the email already exists.

---

# Internal Working

```text
Insert New Record
       │
       ▼
Check Unique Column
       │
       ├── Duplicate Found?
       │        │
       │        ├── Yes → Reject Record
       │        │
       │        └── No
       ▼
Insert Record
```

---

# Unique Key vs Primary Key

| Feature                        | Primary Key                  | Unique Key                   |
| ------------------------------ | ---------------------------- | ---------------------------- |
| Purpose                        | Main identifier of the table | Prevents duplicate values    |
| Duplicate Values               | Not allowed                  | Not allowed                  |
| NULL Values                    | Not allowed                  | Depends on the DBMS          |
| Number Allowed                 | One per table                | Multiple per table           |
| Automatically Creates an Index | Yes (DBMS-dependent)         | Usually yes (DBMS-dependent) |
| Used as Main Identifier        | Yes                          | No                           |

---

# Real-World Examples

| Application         | Unique Column       |
| ------------------- | ------------------- |
| Employee Management | Email               |
| Banking System      | Account Number      |
| Passport System     | Passport Number     |
| Hospital Management | Patient Email       |
| College ERP         | Student Roll Number |

---

# Advantages

* Prevents duplicate values.
* Maintains business data integrity.
* Allows multiple unique constraints in one table.
* Improves data consistency.
* Supports reliable searching of unique business attributes.

---

# Limitations

* Does not replace the Primary Key.
* Behavior of `NULL` values varies between database systems.
* Excessive Unique Keys may slightly increase insert and update overhead.

---

# Common Mistakes

* Confusing Unique Key with Primary Key.
* Assuming only one Unique Key is allowed.
* Forgetting that `NULL` behavior depends on the DBMS.
* Applying a Unique Key to columns that should allow duplicate values.

---

# Best Practices

* Use Unique Keys for business identifiers such as Email or Passport Number.
* Keep the Primary Key separate from business attributes when appropriate.
* Understand your database system's `NULL` handling.
* Create Unique Keys only where uniqueness is required.

---

# Interview Questions

### 1. What is a Unique Key?

**Answer:** A Unique Key is a constraint that prevents duplicate values in a column or combination of columns.

---

### 2. Can a table have multiple Unique Keys?

**Answer:** Yes.

---

### 3. What is the difference between a Primary Key and a Unique Key?

**Answer:** A Primary Key is the main identifier of a table and cannot contain `NULL` values. A Unique Key prevents duplicate values and its `NULL` behavior depends on the DBMS.

---

### 4. Can a Unique Key contain duplicate values?

**Answer:** No.

---

### 5. Can a Foreign Key reference a Unique Key?

**Answer:** Yes. In many relational database systems, a Foreign Key can reference a column that has a `PRIMARY KEY` or `UNIQUE` constraint.

---

# Practice Questions

## Easy

1. Define a Unique Key.
2. Can a table have multiple Unique Keys?
3. Can a Unique Key contain duplicate values?
4. Write SQL to create a Unique Key.
5. Give two real-world examples of Unique Keys.

## Medium

1. Differentiate Primary Key and Unique Key.
2. Explain Unique Key with an Employee table.
3. Why is a Unique Key important?
4. How do you add a Unique Key to an existing table?
5. Explain Composite Unique Key.

## Hard

1. Design Unique Keys for a Hospital Management System.
2. Compare Primary Key, Candidate Key, Alternate Key, and Unique Key.
3. Explain how Unique Keys improve database integrity.
4. Design Unique constraints for an Online Shopping database.
5. Discuss DBMS-specific differences in `NULL` handling for Unique Keys.

---

# Key Takeaways

* A Unique Key prevents duplicate values in a column or combination of columns.
* A table can have multiple Unique Keys.
* Unlike a Primary Key, `NULL` handling depends on the database system.
* Unique Keys are commonly used for business identifiers such as Email and Passport Number.
* Unique Keys help maintain data integrity and consistency.

---

# Conclusion

A Unique Key is an essential database constraint that ensures important business attributes remain unique. While it is different from a Primary Key, it plays a significant role in maintaining data quality, preventing duplicates, and supporting reliable relational database design.
