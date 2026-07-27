# Select Data

# Introduction

After inserting data into a table, the next step is to retrieve it. The **`SELECT`** statement is the most frequently used SQL command because it allows you to fetch data from one or more tables.

Whether you're displaying customer details in a banking application, viewing products in an e-commerce website, or generating student reports in a college management system, the `SELECT` statement is used behind the scenes.

In this chapter, you will learn how to retrieve data from tables using different forms of the `SELECT` statement.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand the purpose of the `SELECT` statement.
* Retrieve all columns from a table.
* Retrieve specific columns.
* Use column aliases.
* Perform simple calculations using `SELECT`.
* Understand how SQL processes a query.
* Follow best practices when retrieving data.

---

# Problem Statement

Suppose the **Student** table contains the following records.

| StudentID | Name  | Age | Department | Email                                         |
| --------- | ----- | --- | ---------- | --------------------------------------------- |
| 101       | Rahul | 20  | CSE        | [rahul@example.com](mailto:rahul@example.com) |
| 102       | Priya | 19  | AI         | [priya@example.com](mailto:priya@example.com) |
| 103       | Arun  | 21  | ECE        | [arun@example.com](mailto:arun@example.com)   |
| 104       | Sneha | 20  | IT         | [sneha@example.com](mailto:sneha@example.com) |

How can we:

* Display all students?
* Display only names?
* Display names and departments?
* Display calculated values?

The answer is the **`SELECT`** statement.

---

# Why Do We Need SELECT?

The `SELECT` statement is used to:

* Display stored data.
* Generate reports.
* Search information.
* Perform calculations.
* Analyze data.
* Retrieve data for applications.

Without `SELECT`, data stored in the database cannot be viewed.

---

# What is SELECT?

The **`SELECT`** statement is used to retrieve data from one or more tables.

It does not modify the data; it only reads and displays the requested information.

---

# Syntax

## Retrieve All Columns

```sql
SELECT *
FROM table_name;
```

---

## Retrieve Specific Columns

```sql
SELECT column1, column2
FROM table_name;
```

---

# Example 1 – Display All Records

```sql
SELECT *
FROM Student;
```

### Output

| StudentID | Name  | Age | Department | Email                                         |
| --------- | ----- | --- | ---------- | --------------------------------------------- |
| 101       | Rahul | 20  | CSE        | [rahul@example.com](mailto:rahul@example.com) |
| 102       | Priya | 19  | AI         | [priya@example.com](mailto:priya@example.com) |
| 103       | Arun  | 21  | ECE        | [arun@example.com](mailto:arun@example.com)   |
| 104       | Sneha | 20  | IT         | [sneha@example.com](mailto:sneha@example.com) |

---

# Example 2 – Display Specific Columns

```sql
SELECT StudentID, Name
FROM Student;
```

### Output

| StudentID | Name  |
| --------- | ----- |
| 101       | Rahul |
| 102       | Priya |
| 103       | Arun  |
| 104       | Sneha |

---

# Example 3 – Display Three Columns

```sql
SELECT Name, Department, Age
FROM Student;
```

### Output

| Name  | Department | Age |
| ----- | ---------- | --: |
| Rahul | CSE        |  20 |
| Priya | AI         |  19 |
| Arun  | ECE        |  21 |
| Sneha | IT         |  20 |

---

# Example 4 – Using Column Aliases

Aliases change the column heading in the result without changing the table structure.

```sql
SELECT
    StudentID AS ID,
    Name AS Student_Name,
    Department AS Branch
FROM Student;
```

### Output

| ID  | Student_Name | Branch |
| --- | ------------ | ------ |
| 101 | Rahul        | CSE    |
| 102 | Priya        | AI     |
| 103 | Arun         | ECE    |
| 104 | Sneha        | IT     |

---

# Example 5 – Display Constant Values

```sql
SELECT 'Welcome to SQL';
```

### Output

| Welcome to SQL |
| -------------- |
| Welcome to SQL |

---

# Example 6 – Perform Calculations

```sql
SELECT 50 + 25 AS Total;
```

### Output

| Total |
| ----: |
|    75 |

---

# Example 7 – Display Current Date

```sql
SELECT CURRENT_DATE;
```

### Sample Output

| CURRENT_DATE |
| ------------ |
| 2026-07-27   |

> The exact function and output format may vary slightly depending on the database system.

---

# Internal Working

```text
User
   │
   ▼
SELECT Statement
   │
   ▼
SQL Parser
   │
   ▼
Database Engine
   │
   ▼
Retrieve Required Data
   │
   ▼
Return Result Set
```

---

# SELECT vs SELECT *

| SELECT *                    | SELECT Column1, Column2         |
| --------------------------- | ------------------------------- |
| Retrieves all columns       | Retrieves selected columns only |
| May return unnecessary data | Returns only required data      |
| Slower for large tables     | More efficient                  |
| Common during learning      | Recommended in production       |

---

# Database Compatibility

| Feature        | MySQL | PostgreSQL | SQL Server | SQLite |
| -------------- | :---: | :--------: | :--------: | :----: |
| `SELECT *`     |   ✅   |      ✅     |      ✅     |    ✅   |
| Column Aliases |   ✅   |      ✅     |      ✅     |    ✅   |
| Calculations   |   ✅   |      ✅     |      ✅     |    ✅   |
| `CURRENT_DATE` |   ✅   |      ✅     |     ✅*     |    ✅   |

> *SQL Server commonly uses `CAST(GETDATE() AS DATE)` to return only the current date.

---

# Real-World Applications

| Application | Example                   |
| ----------- | ------------------------- |
| Banking     | View account details      |
| Hospital    | Display patient records   |
| School      | Show student marks        |
| E-Commerce  | Display products          |
| HR System   | View employee information |
| Library     | Display issued books      |

---

# Advantages

* Retrieves data quickly.
* Can display one or multiple columns.
* Supports calculations and expressions.
* Works with one or many tables.
* Forms the foundation for advanced SQL queries.

---

# Common Mistakes

* Using `SELECT *` unnecessarily.
* Misspelling column names.
* Forgetting commas between selected columns.
* Assuming aliases permanently rename columns.
* Ignoring the order of columns in the output.

---

# Best Practices

* Select only the required columns.
* Use meaningful aliases for reports.
* Format queries with one column per line for readability.
* Avoid `SELECT *` in production applications.
* Use uppercase SQL keywords.

---

# Interview Questions

### 1. What is the purpose of the `SELECT` statement?

**Answer:** It retrieves data from one or more database tables.

---

### 2. What does the asterisk (`*`) mean in `SELECT *`?

**Answer:** It retrieves **all columns** from the specified table.

---

### 3. How do you retrieve only the `Name` and `Department` columns?

**Answer:**

```sql
SELECT Name, Department
FROM Student;
```

---

### 4. What is a column alias?

**Answer:** A temporary name given to a column in the query result using the `AS` keyword.

---

### 5. Why should `SELECT *` be avoided in large applications?

**Answer:** It retrieves unnecessary columns, increases data transfer, and may reduce query performance.

---

# Practice Questions

## Easy

1. What is the purpose of `SELECT`?
2. Write a query to display all columns.
3. Write a query to display only the `Name` column.
4. What is a column alias?
5. What does `SELECT *` return?

---

## Medium

1. Retrieve the `StudentID`, `Name`, and `Department` columns.
2. Use aliases for three columns.
3. Explain the difference between `SELECT *` and selecting specific columns.
4. Display a constant string using `SELECT`.
5. Perform a simple arithmetic calculation using `SELECT`.

---

## Hard

1. Explain the internal working of a `SELECT` query.
2. Compare `SELECT *` with selecting specific columns from a performance perspective.
3. Describe how the database processes a `SELECT` statement.
4. Explain why `SELECT` is classified as a DQL command.
5. Discuss best practices for writing efficient `SELECT` queries.

---

# Key Takeaways

* `SELECT` is used to retrieve data from database tables.
* `SELECT *` retrieves all columns, while specific column selection retrieves only the required data.
* Aliases improve the readability of query results.
* `SELECT` can also display constants and perform calculations.
* Selecting only the necessary columns improves performance and follows industry best practices.

---

# Conclusion

The `SELECT` statement is the foundation of SQL because almost every database application needs to retrieve information. Mastering `SELECT` is essential before learning advanced concepts such as filtering, sorting, grouping, joins, and subqueries. In the next chapter, you will learn how to **modify existing records** using the **`UPDATE`** statement.
