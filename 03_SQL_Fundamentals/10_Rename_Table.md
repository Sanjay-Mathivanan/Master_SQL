# Rename Table

# Introduction

As applications evolve, database table names may need to change. A table created during development might have a temporary name, or a business requirement may require a more meaningful name.

For example:

* `Student` → `Students`
* `Emp` → `Employee`
* `Cust` → `Customer`

Instead of creating a new table and copying all the data, SQL provides commands to **rename an existing table**.

In this chapter, you will learn how to rename tables in different database management systems, understand the internal working of the rename operation, and follow best practices.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand the purpose of renaming a table.
* Rename a table in MySQL.
* Rename a table in PostgreSQL.
* Rename a table in SQL Server.
* Rename a table in SQLite.
* Understand the impact of renaming a table.
* Follow industry best practices.

---

# Problem Statement

Suppose your database contains the following table:

| Table Name |
| ---------- |
| Student    |

Later, your organization decides that all table names should be plural.

The new table name should be:

| Old Name | New Name |
| -------- | -------- |
| Student  | Students |

How can this be done without deleting the table or losing the data?

The answer is by using the **Rename Table** command.

---

# Why Do We Need to Rename a Table?

Table names may change because of:

* Better naming conventions.
* Business requirement changes.
* Improving readability.
* Standardizing database design.
* Correcting spelling mistakes.
* Making names more descriptive.

---

# What is Rename Table?

Renaming a table changes only the **name of the table**.

It does **not** change:

* The table data
* The columns
* The data types
* The constraints
* The indexes

Only the table name changes.

---

# Syntax

## MySQL

```sql
RENAME TABLE old_table_name
TO new_table_name;
```

---

## PostgreSQL

```sql
ALTER TABLE old_table_name
RENAME TO new_table_name;
```

---

## SQL Server

```sql
EXEC sp_rename
'old_table_name',
'new_table_name';
```

---

## SQLite

```sql
ALTER TABLE old_table_name
RENAME TO new_table_name;
```

---

# Example 1 – MySQL

Suppose the following table exists.

```sql
CREATE TABLE Student (
    StudentID INT,
    Name VARCHAR(100),
    Department VARCHAR(50)
);
```

Rename it.

```sql
RENAME TABLE Student
TO Students;
```

---

# Result

## Before

| Tables  |
| ------- |
| Student |

---

## After

| Tables   |
| -------- |
| Students |

The data remains unchanged.

---

# Example 2 – PostgreSQL

```sql
ALTER TABLE Student
RENAME TO Students;
```

---

# Example 3 – SQL Server

```sql
EXEC sp_rename
'Student',
'Students';
```

---

# Example 4 – SQLite

```sql
ALTER TABLE Student
RENAME TO Students;
```

---

# Verify the Rename

### MySQL

```sql
SHOW TABLES;
```

---

### PostgreSQL

```sql
SELECT tablename
FROM pg_tables;
```

---

### SQL Server

```sql
SELECT name
FROM sys.tables;
```

---

### SQLite

```sql
.tables
```

---

# Internal Working

```text
User
   │
   ▼
Rename Table Command
   │
   ▼
DBMS Validates
(Table Exists?)
(New Name Available?)
   │
   ▼
System Catalog Updated
   │
   ▼
Table Renamed
```

---

# Before and After

## Before

```text
Student
│
├── StudentID
├── Name
├── Department
└── Email
```

---

## Rename

```sql
ALTER TABLE Student
RENAME TO Students;
```

---

## After

```text
Students
│
├── StudentID
├── Name
├── Department
└── Email
```

Notice that only the **table name** changes.

---

# Database Compatibility

| Feature               | MySQL | PostgreSQL | SQL Server | SQLite |
| --------------------- | :---: | :--------: | :--------: | :----: |
| Rename Table          |   ✅   |      ✅     |      ✅     |    ✅   |
| Data Preserved        |   ✅   |      ✅     |      ✅     |    ✅   |
| Constraints Preserved |   ✅   |      ✅     |      ✅     |    ✅   |
| Indexes Preserved     |   ✅   |      ✅     |      ✅     |    ✅   |

---

# Real-World Applications

| Industry   | Example                |
| ---------- | ---------------------- |
| School     | `Student` → `Students` |
| Banking    | `Account` → `Accounts` |
| Hospital   | `Patient` → `Patients` |
| E-Commerce | `Product` → `Products` |
| HR         | `Emp` → `Employee`     |
| Library    | `Book` → `Books`       |

---

# Advantages

* Keeps existing data intact.
* No need to recreate the table.
* Improves readability.
* Supports standard naming conventions.
* Fast schema modification.

---

# Limitations

* Applications using the old table name must be updated.
* Stored procedures, views, and scripts referencing the old name may require modification.
* Some database tools may need metadata to be refreshed.

---

# Common Mistakes

* Renaming a table that does not exist.
* Choosing a table name that already exists.
* Forgetting to update application code.
* Ignoring dependent views or stored procedures.
* Not verifying the rename operation.

---

# Best Practices

* Use meaningful and consistent table names.
* Follow your team's naming conventions.
* Test the rename operation in a development environment first.
* Update all dependent SQL queries and application code.
* Verify the new table name after renaming.

---

# Interview Questions

### 1. What is the purpose of renaming a table?

**Answer:** It changes the name of an existing table without affecting its data or structure.

---

### 2. Does renaming a table delete its data?

**Answer:** No. Only the table name changes. All existing records remain unchanged.

---

### 3. Which command is used to rename a table in PostgreSQL?

**Answer:**

```sql
ALTER TABLE Student
RENAME TO Students;
```

---

### 4. Which command is used in SQL Server?

**Answer:**

```sql
EXEC sp_rename
'Student',
'Students';
```

---

### 5. What should developers check after renaming a table?

**Answer:**

* Application code
* Views
* Stored procedures
* Triggers
* Reports
* SQL scripts

---

# Practice Questions

## Easy

1. What is the purpose of renaming a table?
2. Write the MySQL syntax for renaming a table.
3. Does renaming affect the stored data?
4. How do you verify a renamed table?
5. Can a table be renamed to an existing table name?

---

## Medium

1. Rename the `Employee` table to `Employees`.
2. Rename the `Customer` table using PostgreSQL syntax.
3. Explain the internal working of a rename operation.
4. Compare MySQL and SQL Server syntax for renaming a table.
5. List five real-world situations where renaming a table is useful.

---

## Hard

1. Explain how table renaming affects application code and database objects.
2. Compare table renaming across MySQL, PostgreSQL, SQL Server, and SQLite.
3. Describe best practices for renaming tables in production databases.
4. Discuss the risks involved when renaming frequently used tables.
5. Design a migration strategy for renaming multiple tables in a live database.

---

# Key Takeaways

* Renaming a table changes only its name.
* The data and table structure remain unchanged.
* Different database systems use different syntax.
* Application code and dependent database objects may need updating.
* Always verify the renamed table after making the change.

---

# Conclusion

Renaming a table is a simple but important database maintenance task that improves readability, consistency, and long-term maintainability. Since different database systems use different syntax, understanding these differences is essential for database developers and administrators. In the next chapter, you will learn how to **rename table columns** using the **`RENAME COLUMN`** statement and database-specific alternatives.
