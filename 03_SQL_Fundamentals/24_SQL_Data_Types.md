# SQL Data Types

# Introduction

Every value stored in a database has a specific type. For example:

* A student's name is text.
* An employee's salary is a decimal number.
* A customer's age is an integer.
* An order date is a date.
* A profile picture is an image.

To store these different kinds of values correctly and efficiently, SQL uses **Data Types**.

A **Data Type** defines the kind of data that a column can store, how much storage it requires, the range of valid values, and the operations that can be performed on it.

Choosing the correct data type is one of the most important decisions in database design because it directly affects:

* Storage space
* Query performance
* Data accuracy
* Data integrity
* Application scalability

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand what SQL data types are.
* Learn the major categories of SQL data types.
* Choose appropriate data types for different scenarios.
* Compare commonly used SQL data types.
* Understand database-specific data type differences.
* Follow best practices for selecting data types.

---

# Problem Statement

Suppose we are creating an **Employee** table.

What data type should each column use?

| Column       | Example Value |
| ------------ | ------------- |
| EmployeeID   | 101           |
| EmployeeName | Rahul Sharma  |
| Salary       | 55000.75      |
| JoiningDate  | 2026-08-01    |
| IsActive     | TRUE          |
| ProfilePhoto | Image File    |

Using incorrect data types can cause:

* Wasted storage
* Invalid data
* Poor performance
* Difficult maintenance

The solution is to choose the correct SQL data type for every column.

---

# Why Do We Need Data Types?

Data types help to:

* Store data efficiently.
* Validate input values.
* Improve query performance.
* Reduce storage requirements.
* Prevent invalid data.
* Support mathematical and date operations.

Without proper data types, databases become inefficient and error-prone.

---

# What is a SQL Data Type?

A **SQL Data Type** specifies the type of value that can be stored in a column.

For example:

* Numbers → `INT`
* Text → `VARCHAR`
* Dates → `DATE`
* Boolean values → `BOOLEAN`
* Images → `BLOB`

The database uses the data type to validate and store values correctly.

---

# Categories of SQL Data Types

SQL data types can be grouped into the following categories.

| Category         | Examples                        |
| ---------------- | ------------------------------- |
| Numeric          | INT, BIGINT, DECIMAL, FLOAT     |
| Character/String | CHAR, VARCHAR, TEXT             |
| Date & Time      | DATE, TIME, DATETIME, TIMESTAMP |
| Boolean          | BOOLEAN, BIT                    |
| Binary           | BINARY, VARBINARY, BLOB         |

---

# 1. Numeric Data Types

Numeric data types store whole numbers and decimal values.

## Common Numeric Types

| Data Type    | Description                   | Example     |
| ------------ | ----------------------------- | ----------- |
| TINYINT      | Small integer                 | 25          |
| SMALLINT     | Small whole number            | 1500        |
| INT          | Standard integer              | 100000      |
| BIGINT       | Very large integer            | 9876543210  |
| DECIMAL(p,s) | Exact decimal number          | 1250.75     |
| NUMERIC(p,s) | Exact decimal number          | 999.99      |
| FLOAT        | Approximate decimal           | 10.56       |
| DOUBLE       | High precision floating point | 1500.987654 |

---

## Example

```sql
CREATE TABLE Product (
    ProductID INT,
    Price DECIMAL(10,2),
    Quantity INT
);
```

---

# 2. Character (String) Data Types

Character data types store text values.

| Data Type  | Description          | Example               |
| ---------- | -------------------- | --------------------- |
| CHAR(n)    | Fixed-length text    | "ABC"                 |
| VARCHAR(n) | Variable-length text | "Rahul"               |
| TEXT       | Large text           | Description paragraph |

---

## CHAR vs VARCHAR

| CHAR                         | VARCHAR                       |
| ---------------------------- | ----------------------------- |
| Fixed length                 | Variable length               |
| Faster for fixed-size values | Saves storage                 |
| Pads unused spaces           | Stores only actual characters |

---

## Example

```sql
CREATE TABLE Employee (
    EmployeeName VARCHAR(100),
    Department CHAR(5)
);
```

---

# 3. Date and Time Data Types

These store dates and times.

| Data Type | Description                                                 | Example             |
| --------- | ----------------------------------------------------------- | ------------------- |
| DATE      | Date only                                                   | 2026-08-01          |
| TIME      | Time only                                                   | 14:30:00            |
| DATETIME  | Date and time                                               | 2026-08-01 14:30:00 |
| TIMESTAMP | Date and time with automatic tracking support in many DBMSs | 2026-08-01 14:30:00 |
| YEAR*     | Year only (MySQL specific)                                  | 2026                |

> *`YEAR` is a MySQL-specific data type and is not part of the SQL standard.

---

## Example

```sql
CREATE TABLE Attendance (
    AttendanceDate DATE,
    LoginTime TIME,
    LoginTimestamp TIMESTAMP
);
```

---

# 4. Boolean Data Types

Boolean types store logical values.

| Value | Meaning |
| ----- | ------- |
| TRUE  | Yes     |
| FALSE | No      |

Common implementations:

| Database   | Type                                    |
| ---------- | --------------------------------------- |
| MySQL      | BOOLEAN (alias of TINYINT(1))           |
| PostgreSQL | BOOLEAN                                 |
| SQL Server | BIT                                     |
| SQLite     | BOOLEAN (stored using integer affinity) |

---

## Example

```sql
CREATE TABLE Employee (
    EmployeeID INT,
    IsActive BOOLEAN
);
```

---

# 5. Binary Data Types

Binary data types store binary information.

| Data Type | Purpose                     |
| --------- | --------------------------- |
| BINARY    | Fixed binary data           |
| VARBINARY | Variable-length binary data |
| BLOB      | Large binary objects        |

Examples:

* Images
* Videos
* Audio
* PDF files

---

# Example

```sql
CREATE TABLE Documents (
    DocumentID INT,
    FileData BLOB
);
```

---

# Complete Example

```sql
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    Age INT,
    Salary DECIMAL(10,2),
    JoiningDate DATE,
    IsActive BOOLEAN,
    Resume BLOB
);
```

---

# Sample Output

| EmployeeID | EmployeeName | Age |   Salary | JoiningDate | IsActive |
| ---------- | ------------ | --: | -------: | ----------- | :------: |
| 101        | Rahul        |  24 | 55000.50 | 2026-08-01  |   TRUE   |
| 102        | Priya        |  26 | 62000.00 | 2026-08-05  |   TRUE   |

---

# Internal Working

```text
User Input
     │
     ▼
Column Data Type
     │
     ▼
Database Validation
     │
     ├── Correct Type
     │        │
     │        ▼
     │   Store Value
     │
     └── Wrong Type
              │
              ▼
          Reject Value
```

---

# Choosing the Right Data Type

| Requirement       | Recommended Data Type |
| ----------------- | --------------------- |
| Employee ID       | INT                   |
| Product Price     | DECIMAL(10,2)         |
| Customer Name     | VARCHAR(100)          |
| Country Code      | CHAR(2)               |
| Birth Date        | DATE                  |
| Login Time        | TIME                  |
| Login Date & Time | TIMESTAMP             |
| Active Status     | BOOLEAN               |
| Product Image     | BLOB                  |

---

# Data Type Comparison

| Data Type | Best Used For    | Variable Length |
| --------- | ---------------- | :-------------: |
| CHAR      | Fixed codes      |        ❌        |
| VARCHAR   | Names, emails    |        ✅        |
| INT       | Whole numbers    |        ❌        |
| DECIMAL   | Financial values |        ❌        |
| DATE      | Calendar dates   |        ❌        |
| BOOLEAN   | True/False       |        ❌        |
| BLOB      | Binary files     |        ✅        |

---

# Database Compatibility

| Data Type | MySQL | PostgreSQL |   SQL Server   |      SQLite      |
| --------- | :---: | :--------: | :------------: | :--------------: |
| INT       |   ✅   |      ✅     |        ✅       |         ✅        |
| BIGINT    |   ✅   |      ✅     |        ✅       |         ✅        |
| DECIMAL   |   ✅   |      ✅     |        ✅       |         ✅        |
| VARCHAR   |   ✅   |      ✅     |        ✅       |         ✅        |
| CHAR      |   ✅   |      ✅     |        ✅       |         ✅        |
| TEXT      |   ✅   |      ✅     |        ✅       |         ✅        |
| DATE      |   ✅   |      ✅     |        ✅       |         ✅        |
| TIME      |   ✅   |      ✅     |        ✅       |         ✅        |
| TIMESTAMP |   ✅   |      ✅     |       ✅*       |         ✅        |
| BOOLEAN   |   ✅   |      ✅     |       BIT      | Integer affinity |
| BLOB      |   ✅   |    BYTEA   | VARBINARY(MAX) |       BLOB       |

> *SQL Server provides both `DATETIME2` and `TIMESTAMP`/`ROWVERSION`. `ROWVERSION` is **not** a date/time type; `DATETIME2` is generally recommended for storing date and time values.

---

# Real-World Applications

| Industry   | Data Type Examples                      |
| ---------- | --------------------------------------- |
| School     | StudentID, Name, DOB                    |
| Banking    | AccountNumber, Balance, TransactionDate |
| Hospital   | PatientID, Diagnosis, AppointmentDate   |
| HR         | EmployeeID, Salary, JoiningDate         |
| E-Commerce | ProductID, Price, Stock                 |
| Library    | BookID, ISBN, PublishedDate             |

---

# Advantages

* Ensures valid data storage.
* Improves query performance.
* Reduces storage usage.
* Supports efficient indexing.
* Enables accurate calculations and comparisons.

---

# Limitations

* Incorrect data type selection can waste storage.
* Database systems may use different names for similar data types.
* Changing data types later can require schema modifications and data migration.

---

# Common Mistakes

* Using `VARCHAR` for numeric values.
* Using `FLOAT` for financial data instead of `DECIMAL`.
* Choosing a `VARCHAR` length that is unnecessarily large.
* Using `CHAR` for variable-length text.
* Storing dates as plain text instead of `DATE` or `TIMESTAMP`.

---

# Best Practices

* Choose the smallest suitable data type.
* Use `DECIMAL` for financial values.
* Use `VARCHAR` for variable-length text.
* Use `CHAR` only for fixed-length values such as country codes.
* Store dates using date/time data types instead of strings.
* Review database-specific data type behaviour before designing schemas.

---

# Interview Questions

### 1. What is a SQL data type?

**Answer:** A SQL data type defines the kind of data that a column can store and how the database stores and validates that data.

---

### 2. Why are data types important?

**Answer:** They improve storage efficiency, validate data, enhance performance, and ensure data integrity.

---

### 3. What is the difference between `CHAR` and `VARCHAR`?

**Answer:**

| CHAR                           | VARCHAR                           |
| ------------------------------ | --------------------------------- |
| Fixed length                   | Variable length                   |
| Pads unused spaces             | Stores only actual characters     |
| Suitable for fixed-size values | Suitable for variable-length text |

---

### 4. Why should `DECIMAL` be used instead of `FLOAT` for financial data?

**Answer:** `DECIMAL` stores exact numeric values, making it suitable for financial calculations, while `FLOAT` stores approximate values and may introduce rounding errors.

---

### 5. Which data type is commonly used for images and files?

**Answer:** `BLOB` (or the equivalent binary large object type provided by the database system).

---

# Practice Questions

## Easy

1. What is a SQL data type?
2. List the major categories of SQL data types.
3. What is the difference between `CHAR` and `VARCHAR`?
4. Which data type stores dates?
5. Which data type stores Boolean values?

---

## Medium

1. Create an `Employee` table using appropriate data types.
2. Compare `INT` and `BIGINT`.
3. Compare `CHAR` and `VARCHAR`.
4. Explain the difference between `DECIMAL` and `FLOAT`.
5. Describe the purpose of binary data types.

---

## Hard

1. Design a database schema for an e-commerce application using suitable data types.
2. Compare SQL data types across MySQL, PostgreSQL, SQL Server, and SQLite.
3. Explain how choosing the correct data type improves performance.
4. Discuss the advantages and limitations of different numeric data types.
5. Recommend suitable data types for a banking database and justify your choices.

---

# Key Takeaways

* SQL data types define the kind of data that can be stored in each column.
* Selecting the correct data type improves performance, storage efficiency, and data integrity.
* Major categories include numeric, character, date/time, Boolean, and binary types.
* Different database systems provide similar data types with slight variations.
* Choosing appropriate data types is a fundamental part of good database design.

---

# Conclusion

SQL data types form the foundation of every database table by determining how information is stored, validated, and processed. Selecting the appropriate data type improves performance, conserves storage, and ensures accurate data handling. Understanding the strengths and limitations of each data type enables developers to design efficient, scalable, and reliable databases. In the next chapter, you will learn about **Common Beginner Mistakes in SQL**, including practical examples of errors and how to avoid them.
