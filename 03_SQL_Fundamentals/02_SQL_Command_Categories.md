# SQL Command Categories (DDL, DML, DQL, DCL & TCL)

# Introduction

SQL (Structured Query Language) provides different types of commands to perform various operations on a relational database. Instead of having one command for every task, SQL groups similar commands into **five categories**, making it easier to understand and use.

These five categories are:

* DDL (Data Definition Language)
* DML (Data Manipulation Language)
* DQL (Data Query Language)
* DCL (Data Control Language)
* TCL (Transaction Control Language)

Understanding these categories is one of the most important SQL fundamentals and is frequently asked in interviews and placement exams.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand the five SQL command categories.
* Identify which SQL command belongs to which category.
* Know the purpose of each category.
* Learn commonly used SQL commands.
* Differentiate between DDL, DML, DQL, DCL, and TCL.
* Apply the correct category in real-world scenarios.

---

# Problem Statement

Consider an online shopping application.

Different tasks require different SQL commands:

* Create a **Products** table.
* Add new products.
* Display available products.
* Give a manager permission to update products.
* Undo an accidental transaction.

Can one SQL command perform all these operations?

**No.**

SQL divides commands into different categories based on their purpose.

---

# Why Do We Need SQL Command Categories?

Without categories:

* SQL would be difficult to learn.
* Similar commands would be harder to remember.
* Database administration would become confusing.

By grouping commands into categories:

* Learning becomes easier.
* Commands are organized logically.
* Developers can quickly identify the correct command.
* Database operations become more efficient.

---

# SQL Command Categories

| Category | Full Form                    | Purpose                            |
| -------- | ---------------------------- | ---------------------------------- |
| DDL      | Data Definition Language     | Defines database structure         |
| DML      | Data Manipulation Language   | Inserts, updates, and deletes data |
| DQL      | Data Query Language          | Retrieves data                     |
| DCL      | Data Control Language        | Controls user permissions          |
| TCL      | Transaction Control Language | Manages transactions               |

---

# SQL Command Hierarchy

```text
SQL
│
├── DDL
├── DML
├── DQL
├── DCL
└── TCL
```

---

# 1. DDL (Data Definition Language)

## Definition

DDL commands are used to **create and modify the structure of database objects**.

Database objects include:

* Databases
* Tables
* Views
* Indexes

DDL changes the database schema rather than the data itself.

---

## Common DDL Commands

| Command  | Purpose                       |
| -------- | ----------------------------- |
| CREATE   | Creates database objects      |
| ALTER    | Modifies database objects     |
| DROP     | Deletes database objects      |
| TRUNCATE | Removes all rows from a table |
| RENAME*  | Renames database objects      |

> *The syntax for `RENAME` varies between database systems.

---

## Example

Create a table:

```sql
CREATE TABLE Student (
    StudentID INT,
    Name VARCHAR(100)
);
```

---

# 2. DML (Data Manipulation Language)

## Definition

DML commands are used to **modify the data stored inside tables**.

Unlike DDL, DML works with records (rows) rather than the table structure.

---

## Common DML Commands

| Command | Purpose                   |
| ------- | ------------------------- |
| INSERT  | Adds new records          |
| UPDATE  | Modifies existing records |
| DELETE  | Removes records           |

---

## Example

Insert a record:

```sql
INSERT INTO Student (StudentID, Name)
VALUES (101, 'Rahul');
```

Update a record:

```sql
UPDATE Student
SET Name = 'Ravi'
WHERE StudentID = 101;
```

Delete a record:

```sql
DELETE FROM Student
WHERE StudentID = 101;
```

---

# 3. DQL (Data Query Language)

## Definition

DQL commands are used to **retrieve data** from a database.

The primary DQL command is `SELECT`.

---

## Common DQL Command

| Command | Purpose        |
| ------- | -------------- |
| SELECT  | Retrieves data |

---

## Example

```sql
SELECT *
FROM Student;
```

---

# 4. DCL (Data Control Language)

## Definition

DCL commands control **user permissions and database security**.

They determine who can access database objects and what operations users are allowed to perform.

---

## Common DCL Commands

| Command | Purpose             |
| ------- | ------------------- |
| GRANT   | Gives permissions   |
| REVOKE  | Removes permissions |

---

## Example

```sql
GRANT SELECT
ON Student
TO User1;
```

Remove permission:

```sql
REVOKE SELECT
ON Student
FROM User1;
```

---

# 5. TCL (Transaction Control Language)

## Definition

TCL commands manage **database transactions**.

A transaction is a group of SQL statements executed as a single logical unit.

---

## Common TCL Commands

| Command   | Purpose                   |
| --------- | ------------------------- |
| COMMIT    | Saves changes permanently |
| ROLLBACK  | Undoes changes            |
| SAVEPOINT | Creates a rollback point  |

---

## Example

```sql
UPDATE Student
SET Name = 'Kumar'
WHERE StudentID = 101;

COMMIT;
```

Rollback example:

```sql
UPDATE Student
SET Name = 'Arun'
WHERE StudentID = 101;

ROLLBACK;
```

---

# Complete Comparison

| Feature           | DDL                 | DML                    | DQL            | DCL                 | TCL                          |
| ----------------- | ------------------- | ---------------------- | -------------- | ------------------- | ---------------------------- |
| Purpose           | Defines structure   | Modifies data          | Retrieves data | Controls access     | Manages transactions         |
| Works On          | Database objects    | Table rows             | Table rows     | Users & permissions | Transactions                 |
| Common Commands   | CREATE, ALTER, DROP | INSERT, UPDATE, DELETE | SELECT         | GRANT, REVOKE       | COMMIT, ROLLBACK, SAVEPOINT  |
| Affects Structure | Yes                 | No                     | No             | No                  | No                           |
| Affects Data      | No                  | Yes                    | Reads only     | No                  | Controls transaction results |

---

# Real-World Example

Consider an **Online Shopping System**.

| Task                   | Category | Example Command |
| ---------------------- | -------- | --------------- |
| Create Products table  | DDL      | CREATE TABLE    |
| Add a product          | DML      | INSERT          |
| Display products       | DQL      | SELECT          |
| Give manager access    | DCL      | GRANT           |
| Save order transaction | TCL      | COMMIT          |

---

# SQL Command Flow

```text
Create Database
      │
      ▼
DDL
(Create Tables)
      │
      ▼
DML
(Insert / Update / Delete)
      │
      ▼
DQL
(Retrieve Data)
      │
      ▼
DCL
(Manage Permissions)
      │
      ▼
TCL
(Manage Transactions)
```

---

# Advantages of Command Categories

* Easy to understand.
* Organized learning approach.
* Improves SQL readability.
* Simplifies database management.
* Frequently used in interviews and certifications.

---

# Common Mistakes

* Confusing `DELETE` with `DROP`.
* Assuming `SELECT` belongs to DML.
* Forgetting to use `COMMIT` where required.
* Using `TRUNCATE` to remove only specific rows.
* Assuming all SQL databases support every command with identical syntax.

---

# Best Practices

* Learn SQL commands category by category.
* Use `SELECT` to verify data before updating or deleting.
* Use transactions for critical operations.
* Grant users only the permissions they require.
* Always include a `WHERE` clause when using `UPDATE` or `DELETE` unless all rows should be affected.

---

# Interview Questions

### 1. How many SQL command categories are there?

**Answer:** Five — DDL, DML, DQL, DCL, and TCL.

---

### 2. Which SQL category is used to create tables?

**Answer:** DDL.

---

### 3. Which command is used to retrieve data?

**Answer:**

```sql
SELECT * FROM Student;
```

---

### 4. Which SQL category manages user permissions?

**Answer:** DCL.

---

### 5. Which command permanently saves a transaction?

**Answer:**

```sql
COMMIT;
```

---

# Practice Questions

## Easy

1. What is DDL?
2. Expand DML.
3. Which category does `SELECT` belong to?
4. Name two DCL commands.
5. What is the purpose of TCL?

---

## Medium

1. Explain each SQL command category with one example.
2. Differentiate between DDL and DML.
3. Compare DML and DQL.
4. Explain the purpose of DCL in database security.
5. Describe the role of TCL in transaction management.

---

## Hard

1. Compare all five SQL command categories with suitable examples.
2. Explain the execution flow of SQL commands in a real-world application.
3. Why is `SELECT` classified as DQL instead of DML?
4. Explain how DCL and TCL contribute to secure and reliable database systems.
5. Design a workflow showing how all five SQL command categories are used in a banking application.

---

# Key Takeaways

* SQL commands are divided into **five categories**.
* **DDL** defines the database structure.
* **DML** inserts, updates, and deletes records.
* **DQL** retrieves data using the `SELECT` statement.
* **DCL** manages user permissions.
* **TCL** controls transactions using commands such as `COMMIT` and `ROLLBACK`.
* Understanding these categories is fundamental for SQL development and technical interviews.

---

# Conclusion

The five SQL command categories form the foundation of database management. Each category has a specific responsibility, making SQL organized, powerful, and easy to use. In the next chapter, you will begin working with **DDL commands** by creating your own databases and tables.
