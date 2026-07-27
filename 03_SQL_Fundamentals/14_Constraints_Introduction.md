# Constraints Introduction

# Introduction

Data is one of the most valuable assets of any organization. Whether it is a banking system, hospital management system, e-commerce website, or student information system, maintaining **accurate, consistent, and reliable data** is essential.

Imagine a database where:

* Two students have the same Student ID.
* An employee's salary is stored as negative.
* A customer record has no name.
* An order references a customer who does not exist.

Such inconsistencies make the database unreliable and difficult to maintain.

To prevent these problems, SQL provides **Constraints**.

Constraints are rules applied to table columns that ensure only valid and consistent data is stored in the database.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand what constraints are.
* Learn why constraints are important.
* Identify different types of SQL constraints.
* Understand how constraints maintain data integrity.
* Apply constraints while creating tables.
* Follow best practices when designing database tables.

---

# Problem Statement

Suppose we create the following **Student** table.

```sql
CREATE TABLE Student (
    StudentID INT,
    Name VARCHAR(100),
    Age INT,
    Department VARCHAR(50)
);
```

Without constraints, the following invalid records can be inserted.

| StudentID | Name  | Age | Department |
| --------- | ----- | --: | ---------- |
| 101       | Rahul |  20 | CSE        |
| 101       | Priya |  19 | AI         |
| NULL      | Arun  |  21 | ECE        |
| 104       | NULL  |  20 | IT         |

Problems:

* Duplicate Student IDs
* Missing Student IDs
* Missing student names

These problems can be prevented using SQL constraints.

---

# Why Do We Need Constraints?

Constraints help to:

* Prevent invalid data.
* Maintain data consistency.
* Enforce business rules.
* Improve data quality.
* Protect relationships between tables.
* Reduce application-level validation.

Without constraints, the database cannot guarantee that stored data is correct.

---

# What are Constraints?

A **Constraint** is a rule applied to one or more columns in a table.

The database automatically checks these rules whenever data is inserted, updated, or modified.

If the data violates a constraint, the database rejects the operation.

---

# Types of SQL Constraints

SQL provides several built-in constraints.

| Constraint                         | Purpose                                |
| ---------------------------------- | -------------------------------------- |
| NOT NULL                           | Prevents NULL values                   |
| UNIQUE                             | Prevents duplicate values              |
| PRIMARY KEY                        | Uniquely identifies each row           |
| FOREIGN KEY                        | Maintains relationships between tables |
| CHECK                              | Restricts values based on a condition  |
| DEFAULT                            | Assigns a default value                |
| AUTO_INCREMENT / IDENTITY / SERIAL | Automatically generates values         |

Each constraint will be discussed in detail in the upcoming chapters.

---

# Where Can Constraints Be Applied?

Constraints can be defined:

* During table creation.
* After table creation using `ALTER TABLE`.

---

# Example 1 – Constraint During Table Creation

```sql
CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Department VARCHAR(50)
);
```

---

# Example 2 – Constraint Using ALTER TABLE

```sql
ALTER TABLE Student
ADD CONSTRAINT PK_Student
PRIMARY KEY (StudentID);
```

---

# Types of Data Integrity

Constraints help maintain different types of data integrity.

## 1. Entity Integrity

Ensures every row has a unique identity.

Example:

```sql
PRIMARY KEY
```

---

## 2. Referential Integrity

Maintains relationships between tables.

Example:

```sql
FOREIGN KEY
```

---

## 3. Domain Integrity

Ensures values belong to a valid range or format.

Example:

```sql
CHECK (Age >= 18)
```

---

## 4. Column Integrity

Ensures mandatory fields are not left empty.

Example:

```sql
NOT NULL
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
Database Receives Data
   │
   ▼
Constraint Validation
   │
   ├── PRIMARY KEY
   ├── FOREIGN KEY
   ├── UNIQUE
   ├── CHECK
   ├── DEFAULT
   └── NOT NULL
   │
   ▼
Valid?
 │
 ├── Yes → Store Data
 │
 └── No → Reject Operation
```

---

# Real-World Example

## Banking System

Rules:

* Account Number must be unique.
* Customer Name cannot be empty.
* Balance cannot be negative.
* Every transaction must belong to an existing account.

Possible constraints:

| Requirement              | Constraint  |
| ------------------------ | ----------- |
| Unique Account Number    | PRIMARY KEY |
| Customer Name Required   | NOT NULL    |
| Positive Balance         | CHECK       |
| Valid Customer Reference | FOREIGN KEY |

---

# Common Constraints Used Together

```sql
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Email VARCHAR(100) UNIQUE,
    Salary DECIMAL(10,2) CHECK (Salary >= 0),
    Department VARCHAR(50) DEFAULT 'General'
);
```

---

# Database Compatibility

| Constraint                  | MySQL |      PostgreSQL     |  SQL Server  | SQLite |
| --------------------------- | :---: | :-----------------: | :----------: | :----: |
| NOT NULL                    |   ✅   |          ✅          |       ✅      |    ✅   |
| UNIQUE                      |   ✅   |          ✅          |       ✅      |    ✅   |
| PRIMARY KEY                 |   ✅   |          ✅          |       ✅      |    ✅   |
| FOREIGN KEY                 |   ✅   |          ✅          |       ✅      |    ✅   |
| CHECK                       |   ✅*  |          ✅          |       ✅      |    ✅   |
| DEFAULT                     |   ✅   |          ✅          |       ✅      |    ✅   |
| AUTO_INCREMENT / Equivalent |   ✅   | ✅ (SERIAL/IDENTITY) | ✅ (IDENTITY) |    ✅   |

> *Modern MySQL versions enforce `CHECK` constraints. Older versions parsed but ignored them.

---

# Advantages

* Maintains data integrity.
* Prevents invalid data entry.
* Reduces duplicate data.
* Enforces business rules.
* Improves database reliability.
* Reduces application-side validation.

---

# Limitations

* Poorly designed constraints may reduce flexibility.
* Very complex constraints can slightly increase validation overhead.
* Database-specific syntax differs for some constraints.

---

# Common Mistakes

* Not defining a primary key.
* Allowing important columns to accept `NULL`.
* Forgetting to enforce relationships with foreign keys.
* Using too few or too many constraints.
* Assuming application validation alone is sufficient.

---

# Best Practices

* Define constraints during table creation whenever possible.
* Use meaningful constraint names.
* Choose the correct constraint for each business rule.
* Test constraints using valid and invalid data.
* Document constraints as part of the database design.

---

# Interview Questions

### 1. What is a constraint in SQL?

**Answer:** A constraint is a rule applied to one or more table columns to ensure that only valid and consistent data is stored.

---

### 2. Why are constraints important?

**Answer:** They maintain data integrity, prevent invalid data, enforce business rules, and improve database reliability.

---

### 3. Name the commonly used SQL constraints.

**Answer:**

* NOT NULL
* UNIQUE
* PRIMARY KEY
* FOREIGN KEY
* CHECK
* DEFAULT
* AUTO_INCREMENT / IDENTITY / SERIAL

---

### 4. Can constraints be added after creating a table?

**Answer:** Yes. Constraints can be added later using the `ALTER TABLE` statement, subject to existing data satisfying the constraint.

---

### 5. Which constraint uniquely identifies each row?

**Answer:** `PRIMARY KEY`

---

# Practice Questions

## Easy

1. What is a constraint?
2. Why are constraints used?
3. List five SQL constraints.
4. Which constraint prevents duplicate values?
5. Which constraint prevents `NULL` values?

---

## Medium

1. Explain the different types of SQL constraints.
2. Compare `PRIMARY KEY` and `UNIQUE`.
3. Explain entity integrity and referential integrity.
4. Create a table using multiple constraints.
5. Explain how constraints improve data quality.

---

## Hard

1. Explain how constraints help maintain database integrity.
2. Compare constraint support across MySQL, PostgreSQL, SQL Server, and SQLite.
3. Design a database schema with appropriate constraints for a banking application.
4. Discuss the advantages and limitations of database constraints.
5. Explain why database constraints are important even when application validation exists.

---

# Key Takeaways

* Constraints enforce rules on database tables.
* They ensure data integrity and consistency.
* SQL provides several built-in constraints such as `NOT NULL`, `UNIQUE`, `PRIMARY KEY`, `FOREIGN KEY`, `CHECK`, and `DEFAULT`.
* Constraints can be created during table creation or added later.
* Proper use of constraints results in reliable, accurate, and maintainable databases.

---

# Conclusion

Constraints are one of the most important features of relational databases because they protect the quality and consistency of stored data. By enforcing business rules directly within the database, they reduce errors, maintain relationships, and improve application reliability. In the next chapter, you will learn about the **`NOT NULL` constraint**, which ensures that mandatory columns always contain a value.
