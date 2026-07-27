# Create Table

# Introduction

After creating a database, the next step is to create **tables**.

A table is one of the most important objects in a relational database. It stores data in a structured format using **rows** and **columns**.

Every real-world application—such as banking systems, e-commerce websites, hospitals, schools, and social media platforms—stores its information inside database tables.

In this chapter, you will learn how to create tables, define columns, choose appropriate data types, and follow best practices for designing tables.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand what a table is.
* Create a table using SQL.
* Define columns and data types.
* Understand rows and columns.
* Follow table naming conventions.
* Create multiple tables.
* Verify that a table has been created successfully.

---

# Problem Statement

Suppose you are developing a **Student Management System**.

You need to store:

* Student ID
* Student Name
* Age
* Department
* Email

Where should this information be stored?

The answer is **inside a table**.

Before inserting any data, you must first create the table.

---

# Why Do We Need Tables?

Tables help us to:

* Organize related data.
* Store thousands or millions of records.
* Retrieve data quickly.
* Maintain relationships between data.
* Reduce duplication.
* Improve data consistency.

Without tables, a database cannot store meaningful information.

---

# What is a Table?

A **Table** is a database object that stores related data in the form of **rows** and **columns**.

* **Column** → Represents an attribute.
* **Row** → Represents a single record.

Example:

| StudentID | Name  | Age | Department |
| --------- | ----- | --- | ---------- |
| 101       | Rahul | 20  | CSE        |
| 102       | Priya | 19  | AI         |
| 103       | Arun  | 21  | ECE        |

---

# Components of a Table

| Component   | Description                                |
| ----------- | ------------------------------------------ |
| Table Name  | Name of the table                          |
| Columns     | Individual fields that store data          |
| Rows        | Individual records                         |
| Data Types  | Define the type of data each column stores |
| Constraints | Rules applied to columns                   |

---

# Syntax

```sql
CREATE TABLE table_name (
    column1 data_type,
    column2 data_type,
    column3 data_type
);
```

---

# Example 1 – Create Student Table

```sql
CREATE TABLE Student (
    StudentID INT,
    Name VARCHAR(100),
    Age INT,
    Department VARCHAR(50),
    Email VARCHAR(100)
);
```

---

# Example 2 – Create Department Table

```sql
CREATE TABLE Department (
    DepartmentID INT,
    DepartmentName VARCHAR(100)
);
```

---

# Example 3 – Create Employee Table

```sql
CREATE TABLE Employee (
    EmployeeID INT,
    EmployeeName VARCHAR(100),
    Salary DECIMAL(10,2),
    JoiningDate DATE
);
```

---

# Understanding the Example

For the Student table:

| Column     | Data Type    | Purpose              |
| ---------- | ------------ | -------------------- |
| StudentID  | INT          | Stores student ID    |
| Name       | VARCHAR(100) | Stores student name  |
| Age        | INT          | Stores age           |
| Department | VARCHAR(50)  | Stores department    |
| Email      | VARCHAR(100) | Stores email address |

---

# Visual Representation

```text
Student
──────────────────────────────────
StudentID
Name
Age
Department
Email
──────────────────────────────────
```

---

# Table Structure

After executing the `CREATE TABLE` statement, the structure will be:

| Column Name | Data Type    |
| ----------- | ------------ |
| StudentID   | INT          |
| Name        | VARCHAR(100) |
| Age         | INT          |
| Department  | VARCHAR(50)  |
| Email       | VARCHAR(100) |

---

# View Tables

## MySQL

```sql
SHOW TABLES;
```

---

## PostgreSQL

```sql
\dt
```

---

## SQL Server

```sql
SELECT TABLE_NAME
FROM INFORMATION_SCHEMA.TABLES
WHERE TABLE_TYPE = 'BASE TABLE';
```

---

## SQLite

```sql
.tables
```

---

# View Table Structure

## MySQL

```sql
DESCRIBE Student;
```

---

## PostgreSQL

```sql
\d Student
```

---

## SQL Server

```sql
EXEC sp_help Student;
```

---

## SQLite

```sql
PRAGMA table_info(Student);
```

---

# Internal Working

```text
User
   │
   ▼
CREATE TABLE
   │
   ▼
DBMS Checks
(Column Names)
(Data Types)
(Syntax)
   │
   ▼
Creates Table Metadata
   │
   ▼
Empty Table Ready
```

---

# Table Naming Rules

| Good Practice                             | Example                      |
| ----------------------------------------- | ---------------------------- |
| Use meaningful names                      | Student                      |
| Use singular nouns                        | Employee                     |
| Avoid spaces                              | StudentDetails               |
| Use PascalCase or snake_case consistently | StudentMarks / student_marks |
| Keep names descriptive                    | CourseRegistration           |

---

# Good vs Poor Table Names

| Good Names | Poor Names |
| ---------- | ---------- |
| Student    | Table1     |
| Employee   | Test       |
| Department | Data       |
| Course     | ABC        |
| Attendance | Temp       |

---

# Database Compatibility

| Feature             | MySQL | PostgreSQL | SQL Server | SQLite |
| ------------------- | :---: | :--------: | :--------: | :----: |
| CREATE TABLE        |   ✅   |      ✅     |      ✅     |    ✅   |
| SHOW TABLES         |   ✅   |      ❌     |      ❌     |    ❌   |
| DESCRIBE Table      |   ✅   |      ❌     |      ❌     |    ❌   |
| Standard SQL Syntax |   ✅   |      ✅     |      ✅     |    ✅   |

---

# Advantages

* Organizes data efficiently.
* Supports structured storage.
* Enables fast data retrieval.
* Simplifies data management.
* Supports relationships through keys.
* Provides data consistency.

---

# Common Mistakes

* Choosing incorrect data types.
* Using unclear table names.
* Forgetting to select the database before creating a table.
* Creating duplicate tables.
* Ignoring naming conventions.

---

# Best Practices

* Use meaningful table names.
* Select appropriate data types.
* Keep table names consistent.
* Design tables based on real-world entities.
* Avoid storing multiple values in a single column.
* Add constraints such as `PRIMARY KEY` and `NOT NULL` where appropriate.

---

# Interview Questions

### 1. What is a table in SQL?

**Answer:** A table is a database object that stores related data in rows and columns.

---

### 2. Which SQL command is used to create a table?

**Answer:**

```sql
CREATE TABLE Student (
    StudentID INT,
    Name VARCHAR(100)
);
```

---

### 3. What is the difference between a row and a column?

**Answer:**

| Row                   | Column                        |
| --------------------- | ----------------------------- |
| Represents one record | Represents one attribute      |
| Horizontal            | Vertical                      |
| Contains values       | Defines data type and purpose |

---

### 4. Can a table exist without a database?

**Answer:** No. Every table belongs to a database.

---

### 5. Why are data types required while creating a table?

**Answer:** Data types define the kind of values each column can store, ensuring data accuracy and efficient storage.

---

# Practice Questions

## Easy

1. What is a table?
2. Write the syntax to create a table.
3. What is the difference between a row and a column?
4. Which command creates a table?
5. Name three commonly used data types.

---

## Medium

1. Explain the structure of a table.
2. Create a table for an Employee Management System.
3. Explain the importance of data types.
4. Compare a database and a table.
5. What are the best practices for naming tables?

---

## Hard

1. Design a table for an Online Shopping System.
2. Explain how the DBMS processes a `CREATE TABLE` statement internally.
3. Compare table creation across MySQL, PostgreSQL, SQL Server, and SQLite.
4. Discuss the importance of proper table design in database normalization.
5. Design tables for a Library Management System with appropriate columns.

---

# Key Takeaways

* A table stores related data in rows and columns.
* Use the `CREATE TABLE` statement to create a new table.
* Columns define the structure, while rows store the actual data.
* Selecting appropriate data types is essential for efficient storage and validation.
* Well-designed tables are the foundation of a reliable relational database.

---

# Conclusion

Creating tables is one of the most important skills in SQL because every piece of data is stored inside a table. A well-designed table improves data organization, consistency, and performance. In the next chapter, you will learn how to **insert data into tables** using the `INSERT INTO` statement.
