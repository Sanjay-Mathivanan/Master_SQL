# SQL Fundamentals - Practice Exercises

# Introduction

Congratulations! You have completed the **SQL Fundamentals** module.

You have learned:

* SQL Introduction
* SQL Commands
* Database Creation
* Table Creation
* CRUD Operations
* Constraints
* SQL Comments
* Data Types
* Common Beginner Mistakes

Now it's time to test your understanding by solving practical SQL exercises.

These exercises are divided into multiple difficulty levels, similar to coding platforms and technical interviews.

---

# Learning Objectives

After completing these exercises, you will be able to:

* Apply SQL concepts in practical scenarios.
* Improve problem-solving skills.
* Write efficient SQL queries.
* Strengthen interview preparation.
* Build confidence for real-world database development.

---

# Prerequisites

Before starting these exercises, ensure you understand:

* CREATE DATABASE
* CREATE TABLE
* INSERT
* SELECT
* UPDATE
* DELETE
* ALTER TABLE
* Constraints
* SQL Data Types
* SQL Comments

---

# Sample Database

Use the following database for practice.

## Employee Table

```sql
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY AUTO_INCREMENT,
    EmployeeName VARCHAR(100) NOT NULL,
    Department VARCHAR(50),
    Salary DECIMAL(10,2),
    Email VARCHAR(100) UNIQUE,
    JoiningDate DATE,
    Status VARCHAR(20) DEFAULT 'Active'
);
```

---

## Sample Data

```sql
INSERT INTO Employee
(EmployeeName, Department, Salary, Email, JoiningDate)

VALUES
('Rahul','IT',65000,'rahul@example.com','2024-01-10'),
('Priya','HR',50000,'priya@example.com','2023-06-15'),
('Arun','Finance',72000,'arun@example.com','2022-09-18'),
('Sneha','IT',60000,'sneha@example.com','2025-02-01'),
('Karthik','Marketing',45000,'karthik@example.com','2024-08-20');
```

---

# Employee Table

| EmployeeID | EmployeeName | Department |   Salary | JoiningDate | Status |
| ---------- | ------------ | ---------- | -------: | ----------- | ------ |
| 1          | Rahul        | IT         | 65000.00 | 2024-01-10  | Active |
| 2          | Priya        | HR         | 50000.00 | 2023-06-15  | Active |
| 3          | Arun         | Finance    | 72000.00 | 2022-09-18  | Active |
| 4          | Sneha        | IT         | 60000.00 | 2025-02-01  | Active |
| 5          | Karthik      | Marketing  | 45000.00 | 2024-08-20  | Active |

---

# Exercise Levels

| Level   | Difficulty | Purpose                 |
| ------- | ---------- | ----------------------- |
| Level 1 | Easy       | Learn SQL syntax        |
| Level 2 | Medium     | Apply multiple concepts |
| Level 3 | Hard       | Real-world scenarios    |
| Level 4 | Interview  | Placement preparation   |

---

# Level 1 - Easy Exercises

### Exercise 1

Create a database named **CompanyDB**.

---

### Exercise 2

Use the database.

---

### Exercise 3

Create an **Employee** table.

---

### Exercise 4

Insert five employee records.

---

### Exercise 5

Display all employees.

---

### Exercise 6

Display only employee names.

---

### Exercise 7

Display employee names and salaries.

---

### Exercise 8

Update Rahul's salary to **70000**.

---

### Exercise 9

Delete the employee whose ID is **5**.

---

### Exercise 10

Add a new employee.

---

### Exercise 11

Create a table with a PRIMARY KEY.

---

### Exercise 12

Create a table with a UNIQUE constraint.

---

### Exercise 13

Create a table with a DEFAULT constraint.

---

### Exercise 14

Create a table with a CHECK constraint.

---

### Exercise 15

Create a Department table.

---

# Level 2 - Medium Exercises

### Exercise 16

Add a new column named **PhoneNumber**.

---

### Exercise 17

Rename **EmployeeName** to **FullName**.

---

### Exercise 18

Change Salary data type to **DECIMAL(12,2)**.

---

### Exercise 19

Drop the **PhoneNumber** column.

---

### Exercise 20

Create Employee and Department tables using a FOREIGN KEY.

---

### Exercise 21

Insert records into both tables.

---

### Exercise 22

Try inserting an invalid DepartmentID.

Observe the error.

---

### Exercise 23

Insert an employee without specifying the Status.

Observe the DEFAULT value.

---

### Exercise 24

Insert a duplicate Email.

Observe the UNIQUE constraint.

---

### Exercise 25

Insert a negative Salary.

Observe the CHECK constraint.

---

### Exercise 26

Insert NULL into a NOT NULL column.

Observe the error.

---

### Exercise 27

Create a table using all constraints together.

---

### Exercise 28

Write a script using SQL comments.

---

### Exercise 29

Create a table using different SQL data types.

---

### Exercise 30

Identify five mistakes in an incorrect SQL script.

---

# Level 3 - Hard Exercises

### Exercise 31

Design a Student Management database.

Include:

* Students
* Courses
* Departments

---

### Exercise 32

Design a Library Management database.

---

### Exercise 33

Design a Hospital database.

---

### Exercise 34

Design an E-Commerce database.

---

### Exercise 35

Design a Banking database.

---

### Exercise 36

Create an Employee table using every major SQL constraint.

---

### Exercise 37

Write SQL scripts that intentionally violate each constraint and explain the resulting errors.

---

### Exercise 38

Convert an existing table into a well-designed production table.

---

### Exercise 39

Explain the purpose of every column and constraint in your schema.

---

### Exercise 40

Review a poorly designed database and suggest improvements.

---

# Level 4 - Interview Practice

### Question 1

Differentiate between:

* DELETE
* DROP
* TRUNCATE

---

### Question 2

Differentiate between:

* CHAR
* VARCHAR

---

### Question 3

Differentiate between:

* PRIMARY KEY
* UNIQUE KEY

---

### Question 4

Differentiate between:

* CHECK
* NOT NULL

---

### Question 5

Differentiate between:

* DEFAULT
* AUTO_INCREMENT

---

### Question 6

Explain the SQL command categories:

* DDL
* DML
* DQL
* DCL
* TCL

---

### Question 7

Why should every table have a PRIMARY KEY?

---

### Question 8

What happens when a FOREIGN KEY constraint is violated?

---

### Question 9

Why is DECIMAL preferred over FLOAT for financial applications?

---

### Question 10

Explain the purpose of SQL comments.

---

# Mini Projects

## Project 1

Employee Management System

Requirements:

* Employee table
* Department table
* Constraints
* Sample data

---

## Project 2

Student Management System

Requirements:

* Students
* Courses
* Enrollment

---

## Project 3

Hospital Management System

Requirements:

* Patients
* Doctors
* Appointments

---

## Project 4

Library Management System

Requirements:

* Books
* Members
* Borrow Records

---

## Project 5

Online Shopping Database

Requirements:

* Customers
* Products
* Orders

---

# SQL Coding Challenges

## Challenge 1

Write SQL to create a complete Employee database from scratch.

---

## Challenge 2

Create all tables using proper constraints.

---

## Challenge 3

Populate the database with sample data.

---

## Challenge 4

Modify the schema using ALTER TABLE.

---

## Challenge 5

Correct a script containing syntax errors.

---

## Challenge 6

Find and fix constraint violations.

---

## Challenge 7

Review a poorly designed table and redesign it.

---

## Challenge 8

Write a fully documented SQL script using comments.

---

## Challenge 9

Create an interview-ready SQL schema.

---

## Challenge 10

Explain your schema as if you were presenting it in a technical interview.

---

# Self-Assessment Checklist

Mark each item after completing it.

| Topic                       | Completed |
| --------------------------- | :-------: |
| SQL Introduction            |     ☐     |
| SQL Commands                |     ☐     |
| CREATE DATABASE             |     ☐     |
| CREATE TABLE                |     ☐     |
| INSERT                      |     ☐     |
| SELECT                      |     ☐     |
| UPDATE                      |     ☐     |
| DELETE                      |     ☐     |
| ALTER TABLE                 |     ☐     |
| RENAME TABLE                |     ☐     |
| RENAME COLUMN               |     ☐     |
| ADD / MODIFY / DROP Columns |     ☐     |
| DELETE vs DROP vs TRUNCATE  |     ☐     |
| NOT NULL                    |     ☐     |
| UNIQUE                      |     ☐     |
| PRIMARY KEY                 |     ☐     |
| FOREIGN KEY                 |     ☐     |
| CHECK                       |     ☐     |
| DEFAULT                     |     ☐     |
| AUTO_INCREMENT              |     ☐     |
| SQL Comments                |     ☐     |
| SQL Data Types              |     ☐     |
| Common Beginner Mistakes    |     ☐     |

---

# Internal Learning Workflow

```text
Read Concept
      │
      ▼
Study Syntax
      │
      ▼
Write SQL
      │
      ▼
Execute Query
      │
      ▼
Observe Output
      │
      ▼
Debug Errors
      │
      ▼
Practice Again
      │
      ▼
Master SQL Fundamentals
```

---

# Practice Strategy

| Week   | Goal                                           |
| ------ | ---------------------------------------------- |
| Week 1 | Complete Easy Exercises                        |
| Week 2 | Solve Medium Exercises                         |
| Week 3 | Finish Hard Exercises                          |
| Week 4 | Complete Interview Questions and Mini Projects |

---

# Common Mistakes During Practice

* Skipping syntax validation.
* Not reading error messages carefully.
* Forgetting the `WHERE` clause in `UPDATE` or `DELETE`.
* Ignoring constraints while inserting data.
* Using incorrect data types.
* Not testing scripts before making changes.

---

# Best Practices

* Practice SQL daily.
* Write queries manually instead of copying them.
* Test every query with sample data.
* Read database error messages carefully.
* Keep SQL scripts properly formatted.
* Comment complex SQL scripts.
* Use meaningful table and column names.
* Experiment with different constraints and data types.

---

# Key Takeaways

* Practice is the key to mastering SQL.
* Start with simple queries before moving to complex scenarios.
* Understand why a query works instead of memorising syntax.
* Learn from errors—they are valuable learning opportunities.
* Build complete database projects to strengthen practical skills.
* Consistent practice improves interview performance and real-world development skills.

---

# Conclusion

This chapter brings together everything covered in the **SQL Fundamentals** module through structured exercises, coding challenges, interview questions, and mini projects. Completing these exercises will strengthen your understanding of SQL syntax, database design, constraints, and data manipulation. Once you can confidently solve these problems, you will be well prepared to move on to advanced SQL topics such as joins, grouping, subqueries, views, indexes, transactions, and query optimisation.
