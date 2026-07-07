# Create Your First Database

# Introduction

Now that your SQL development environment is ready, it's time to create your **first database**.

A database is a collection of related tables used to store and organize data. Before creating tables, inserting records, or writing SQL queries, you must first create a database.

In this chapter, you will learn how to create, view, use, and delete a database.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand what a database is.
* Create a database using SQL.
* View existing databases.
* Select a database for use.
* Delete a database.
* Verify that a database has been created successfully.

---

# Problem Statement

Suppose you want to build a **Student Management System**.

Before creating tables such as:

* Student
* Course
* Faculty
* Department

you first need a database to store them.

Let's create a database named **CollegeDB**.

---

# Why Do We Need a Database?

A database helps you:

* Organize related information.
* Store data permanently.
* Manage multiple tables.
* Improve data security.
* Retrieve information efficiently.

Without a database, tables cannot be created.

---

# What is a Database?

A **Database** is an organized collection of related data stored electronically.

Example:

```text
CollegeDB
│
├── Student
├── Course
├── Faculty
├── Department
└── Marks
```

---

# SQL Syntax

## Create a Database

```sql
CREATE DATABASE CollegeDB;
```

---

## View Available Databases

### MySQL

```sql
SHOW DATABASES;
```

### PostgreSQL

```sql
SELECT datname
FROM pg_database;
```

### SQL Server

```sql
SELECT name
FROM sys.databases;
```

### SQLite

SQLite creates a database automatically when you create or open a database file.

---

## Select a Database

### MySQL

```sql
USE CollegeDB;
```

### PostgreSQL

Connect to the database using your SQL client.

### SQL Server

```sql
USE CollegeDB;
GO
```

### SQLite

Open the database file using your SQLite tool.

---

## Delete a Database

```sql
DROP DATABASE CollegeDB;
```

> **Warning:** `DROP DATABASE` permanently deletes the database and all its data.

---

# Example

## Step 1: Create the Database

```sql
CREATE DATABASE CollegeDB;
```

---

## Step 2: Select the Database

```sql
USE CollegeDB;
```

---

## Step 3: Verify the Current Database

### MySQL

```sql
SELECT DATABASE();
```

### Expected Output

| DATABASE() |
| ---------- |
| CollegeDB  |

---

# Execution Flow

```text
Start
   │
   ▼
Create Database
   │
   ▼
Database Created
   │
   ▼
Select Database
   │
   ▼
Ready to Create Tables
```

---

# Database Structure

```text
CollegeDB
│
├── Student
├── Department
├── Course
├── Faculty
└── Marks
```

---

# Common Commands

| Command             | Purpose                              |
| ------------------- | ------------------------------------ |
| `CREATE DATABASE`   | Creates a new database               |
| `SHOW DATABASES`    | Displays available databases (MySQL) |
| `USE`               | Selects a database                   |
| `SELECT DATABASE()` | Shows the current database (MySQL)   |
| `DROP DATABASE`     | Deletes a database                   |

---

# Database Compatibility

| Database System | `CREATE DATABASE` | `USE` | Notes                         |
| --------------- | ----------------- | ----- | ----------------------------- |
| MySQL           | ✅                 | ✅     | Fully supported               |
| PostgreSQL      | ✅                 | ❌     | Connect using the client      |
| SQL Server      | ✅                 | ✅     | Uses `GO` after `USE`         |
| SQLite          | File-based        | ❌     | Database is created as a file |

---

# Common Mistakes

* Forgetting to select the database before creating tables.
* Creating a database with an incorrect name.
* Accidentally deleting a database using `DROP DATABASE`.
* Assuming every database uses the `USE` command.

---

# Best Practices

* Use meaningful database names.
* Follow a consistent naming convention.
* Create one database for each project.
* Verify the selected database before creating tables.
* Avoid deleting databases unless necessary.

---

# Interview Questions

### 1. What is a database?

**Answer:** A database is an organized collection of related data stored electronically.

---

### 2. Which SQL command creates a database?

**Answer:**

```sql
CREATE DATABASE DatabaseName;
```

---

### 3. Which command selects a database in MySQL?

**Answer:**

```sql
USE DatabaseName;
```

---

### 4. Which command deletes a database?

**Answer:**

```sql
DROP DATABASE DatabaseName;
```

---

### 5. Does SQLite use the `CREATE DATABASE` command?

**Answer:** No. SQLite creates a database automatically as a file.

---

# Practice Questions

## Easy

1. What is a database?
2. Write the syntax to create a database.
3. Which command selects a database in MySQL?
4. How do you delete a database?
5. What is the purpose of a database?

---

## Medium

1. Explain the process of creating a database.
2. Compare database creation in MySQL and SQLite.
3. What happens if you try to create a database that already exists?
4. Why should you verify the selected database?
5. Explain the purpose of the `USE` command.

---

## Hard

1. Compare database creation in MySQL, PostgreSQL, SQL Server, and SQLite.
2. Explain why databases are required before creating tables.
3. Design a database structure for a Library Management System.
4. Explain the risks of using `DROP DATABASE`.
5. Discuss database naming conventions used in real-world applications.

---

# Key Takeaways

* A database stores related tables and data.
* Use `CREATE DATABASE` to create a new database.
* Select the database before creating tables.
* Different database systems have different methods for selecting a database.
* `DROP DATABASE` permanently removes the database and all its contents.

---

# Conclusion

Creating a database is the first practical step in SQL development. Once your database is ready, you can create tables, insert records, and start writing SQL queries. In the next chapter, you will create your **first table** and begin working with real data.
