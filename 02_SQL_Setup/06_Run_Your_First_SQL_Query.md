# Run Your First SQL Query

# Introduction

Congratulations! 🎉

Your SQL development environment is now ready, and you have created your first database. The next step is to execute your **first SQL query**.

A SQL query is a command that allows you to communicate with the database. Using SQL queries, you can create tables, insert data, retrieve information, update records, and delete data.

In this chapter, you will learn how to execute your first SQL query and understand the basic workflow of interacting with a database.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand what a SQL query is.
* Execute your first SQL query.
* Understand the SQL query execution process.
* Interpret query results.
* Verify that your SQL environment is working correctly.

---

# Problem Statement

Suppose you have created a database named **CollegeDB**.

How do you check whether your SQL environment is working correctly?

The easiest way is to execute a simple SQL query.

---

# Why Do We Need SQL Queries?

SQL queries allow us to:

* Retrieve data from a database.
* Create database objects.
* Insert new records.
* Modify existing data.
* Delete unwanted data.
* Manage databases efficiently.

Without SQL queries, a database cannot be used effectively.

---

# What is a SQL Query?

A **SQL Query** is an instruction sent to a database to perform a specific operation.

Examples include:

* Creating a database
* Creating a table
* Retrieving data
* Updating records
* Deleting records

---

# Your First SQL Query

Execute the following query.

```sql
SELECT 'Hello, SQL!';
```

---

# Expected Output

| Hello, SQL! |
| ----------- |
| Hello, SQL! |

If you receive the above output, your SQL environment is working correctly.

---

# Another Simple Query

```sql
SELECT 100;
```

### Output

| 100 |
| --- |
| 100 |

---

# Mathematical Query

```sql
SELECT 25 + 15;
```

### Output

| 25 + 15 |
| ------- |
| 40      |

---

# Using Aliases

Aliases make the output easier to read.

```sql
SELECT 'Welcome to SQL' AS Message;
```

### Output

| Message        |
| -------------- |
| Welcome to SQL |

---

# Query Execution Flow

```text
Write SQL Query
        │
        ▼
SQL Client
        │
        ▼
Database Server
        │
        ▼
Execute Query
        │
        ▼
Return Result
        │
        ▼
Display Output
```

---

# How SQL Processes a Query

1. You write a SQL query.
2. The SQL client sends the query to the database server.
3. The database checks the syntax.
4. The query is executed.
5. The result is returned.
6. The SQL client displays the output.

---

# Common SQL Queries for Testing

## Display Current Date

```sql
SELECT CURRENT_DATE;
```

---

## Display Current Time

```sql
SELECT CURRENT_TIME;
```

---

## Display Current Timestamp

```sql
SELECT CURRENT_TIMESTAMP;
```

> **Note:** These functions are supported by most SQL database systems. The exact output format may vary depending on the database.

---

# Database Compatibility

| Query                   | MySQL | PostgreSQL | SQL Server | SQLite |
| ----------------------- | :---: | :--------: | :--------: | :----: |
| `SELECT 'Hello, SQL!';` |   ✅   |      ✅     |      ✅     |    ✅   |
| `SELECT 100;`           |   ✅   |      ✅     |      ✅     |    ✅   |
| `SELECT 25 + 15;`       |   ✅   |      ✅     |      ✅     |    ✅   |
| `CURRENT_DATE`          |   ✅   |      ✅     |     ✅*     |    ✅   |

> *SQL Server uses `CAST(GETDATE() AS DATE)` or similar expressions to return only the current date.

---

# Common Mistakes

* Forgetting the semicolon (`;`) at the end of the query (required in many SQL tools).
* Typing SQL keywords incorrectly.
* Executing the query without connecting to a database server.
* Ignoring syntax error messages.

---

# Best Practices

* Write SQL keywords in uppercase for better readability.
* Use meaningful aliases.
* Execute one query at a time while learning.
* Read error messages carefully.
* Practice simple queries before moving to complex ones.

---

# Interview Questions

### 1. What is a SQL query?

**Answer:** A SQL query is a command used to communicate with a database and perform operations such as retrieving, inserting, updating, or deleting data.

---

### 2. Which keyword is used to retrieve data in SQL?

**Answer:**

```sql
SELECT
```

---

### 3. What does the following query return?

```sql
SELECT 10 + 20;
```

**Answer:**

| 10 + 20 |
| ------- |
| 30      |

---

### 4. What is the purpose of the `SELECT` statement?

**Answer:** It retrieves data or displays values from the database.

---

### 5. How can you verify that your SQL environment is working?

**Answer:** Execute a simple query such as:

```sql
SELECT 'Hello, SQL!';
```

If the query runs successfully and returns the expected output, your SQL environment is working correctly.

---

# Practice Questions

## Easy

1. What is a SQL query?
2. Write a query to display the number **50**.
3. Write a query to display the text **"Welcome"**.
4. What is the purpose of the `SELECT` statement?
5. Execute a query to add **30 + 40**.

---

## Medium

1. Explain the SQL query execution process.
2. Write a query using an alias.
3. Differentiate between a SQL query and a database.
4. Explain how a SQL client communicates with a database server.
5. Execute a query to display the current date.

---

## Hard

1. Explain the complete SQL query execution workflow.
2. Compare SQL query execution in MySQL, PostgreSQL, SQL Server, and SQLite.
3. Discuss common syntax errors beginners make.
4. Explain why SQL keywords are generally written in uppercase.
5. Describe how a database server processes a SQL query internally.

---

# Key Takeaways

* A SQL query is used to communicate with a database.
* The `SELECT` statement is one of the most commonly used SQL commands.
* Simple queries help verify that the SQL environment is working.
* SQL clients send queries to the database server, which executes them and returns the results.
* Practicing basic SQL queries is the foundation for learning advanced SQL concepts.

---

# Conclusion

You have successfully executed your first SQL query. This marks the beginning of your SQL journey. In the next section, you will start learning core SQL concepts such as **DDL (Data Definition Language)**, where you'll create tables and define the structure of your database.
