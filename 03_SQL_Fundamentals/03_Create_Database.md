# Create Database

# Introduction

A **database** is the foundation of every SQL application. Before creating tables, inserting records, or writing SQL queries, you must first create a database.

A database acts as a container that stores related tables, views, indexes, procedures, and other database objects.

In this chapter, you will learn how to create a database, view existing databases, select a database for use, and safely delete a database.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand what a database is.
* Create a new database.
* View available databases.
* Select a database for use.
* Delete a database.
* Create a database only if it does not already exist.
* Understand database naming conventions.

---

# Problem Statement

Suppose you are developing a **Student Management System**.

You need to store:

* Student information
* Faculty details
* Department records
* Course information
* Examination results

Where should all these tables be stored?

The answer is **inside a database**.

Before creating any table, you must first create a database.

---

# Why Do We Need a Database?

A database helps us:

* Organize related information.
* Store large amounts of data.
* Manage multiple tables.
* Reduce data redundancy.
* Improve security.
* Retrieve data efficiently.

Without a database, tables cannot be created or managed properly.

---

# What is a Database?

A **Database** is an organized collection of related data that is stored electronically and managed by a Database Management System (DBMS).

Think of a database as a **folder**, and the tables inside it as **files**.

```text
CollegeDB
│
├── Student
├── Department
├── Faculty
├── Course
└── Marks
```

---

# Syntax

## Create a Database

```sql
CREATE DATABASE database_name;
```

### Example

```sql
CREATE DATABASE CollegeDB;
```

---

# Create Database Only If It Doesn't Exist

Some database systems allow you to avoid errors if the database already exists.

```sql
CREATE DATABASE IF NOT EXISTS CollegeDB;
```

> **Note:** `IF NOT EXISTS` is supported in MySQL and some other database systems. It is not available in all SQL databases.

---

# View Existing Databases

## MySQL

```sql
SHOW DATABASES;
```

---

## PostgreSQL

```sql
SELECT datname
FROM pg_database;
```

---

## SQL Server

```sql
SELECT name
FROM sys.databases;
```

---

## SQLite

SQLite creates the database automatically when you create or open a database file.

---

# Select a Database

Before creating tables, select the database.

## MySQL

```sql
USE CollegeDB;
```

---

## SQL Server

```sql
USE CollegeDB;
GO
```

---

## PostgreSQL

Connect to the required database using your SQL client or terminal.

---

## SQLite

Open the required database file.

---

# Verify the Current Database

## MySQL

```sql
SELECT DATABASE();
```

### Output

| DATABASE() |
| ---------- |
| CollegeDB  |

---

# Delete a Database

```sql
DROP DATABASE CollegeDB;
```

> **Warning:** This command permanently deletes the database and all the objects stored inside it.

---

# Complete Example

## Step 1: Create the Database

```sql
CREATE DATABASE CollegeDB;
```

---

## Step 2: Verify the Database

```sql
SHOW DATABASES;
```

### Sample Output

| Database           |
| ------------------ |
| CollegeDB          |
| mysql              |
| information_schema |
| performance_schema |

---

## Step 3: Select the Database

```sql
USE CollegeDB;
```

---

## Step 4: Verify the Selected Database

```sql
SELECT DATABASE();
```

### Output

| DATABASE() |
| ---------- |
| CollegeDB  |

---

# Internal Working

```text
User
   │
   ▼
CREATE DATABASE CollegeDB
   │
   ▼
DBMS Checks
(Database Name & Permissions)
   │
   ▼
Database Created
   │
   ▼
Ready to Store Tables
```

---

# Database Naming Rules

Follow these naming rules while creating databases:

| Rule                                 | Example      |
| ------------------------------------ | ------------ |
| Use meaningful names                 | CollegeDB    |
| Avoid spaces                         | StudentDB ✔  |
| Avoid special characters             | EmployeeDB ✔ |
| Use letters, numbers and underscores | School_DB ✔  |
| Keep names simple                    | InventoryDB  |

---

# Database Naming Examples

| Good Names  | Poor Names        |
| ----------- | ----------------- |
| CollegeDB   | db1               |
| LibraryDB   | Test              |
| HospitalDB  | New Database      |
| InventoryDB | My Database       |
| EmployeeDB  | Database123456789 |

---

# Database Compatibility

| Feature         | MySQL | PostgreSQL | SQL Server |    SQLite    |
| --------------- | :---: | :--------: | :--------: | :----------: |
| CREATE DATABASE |   ✅   |      ✅     |      ✅     |  File-based  |
| IF NOT EXISTS   |   ✅   |      ❌     |      ❌     | Not Required |
| USE Database    |   ✅   |      ❌     |      ✅     |  File-based  |
| SHOW DATABASES  |   ✅   |      ❌     |      ❌     |       ❌      |

---

# Advantages

* Organizes related data.
* Supports multiple tables.
* Improves data management.
* Enables data security.
* Makes backup and recovery easier.
* Supports multi-user applications.

---

# Common Mistakes

* Forgetting to select the database before creating tables.
* Using invalid database names.
* Accidentally executing `DROP DATABASE`.
* Assuming every DBMS supports identical SQL syntax.
* Creating unnecessary databases for small projects.

---

# Best Practices

* Use meaningful database names.
* Follow a consistent naming convention.
* Create one database for each application.
* Verify the current database before creating tables.
* Back up important databases regularly.
* Avoid deleting databases without confirmation.

---

# Interview Questions

### 1. What is a database?

**Answer:** A database is an organized collection of related data managed by a Database Management System (DBMS).

---

### 2. Which SQL command creates a database?

**Answer:**

```sql
CREATE DATABASE CollegeDB;
```

---

### 3. Which command selects a database in MySQL?

**Answer:**

```sql
USE CollegeDB;
```

---

### 4. Which command permanently deletes a database?

**Answer:**

```sql
DROP DATABASE CollegeDB;
```

---

### 5. Why should a database be created before creating tables?

**Answer:** Because tables are stored inside a database. Without a database, there is no container to hold tables and other database objects.

---

# Practice Questions

## Easy

1. What is a database?
2. Write the syntax to create a database.
3. Which command displays all databases in MySQL?
4. Which command selects a database?
5. Which command deletes a database?

---

## Medium

1. Explain the process of creating a database.
2. Compare database creation in MySQL and SQLite.
3. Explain the purpose of the `USE` command.
4. What are the best practices for naming databases?
5. Why is `DROP DATABASE` considered a dangerous command?

---

## Hard

1. Compare database creation in MySQL, PostgreSQL, SQL Server, and SQLite.
2. Explain the internal working of the `CREATE DATABASE` command.
3. Design a database structure for an Online Shopping System.
4. Explain why different database systems use different commands to select a database.
5. Discuss database management best practices used in enterprise applications.

---

# Key Takeaways

* A database is a container that stores related tables and database objects.
* Use `CREATE DATABASE` to create a new database.
* Select the database before creating tables.
* Use `SHOW DATABASES` (MySQL) to view existing databases.
* Use `DROP DATABASE` carefully because it permanently removes the database and its contents.
* Different database systems provide slightly different commands for managing databases.

---

# Conclusion

Creating a database is the first practical step in building any SQL application. Once a database has been created and selected, you are ready to create tables, define columns, and start storing real-world data. In the next chapter, you will learn how to **create tables** and define the structure of your data.
