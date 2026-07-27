# SQL Comments

# Introduction

When writing SQL queries, not every line is meant to be executed by the database. Developers often need to explain the purpose of a query, temporarily disable code for testing, or document important information.

For example:

* Explain what a query does.
* Mark sections of a long SQL script.
* Temporarily disable a query while debugging.
* Add author information or version history.

SQL provides **Comments** for these purposes.

Comments are ignored by the SQL engine during execution, making them useful for improving the readability and maintainability of SQL code.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand the purpose of SQL comments.
* Write single-line and multi-line comments.
* Use comments to document SQL scripts.
* Comment out SQL statements during debugging.
* Follow best practices for writing meaningful comments.

---

# Problem Statement

Consider the following SQL query.

```sql
SELECT *
FROM Employee
WHERE Salary > 50000;
```

Someone reading this query may not know:

* Why is the salary filtered?
* Is this report for HR?
* Is this a temporary query?
* Can it be removed later?

Adding comments makes the purpose clear.

---

# Why Do We Need SQL Comments?

SQL comments help to:

* Explain SQL statements.
* Improve code readability.
* Document business logic.
* Help team collaboration.
* Make maintenance easier.
* Temporarily disable SQL code during testing.

Without comments, SQL scripts become difficult to understand, especially in large projects.

---

# What are SQL Comments?

A **SQL Comment** is text written inside an SQL script that is ignored by the database engine during execution.

Comments are intended only for developers and database administrators.

---

# Types of SQL Comments

SQL supports two types of comments:

| Type                | Symbol      |
| ------------------- | ----------- |
| Single-Line Comment | `--`        |
| Multi-Line Comment  | `/* ... */` |

---

# 1. Single-Line Comment

A single-line comment begins with two hyphens (`--`).

Everything after `--` on that line is ignored.

## Syntax

```sql
-- Comment text
```

---

## Example

```sql
-- Display all employees
SELECT *
FROM Employee;
```

---

## Example with Query

```sql
SELECT *
FROM Employee
-- Show only active employees
WHERE Status = 'Active';
```

---

# 2. Multi-Line Comment

Multi-line comments begin with `/*` and end with `*/`.

Everything between them is ignored.

## Syntax

```sql
/*
Comment Line 1
Comment Line 2
*/
```

---

## Example

```sql
/*
Author : Sanjay
Project : Employee Management System
Version : 1.0
*/

SELECT *
FROM Employee;
```

---

# Commenting Out SQL Statements

Comments are often used to temporarily disable SQL statements.

Example:

```sql
-- DELETE FROM Employee;
```

The `DELETE` statement is ignored by the database.

---

## Multi-Line Example

```sql
/*
UPDATE Employee
SET Salary = Salary * 1.10;

DELETE FROM Employee;
*/
```

Both statements are ignored.

---

# Example 1 – Documenting a Query

```sql
-- Display employees earning more than £50,000

SELECT *
FROM Employee
WHERE Salary > 50000;
```

---

# Example 2 – Explaining Business Logic

```sql
-- Employees become eligible for bonus
-- after completing one year.

SELECT *
FROM Employee
WHERE Experience >= 1;
```

---

# Example 3 – Section Heading

```sql
/*==========================
 Employee Report
===========================*/

SELECT *
FROM Employee;
```

---

# Example 4 – Table Creation Script

```sql
/*
Table:
Employee

Purpose:
Stores employee information.
*/

CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    Salary DECIMAL(10,2)
);
```

---

# Internal Working

```text
Developer Writes SQL
        │
        ▼
SQL Parser Reads Script
        │
        ├── SQL Statements
        │         │
        │         ▼
        │   Execute
        │
        └── Comments
                  │
                  ▼
             Ignore
```

---

# Comments vs SQL Statements

| SQL Comment              | SQL Statement            |
| ------------------------ | ------------------------ |
| Ignored during execution | Executed by the database |
| Used for documentation   | Used for data operations |
| Helps developers         | Affects the database     |
| Improves readability     | Performs actual work     |

---

# Database Compatibility

| Feature              | MySQL | PostgreSQL | SQL Server | SQLite |
| -------------------- | :---: | :--------: | :--------: | :----: |
| Single-Line (`--`)   |   ✅   |      ✅     |      ✅     |    ✅   |
| Multi-Line (`/* */`) |   ✅   |      ✅     |      ✅     |    ✅   |
| Comments in Scripts  |   ✅   |      ✅     |      ✅     |    ✅   |

---

# Real-World Applications

| Industry   | Example                         |
| ---------- | ------------------------------- |
| Banking    | Explain financial reports       |
| HR         | Document payroll queries        |
| Hospital   | Describe patient reports        |
| E-Commerce | Explain sales reports           |
| School     | Document student queries        |
| Library    | Explain book management scripts |

---

# Advantages

* Improves readability.
* Helps team collaboration.
* Documents business logic.
* Makes debugging easier.
* Simplifies maintenance.
* Prevents confusion in large SQL scripts.

---

# Limitations

* Comments do not improve query performance.
* Outdated comments can become misleading.
* Excessive comments may reduce readability.
* Sensitive information should never be placed in comments.

---

# Common Mistakes

* Writing comments that no longer match the SQL code.
* Commenting every obvious line unnecessarily.
* Forgetting to remove temporary debugging comments.
* Including passwords, API keys, or confidential information in comments.
* Forgetting to close a multi-line comment (`*/`).

---

# Best Practices

* Write meaningful and concise comments.
* Explain **why** the query exists rather than **what** obvious SQL syntax does.
* Update comments whenever the SQL code changes.
* Use comments to separate major sections of long scripts.
* Avoid storing sensitive information in comments.
* Remove obsolete comments before deploying to production.

---

# Interview Questions

### 1. What is a SQL comment?

**Answer:** A SQL comment is text inside a SQL script that is ignored by the database engine and is used to document or explain the code.

---

### 2. How many types of SQL comments are available?

**Answer:** Two:

* Single-line comments (`--`)
* Multi-line comments (`/* ... */`)

---

### 3. Why are SQL comments important?

**Answer:** They improve readability, document business logic, support collaboration, and simplify maintenance.

---

### 4. Can SQL comments affect query execution?

**Answer:** No. SQL comments are ignored by the database engine and do not affect query execution.

---

### 5. Can SQL comments be used to disable SQL statements?

**Answer:** Yes. Developers often comment out SQL statements temporarily during testing and debugging.

---

# Practice Questions

## Easy

1. What is a SQL comment?
2. Write the syntax for a single-line comment.
3. Write the syntax for a multi-line comment.
4. Why are comments used?
5. Are SQL comments executed by the database?

---

## Medium

1. Write a SQL script using both types of comments.
2. Explain the difference between single-line and multi-line comments.
3. Comment out a `DELETE` statement.
4. Create a documented `CREATE TABLE` script.
5. Explain how comments improve maintainability.

---

## Hard

1. Design a well-documented SQL script for an Employee Management System.
2. Explain best practices for writing SQL comments in enterprise projects.
3. Compare SQL comments across MySQL, PostgreSQL, SQL Server, and SQLite.
4. Explain how SQL parsers treat comments during execution.
5. Discuss the risks of outdated or poorly written comments.

---

# Key Takeaways

* SQL comments improve the readability and maintainability of SQL scripts.
* SQL supports two comment styles:

  * `--` for single-line comments.
  * `/* ... */` for multi-line comments.
* Comments are ignored during execution.
* Comments are useful for documentation, debugging, and collaboration.
* Well-written comments make SQL code easier to understand and maintain.

---

# Conclusion

SQL comments are an essential part of writing professional and maintainable SQL code. Although they do not affect query execution, they help developers understand business logic, organise scripts, and simplify debugging. Good commenting practices make SQL scripts easier to maintain, especially in team environments and large database projects. In the next chapter, you will learn about **SQL Data Types**, which define the kind of values that can be stored in database columns.
