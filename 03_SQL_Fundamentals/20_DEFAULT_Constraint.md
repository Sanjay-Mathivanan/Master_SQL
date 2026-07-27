# DEFAULT Constraint

# Introduction

In many real-world applications, some columns should automatically receive a predefined value when the user does not provide one.

For example:

* A newly registered user's status should be **'Active'**.
* A new employee's joining date should default to the current date.
* A product's stock quantity should start at **0**.
* A customer's country should default to **'India'**.

Instead of requiring users or applications to provide these values every time, SQL provides the **DEFAULT** constraint.

The **DEFAULT** constraint automatically assigns a predefined value to a column whenever an `INSERT` statement does not specify a value for that column.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand the purpose of the `DEFAULT` constraint.
* Create tables using `DEFAULT`.
* Add a `DEFAULT` constraint to an existing table.
* Use built-in functions as default values.
* Understand how the database applies default values.
* Follow best practices when using `DEFAULT`.

---

# Problem Statement

Suppose we create the following **Employee** table.

```sql
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(100),
    Status VARCHAR(20),
    JoiningDate DATE
);
```

Now insert the following record.

```sql
INSERT INTO Employee (EmployeeID, Name)
VALUES (101, 'Rahul');
```

Result:

| EmployeeID | Name  | Status | JoiningDate |
| ---------- | ----- | ------ | ----------- |
| 101        | Rahul | NULL   | NULL        |

Problems:

* Employee status is missing.
* Joining date is missing.

The solution is to use the **DEFAULT** constraint.

---

# Why Do We Need DEFAULT?

The `DEFAULT` constraint helps to:

* Automatically assign standard values.
* Reduce repetitive data entry.
* Improve data consistency.
* Minimize application logic.
* Prevent unnecessary `NULL` values.

Without a `DEFAULT` constraint, applications often need additional code to assign common values.

---

# What is the DEFAULT Constraint?

A **DEFAULT** constraint specifies a value that SQL automatically inserts into a column **when no value is provided** during an `INSERT` operation.

The default value is used **only if the column is omitted** from the `INSERT` statement or the `DEFAULT` keyword is explicitly used.

---

# Syntax

## During Table Creation

```sql
CREATE TABLE table_name (
    column_name data_type
    DEFAULT default_value
);
```

---

# Example 1 – Default Status

```sql
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(100),
    Status VARCHAR(20) DEFAULT 'Active'
);
```

---

# Example 2 – Default Country

```sql
CREATE TABLE Customer (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(100),
    Country VARCHAR(50) DEFAULT 'India'
);
```

---

# Example 3 – Default Quantity

```sql
CREATE TABLE Product (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100),
    Stock INT DEFAULT 0
);
```

---

# Example 4 – Current Date

Most database systems allow built-in functions as default values.

```sql
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(100),
    JoiningDate DATE DEFAULT CURRENT_DATE
);
```

> Some database systems use equivalent functions such as `GETDATE()` (SQL Server) or `CURRENT_TIMESTAMP` depending on the data type.

---

# Valid Insert (Using DEFAULT)

```sql
INSERT INTO Employee (
    EmployeeID,
    Name
)
VALUES (
    101,
    'Rahul'
);
```

### Result

| EmployeeID | Name  | Status |
| ---------- | ----- | ------ |
| 101        | Rahul | Active |

Since no value was provided for `Status`, SQL automatically inserted the default value.

---

# Insert with Explicit Value

```sql
INSERT INTO Employee (
    EmployeeID,
    Name,
    Status
)
VALUES (
    102,
    'Priya',
    'Inactive'
);
```

### Result

| EmployeeID | Name  | Status   |
| ---------- | ----- | -------- |
| 102        | Priya | Inactive |

The explicitly provided value overrides the default.

---

# Using the DEFAULT Keyword

You can explicitly request the default value.

```sql
INSERT INTO Employee
VALUES (
    103,
    'Arun',
    DEFAULT
);
```

Result:

| EmployeeID | Name | Status |
| ---------- | ---- | ------ |
| 103        | Arun | Active |

---

# Adding DEFAULT to an Existing Table

## MySQL

```sql
ALTER TABLE Employee
ALTER Status
SET DEFAULT 'Active';
```

---

## PostgreSQL

```sql
ALTER TABLE Employee
ALTER COLUMN Status
SET DEFAULT 'Active';
```

---

## SQL Server

```sql
ALTER TABLE Employee
ADD CONSTRAINT DF_Employee_Status
DEFAULT 'Active'
FOR Status;
```

---

## SQLite

SQLite supports `DEFAULT` values during table creation. Changing an existing default value often requires recreating the table.

---

# Internal Working

```text
User
   │
   ▼
INSERT Statement
   │
   ▼
Value Provided?
 │
 ├── Yes
 │      │
 │      ▼
 │  Store User Value
 │
 └── No
        │
        ▼
Apply DEFAULT Value
        │
        ▼
Store Data
```

---

# DEFAULT vs NULL

| DEFAULT                                           | NULL                               |
| ------------------------------------------------- | ---------------------------------- |
| Automatically assigns a predefined value          | Represents missing or unknown data |
| Applied during `INSERT` when no value is supplied | Stored only when permitted         |
| Improves consistency                              | Indicates absence of data          |

---

# DEFAULT vs NOT NULL

| DEFAULT                        | NOT NULL                      |
| ------------------------------ | ----------------------------- |
| Provides a value automatically | Requires a value to exist     |
| Can be used alone              | Prevents `NULL` values        |
| Often used together            | Often combined with `DEFAULT` |

Example:

```sql
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY,
    Status VARCHAR(20)
        NOT NULL
        DEFAULT 'Active'
);
```

---

# Common DEFAULT Values

| Column      | Default Value     |
| ----------- | ----------------- |
| Status      | 'Active'          |
| Stock       | 0                 |
| Quantity    | 0                 |
| Country     | 'India'           |
| JoiningDate | CURRENT_DATE      |
| CreatedAt   | CURRENT_TIMESTAMP |

---

# Real-World Applications

| Industry   | DEFAULT Example                            |
| ---------- | ------------------------------------------ |
| HR         | Employee status defaults to 'Active'       |
| Banking    | Account balance starts at 0                |
| School     | Admission status defaults to 'Pending'     |
| E-Commerce | Product stock defaults to 0                |
| Hospital   | Registration date defaults to current date |
| Library    | Book availability defaults to 'Available'  |

---

# Database Compatibility

| Feature                 | MySQL | PostgreSQL | SQL Server |   SQLite  |
| ----------------------- | :---: | :--------: | :--------: | :-------: |
| DEFAULT Constraint      |   ✅   |      ✅     |      ✅     |     ✅     |
| String Defaults         |   ✅   |      ✅     |      ✅     |     ✅     |
| Numeric Defaults        |   ✅   |      ✅     |      ✅     |     ✅     |
| Built-in Functions      |   ✅   |      ✅     |      ✅     |     ✅*    |
| Add Using `ALTER TABLE` |   ✅   |      ✅     |      ✅     | Limited** |

> *SQLite supports expressions such as `CURRENT_DATE` and `CURRENT_TIMESTAMP`.

> **Changing existing default definitions in SQLite often requires recreating the table.

---

# Advantages

* Reduces repetitive data entry.
* Ensures consistent default values.
* Simplifies application code.
* Minimizes unnecessary `NULL` values.
* Improves database usability.

---

# Limitations

* Default values are applied only when no value is provided.
* An explicitly supplied value always overrides the default.
* Existing rows are not automatically updated when a new default is added.
* Syntax differs slightly between database systems.

---

# Common Mistakes

* Assuming the default value is applied when `NULL` is explicitly inserted.
* Using an inappropriate default value.
* Forgetting that application code can override defaults.
* Confusing `DEFAULT` with `NOT NULL`.
* Not testing database-specific syntax.

---

# Best Practices

* Use meaningful default values that match business requirements.
* Combine `DEFAULT` with `NOT NULL` for mandatory columns when appropriate.
* Name default constraints clearly in SQL Server.
* Use built-in date and time functions instead of hard-coded dates.
* Document default values in the database schema.

---

# Interview Questions

### 1. What is the purpose of the `DEFAULT` constraint?

**Answer:** It automatically assigns a predefined value when no value is supplied during an `INSERT` operation.

---

### 2. When is a default value applied?

**Answer:** When a column is omitted from an `INSERT` statement or the `DEFAULT` keyword is explicitly used.

---

### 3. Can an explicit value override the default?

**Answer:** Yes. If a value is provided, SQL stores that value instead of the default.

---

### 4. Can `DEFAULT` be combined with `NOT NULL`?

**Answer:** Yes. This is a common practice to ensure every row has a valid value.

---

### 5. Does adding a default value update existing rows?

**Answer:** No. It affects only future inserts unless existing rows are updated separately.

---

# Practice Questions

## Easy

1. What is the purpose of the `DEFAULT` constraint?
2. Write the syntax for creating a default value.
3. Give three examples of commonly used default values.
4. Can a user override a default value?
5. What happens if a column is omitted from an `INSERT` statement?

---

## Medium

1. Create an `Employee` table with a default status.
2. Add a default value to an existing table.
3. Explain the internal working of the `DEFAULT` constraint.
4. Compare `DEFAULT` and `NOT NULL`.
5. Compare `DEFAULT` and `NULL`.

---

## Hard

1. Design a database for an e-commerce application using appropriate default values.
2. Compare `DEFAULT` support across MySQL, PostgreSQL, SQL Server, and SQLite.
3. Explain how built-in functions are used as default values.
4. Discuss the advantages and limitations of the `DEFAULT` constraint.
5. Explain best practices for using default values in enterprise database systems.

---

# Key Takeaways

* The `DEFAULT` constraint automatically assigns predefined values.
* It reduces repetitive data entry and improves consistency.
* Explicit values always override the default.
* `DEFAULT` is commonly combined with `NOT NULL`.
* Built-in functions such as `CURRENT_DATE` and `CURRENT_TIMESTAMP` are commonly used as default values.

---

# Conclusion

The `DEFAULT` constraint simplifies database design by automatically assigning predefined values whenever data is not supplied. It improves consistency, reduces repetitive input, and minimizes application-side logic. When combined with constraints such as `NOT NULL`, `PRIMARY KEY`, and `CHECK`, it helps create reliable and well-structured databases. In the next chapter, you will learn about the **`AUTO_INCREMENT` constraint**, which automatically generates unique numeric values for identifier columns.
