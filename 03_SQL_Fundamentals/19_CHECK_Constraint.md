# CHECK Constraint

# Introduction

Not all values entered into a database are valid. For example:

* A student's age cannot be negative.
* An employee's salary cannot be less than 0.
* A product's price cannot be negative.
* A student's grade should only be A, B, C, D, or F.

If invalid values are stored, the database becomes unreliable and business rules are violated.

The **CHECK** constraint allows us to define a condition that every value in a column (or combination of columns) must satisfy before it can be stored.

In this chapter, you will learn what the `CHECK` constraint is, why it is important, how to create it, and how it helps maintain data integrity.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand the purpose of the `CHECK` constraint.
* Create tables using `CHECK`.
* Add a `CHECK` constraint to an existing table.
* Apply multiple `CHECK` constraints.
* Understand how the database validates `CHECK` conditions.
* Follow best practices when using `CHECK`.

---

# Problem Statement

Suppose we create the following **Student** table.

```sql
CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(100),
    Age INT
);
```

Now consider the following data.

| StudentID | Name  | Age |
| --------- | ----- | --: |
| 101       | Rahul |  20 |
| 102       | Priya |  -5 |
| 103       | Arun  | 150 |

Problems:

* Age cannot be negative.
* Age should fall within a valid range.

The solution is to use the **CHECK** constraint.

---

# Why Do We Need CHECK?

The `CHECK` constraint helps to:

* Prevent invalid data.
* Enforce business rules.
* Improve data quality.
* Reduce application-side validation.
* Maintain database consistency.

Without a `CHECK` constraint, invalid values can be stored unless every application validates them.

---

# What is a CHECK Constraint?

A **CHECK** constraint specifies a condition that every inserted or updated value must satisfy.

Whenever data is inserted or updated, the database evaluates the condition.

* If the condition is **TRUE**, the operation succeeds.
* If the condition is **FALSE**, the operation is rejected.

---

# Syntax

## Column-Level CHECK

```sql
CREATE TABLE table_name (
    column_name data_type
    CHECK (condition)
);
```

---

## Table-Level CHECK

```sql
CREATE TABLE table_name (
    column1 data_type,
    column2 data_type,
    CHECK (condition)
);
```

---

# Example 1 – Age Validation

```sql
CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(100),
    Age INT CHECK (Age >= 18)
);
```

Only students aged **18 or above** can be inserted.

---

# Example 2 – Salary Validation

```sql
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(100),
    Salary DECIMAL(10,2)
    CHECK (Salary >= 0)
);
```

Negative salaries are not allowed.

---

# Example 3 – Grade Validation

```sql
CREATE TABLE Result (
    StudentID INT,
    Grade CHAR(1)
    CHECK (Grade IN ('A', 'B', 'C', 'D', 'F'))
);
```

Only valid grades can be stored.

---

# Example 4 – Price Validation

```sql
CREATE TABLE Product (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100),
    Price DECIMAL(10,2)
    CHECK (Price > 0)
);
```

Products must have a positive price.

---

# Valid Insert

```sql
INSERT INTO Student
VALUES (
    101,
    'Rahul',
    20
);
```

### Result

The record is inserted successfully because the condition is satisfied.

---

# Invalid Insert

```sql
INSERT INTO Student
VALUES (
    102,
    'Priya',
    16
);
```

### Result

❌ Error

Reason:

The value **16** violates the condition:

```sql
CHECK (Age >= 18)
```

---

# Multiple CHECK Constraints

A table can contain more than one `CHECK` constraint.

```sql
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY,
    Age INT CHECK (Age >= 18),
    Salary DECIMAL(10,2)
        CHECK (Salary >= 0)
);
```

Both conditions must be satisfied.

---

# Table-Level CHECK Example

A table-level constraint can validate multiple columns together.

```sql
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY,
    JoiningDate DATE,
    RetirementDate DATE,
    CHECK (RetirementDate > JoiningDate)
);
```

This ensures the retirement date is after the joining date.

---

# Adding CHECK to an Existing Table

## MySQL

```sql
ALTER TABLE Employee
ADD CONSTRAINT CHK_Salary
CHECK (Salary >= 0);
```

---

## PostgreSQL

```sql
ALTER TABLE Employee
ADD CONSTRAINT CHK_Salary
CHECK (Salary >= 0);
```

---

## SQL Server

```sql
ALTER TABLE Employee
ADD CONSTRAINT CHK_Salary
CHECK (Salary >= 0);
```

---

## SQLite

SQLite supports `CHECK` constraints during table creation. Adding new `CHECK` constraints to existing tables generally requires creating a new table and copying the data.

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
CHECK Constraint
   │
   ▼
Condition True?
 │
 ├── Yes → Store Data
 │
 └── No → Reject Operation
```

---

# Common CHECK Expressions

| Business Rule       | CHECK Constraint                                |
| ------------------- | ----------------------------------------------- |
| Age ≥ 18            | `CHECK (Age >= 18)`                             |
| Salary ≥ 0          | `CHECK (Salary >= 0)`                           |
| Price > 0           | `CHECK (Price > 0)`                             |
| Marks Between 0–100 | `CHECK (Marks BETWEEN 0 AND 100)`               |
| Gender Validation   | `CHECK (Gender IN ('Male', 'Female', 'Other'))` |
| Quantity Positive   | `CHECK (Quantity > 0)`                          |

---

# Real-World Applications

| Industry   | CHECK Example                   |
| ---------- | ------------------------------- |
| School     | Age must be at least 18         |
| Banking    | Balance cannot be negative      |
| Hospital   | Patient age must be positive    |
| HR         | Salary must be non-negative     |
| E-Commerce | Price must be greater than zero |
| Library    | Fine amount cannot be negative  |

---

# Database Compatibility

| Feature                    | MySQL | PostgreSQL | SQL Server |   SQLite  |
| -------------------------- | :---: | :--------: | :--------: | :-------: |
| CHECK Constraint           |   ✅*  |      ✅     |      ✅     |     ✅     |
| Multiple CHECK Constraints |   ✅   |      ✅     |      ✅     |     ✅     |
| Table-Level CHECK          |   ✅   |      ✅     |      ✅     |     ✅     |
| Add Using `ALTER TABLE`    |   ✅   |      ✅     |      ✅     | Limited** |

> *Modern versions of MySQL enforce `CHECK` constraints. Older versions accepted the syntax but ignored the constraint.

> **SQLite usually requires recreating the table to add new `CHECK` constraints.

---

# Advantages

* Enforces business rules at the database level.
* Prevents invalid values.
* Improves data integrity.
* Reduces application-side validation.
* Supports complex validation rules.

---

# Limitations

* Cannot reference data in other tables.
* Existing data must satisfy the condition before adding the constraint.
* Complex conditions may slightly increase validation overhead.
* Some database systems differ in implementation details.

---

# Common Mistakes

* Writing incorrect logical conditions.
* Assuming `CHECK` can validate values in another table.
* Forgetting to validate existing data before adding the constraint.
* Using overly complex conditions.
* Relying only on application validation.

---

# Best Practices

* Keep `CHECK` conditions simple and meaningful.
* Use descriptive constraint names.
* Validate existing data before adding constraints.
* Use `CHECK` for business rules that belong in the database.
* Test both valid and invalid inputs.

---

# Interview Questions

### 1. What is the purpose of the `CHECK` constraint?

**Answer:** It ensures that inserted or updated values satisfy a specified condition.

---

### 2. Can a table have multiple `CHECK` constraints?

**Answer:** Yes. A table can have multiple `CHECK` constraints on different columns or conditions.

---

### 3. Can `CHECK` validate multiple columns?

**Answer:** Yes. A table-level `CHECK` constraint can validate conditions involving multiple columns.

---

### 4. What happens if a `CHECK` condition fails?

**Answer:** The database rejects the insert or update operation and returns a constraint violation error.

---

### 5. Can a `CHECK` constraint reference another table?

**Answer:** No. A `CHECK` constraint validates only the values within the current row. Relationships between tables should be enforced using a `FOREIGN KEY`.

---

# Practice Questions

## Easy

1. What is a `CHECK` constraint?
2. Why is a `CHECK` constraint used?
3. Write the syntax for creating a `CHECK` constraint.
4. Can a table have multiple `CHECK` constraints?
5. Give two examples of business rules that can use `CHECK`.

---

## Medium

1. Create a `Student` table with an age validation rule.
2. Add a `CHECK` constraint to an existing table.
3. Explain the difference between column-level and table-level `CHECK`.
4. Write a `CHECK` constraint for valid grades.
5. Explain how the database validates `CHECK` constraints.

---

## Hard

1. Design an employee table with multiple `CHECK` constraints.
2. Compare `CHECK` constraint support across MySQL, PostgreSQL, SQL Server, and SQLite.
3. Explain the internal working of the `CHECK` constraint.
4. Discuss the advantages and limitations of `CHECK`.
5. Design a database for an online store using appropriate `CHECK` constraints.

---

# Key Takeaways

* A `CHECK` constraint enforces business rules on column values.
* Data must satisfy the defined condition before being stored.
* `CHECK` can be applied at both the column level and the table level.
* Multiple `CHECK` constraints can exist in a single table.
* Using `CHECK` improves data quality and consistency.

---

# Conclusion

The `CHECK` constraint is a powerful feature for enforcing business rules directly within a database. By validating data during `INSERT` and `UPDATE` operations, it prevents invalid values from being stored and improves overall data integrity. Combined with other constraints such as `NOT NULL`, `UNIQUE`, `PRIMARY KEY`, and `FOREIGN KEY`, the `CHECK` constraint plays an important role in building secure, reliable, and well-designed relational databases. In the next chapter, you will learn about the **`DEFAULT` constraint**, which automatically assigns default values when no value is provided.
