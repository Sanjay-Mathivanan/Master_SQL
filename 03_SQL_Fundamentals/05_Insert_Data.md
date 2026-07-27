# Insert Data

# Introduction

Creating a table only defines its structure—it does not store any information. To make a table useful, you need to insert records into it.

The **`INSERT INTO`** statement is used to add one or more rows of data to a table. Every SQL application, from banking systems to e-commerce platforms, uses the `INSERT` statement to store new information.

In this chapter, you will learn how to insert single and multiple records, use different insertion techniques, and follow best practices for adding data.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand the purpose of the `INSERT INTO` statement.
* Insert a single row into a table.
* Insert multiple rows in one query.
* Insert values into selected columns.
* Understand how SQL validates inserted data.
* Avoid common insertion errors.

---

# Problem Statement

Suppose you have created the following **Student** table.

```sql
CREATE TABLE Student (
    StudentID INT,
    Name VARCHAR(100),
    Age INT,
    Department VARCHAR(50),
    Email VARCHAR(100)
);
```

The table exists, but it contains **no data**.

How do you add student records?

The answer is the **`INSERT INTO`** statement.

---

# Why Do We Need INSERT?

The `INSERT` statement allows us to:

* Store new records.
* Register new users.
* Add products.
* Save customer information.
* Store employee details.
* Build datasets for analysis.

Without `INSERT`, a database would contain only empty tables.

---

# What is INSERT INTO?

The **`INSERT INTO`** statement is used to add new rows of data into a table.

Each execution of an `INSERT` statement creates one or more new records.

---

# Syntax

## Insert All Columns

```sql
INSERT INTO table_name
VALUES (value1, value2, value3, ...);
```

---

## Insert Specific Columns

```sql
INSERT INTO table_name (
    column1,
    column2,
    column3
)
VALUES (
    value1,
    value2,
    value3
);
```

---

# Example 1 – Insert a Single Record

```sql
INSERT INTO Student
VALUES (
    101,
    'Rahul',
    20,
    'CSE',
    'rahul@example.com'
);
```

---

# Table After Insertion

| StudentID | Name  | Age | Department | Email                                         |
| --------- | ----- | --- | ---------- | --------------------------------------------- |
| 101       | Rahul | 20  | CSE        | [rahul@example.com](mailto:rahul@example.com) |

---

# Example 2 – Insert Multiple Records

```sql
INSERT INTO Student
VALUES
(102, 'Priya', 19, 'AI', 'priya@example.com'),
(103, 'Arun', 21, 'ECE', 'arun@example.com'),
(104, 'Sneha', 20, 'IT', 'sneha@example.com');
```

---

# Table After Multiple Inserts

| StudentID | Name  | Age | Department | Email                                         |
| --------- | ----- | --- | ---------- | --------------------------------------------- |
| 101       | Rahul | 20  | CSE        | [rahul@example.com](mailto:rahul@example.com) |
| 102       | Priya | 19  | AI         | [priya@example.com](mailto:priya@example.com) |
| 103       | Arun  | 21  | ECE        | [arun@example.com](mailto:arun@example.com)   |
| 104       | Sneha | 20  | IT         | [sneha@example.com](mailto:sneha@example.com) |

---

# Example 3 – Insert Into Selected Columns

```sql
INSERT INTO Student (
    StudentID,
    Name,
    Department
)
VALUES (
    105,
    'Kiran',
    'AI'
);
```

If the remaining columns allow `NULL` values or have default values, the insertion succeeds.

---

# Result

| StudentID | Name  | Age  | Department | Email |
| --------- | ----- | ---- | ---------- | ----- |
| 105       | Kiran | NULL | AI         | NULL  |

---

# Example 4 – Insert a New Department

```sql
INSERT INTO Department
VALUES (
    10,
    'Artificial Intelligence'
);
```

---

# Internal Working

```text
User
   │
   ▼
INSERT INTO Statement
   │
   ▼
DBMS Validates
(Column Count)
(Data Types)
(Constraints)
   │
   ▼
Stores Data
   │
   ▼
Record Added Successfully
```

---

# Rules for INSERT

* Values must follow the same order as the columns when column names are omitted.
* The number of values must match the number of columns.
* Data types must be compatible.
* String values should be enclosed in single quotes.
* Numeric values should not be enclosed in quotes.
* Date values should follow the database's supported date format.

---

# Common Data Types During INSERT

| Data Type | Example      |
| --------- | ------------ |
| INT       | 101          |
| VARCHAR   | 'Rahul'      |
| CHAR      | 'A'          |
| DECIMAL   | 45000.75     |
| DATE      | '2026-07-27' |
| BOOLEAN   | TRUE         |

---

# Common Errors

## Incorrect Number of Values

```sql
INSERT INTO Student
VALUES (101, 'Rahul');
```

❌ Error: The number of values does not match the number of columns.

---

## Incorrect Data Type

```sql
INSERT INTO Student
VALUES (
    'ABC',
    'Rahul',
    20,
    'CSE',
    'rahul@example.com'
);
```

❌ Error: `StudentID` expects an integer.

---

## Wrong Column Order

```sql
INSERT INTO Student
VALUES (
    'Rahul',
    101,
    20,
    'CSE',
    'rahul@example.com'
);
```

❌ The values are placed in the wrong columns.

---

# Best Practice

Always specify the column names.

```sql
INSERT INTO Student (
    StudentID,
    Name,
    Age,
    Department,
    Email
)
VALUES (
    106,
    'Anitha',
    20,
    'CSE',
    'anitha@example.com'
);
```

This improves readability and prevents errors if the table structure changes.

---

# Database Compatibility

| Feature             | MySQL | PostgreSQL | SQL Server | SQLite |
| ------------------- | :---: | :--------: | :--------: | :----: |
| INSERT INTO         |   ✅   |      ✅     |      ✅     |    ✅   |
| Multiple Row Insert |   ✅   |      ✅     |      ✅     |    ✅   |
| Column List         |   ✅   |      ✅     |      ✅     |    ✅   |
| NULL Values         |   ✅   |      ✅     |      ✅     |    ✅   |

---

# Real-World Applications

| Application | Example               |
| ----------- | --------------------- |
| Banking     | Add a new customer    |
| Hospital    | Register a patient    |
| School      | Add a student         |
| E-Commerce  | Add a new product     |
| HR System   | Add an employee       |
| Library     | Register a new member |

---

# Advantages

* Adds new records quickly.
* Supports inserting one or many rows.
* Works with all major relational databases.
* Supports inserting values into selected columns.
* Easy to understand and use.

---

# Common Mistakes

* Forgetting to specify column names.
* Using an incorrect number of values.
* Inserting incompatible data types.
* Omitting quotes for string values.
* Using double quotes instead of single quotes for string literals (database-specific behaviour may vary).

---

# Best Practices

* Always specify column names.
* Verify data before inserting.
* Use meaningful and valid values.
* Follow consistent formatting.
* Validate data types before execution.

---

# Interview Questions

### 1. What is the purpose of the `INSERT INTO` statement?

**Answer:** It is used to add one or more new records to a table.

---

### 2. Can multiple rows be inserted using a single `INSERT` statement?

**Answer:** Yes.

```sql
INSERT INTO Student
VALUES
(101, 'Rahul', 20, 'CSE', 'rahul@example.com'),
(102, 'Priya', 19, 'AI', 'priya@example.com');
```

---

### 3. Why is specifying column names recommended?

**Answer:** It improves readability, prevents errors, and makes the query independent of the table's column order.

---

### 4. What happens if the number of values does not match the number of columns?

**Answer:** The database returns an error and the record is not inserted.

---

### 5. Can `NULL` values be inserted?

**Answer:** Yes, provided the column allows `NULL` values or has a default value.

---

# Practice Questions

## Easy

1. What is the purpose of `INSERT INTO`?
2. Write the syntax for inserting one row.
3. Can multiple rows be inserted in one statement?
4. Why are column names recommended?
5. What happens if data types do not match?

---

## Medium

1. Insert three student records into a `Student` table.
2. Insert data into selected columns only.
3. Explain how SQL validates inserted data.
4. Compare single-row and multiple-row insertion.
5. Explain the advantages of specifying column names.

---

## Hard

1. Design `INSERT` statements for a Library Management System.
2. Explain the internal working of the `INSERT` statement.
3. Compare `INSERT` behaviour across MySQL, PostgreSQL, SQL Server, and SQLite.
4. Explain common insertion failures and how to resolve them.
5. Discuss best practices for inserting large volumes of data efficiently.

---

# Key Takeaways

* `INSERT INTO` is used to add new records to a table.
* Records can be inserted one at a time or multiple at once.
* Specifying column names is a recommended best practice.
* The number of values must match the selected columns.
* SQL validates data types and constraints before storing records.

---

# Conclusion

The `INSERT INTO` statement is one of the most frequently used SQL commands because every database application needs to store new information. Understanding how to insert data correctly is essential before learning how to retrieve, update, and delete records. In the next chapter, you will learn how to **retrieve data** from a table using the **`SELECT`** statement.
