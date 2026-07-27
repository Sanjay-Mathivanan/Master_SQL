# Rename Column

# Introduction

As software applications evolve, database column names often need to be updated to better reflect their purpose. A column created with a short or unclear name during development may later require a more descriptive name.

For example:

* `Name` → `StudentName`
* `Dept` → `Department`
* `Mob` → `MobileNumber`

Instead of creating a new table or copying data, SQL allows us to rename an existing column while preserving its data.

In this chapter, you will learn how to rename columns in different Database Management Systems (DBMS), understand how the operation works internally, and follow best practices.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand the purpose of renaming a column.
* Rename a column in MySQL.
* Rename a column in PostgreSQL.
* Rename a column in SQL Server.
* Rename a column in SQLite.
* Understand the impact of renaming a column.
* Follow best practices.

---

# Problem Statement

Suppose the **Student** table has the following structure.

| StudentID | Name | Age | Department |
| --------- | ---- | --- | ---------- |

Your development team decides that the column **Name** should be renamed to **StudentName** for better readability.

How can this be done without losing the existing data?

The answer is by using the **Rename Column** command.

---

# Why Do We Need to Rename a Column?

Renaming a column helps to:

* Improve readability.
* Follow naming conventions.
* Correct spelling mistakes.
* Make the database easier to maintain.
* Better represent the data stored in the column.

---

# What is Rename Column?

Renaming a column changes only the **column name**.

It does **not** change:

* Existing data
* Data type
* Constraints
* Default values
* Indexes (in most databases)

Only the name of the column is modified.

---

# Example Table

```sql
CREATE TABLE Student (
    StudentID INT,
    Name VARCHAR(100),
    Age INT,
    Department VARCHAR(50)
);
```

---

# Syntax

## MySQL (Version 8.0+)

```sql
ALTER TABLE table_name
RENAME COLUMN old_column_name
TO new_column_name;
```

---

## PostgreSQL

```sql
ALTER TABLE table_name
RENAME COLUMN old_column_name
TO new_column_name;
```

---

## SQL Server

```sql
EXEC sp_rename
'table_name.old_column_name',
'new_column_name',
'COLUMN';
```

---

## SQLite

```sql
ALTER TABLE table_name
RENAME COLUMN old_column_name
TO new_column_name;
```

---

# Example 1 – MySQL

Rename the **Name** column.

```sql
ALTER TABLE Student
RENAME COLUMN Name
TO StudentName;
```

---

# Before Rename

| StudentID | Name  | Age | Department |
| --------- | ----- | --- | ---------- |
| 101       | Rahul | 20  | CSE        |

---

# After Rename

| StudentID | StudentName | Age | Department |
| --------- | ----------- | --- | ---------- |
| 101       | Rahul       | 20  | CSE        |

Notice that only the column name has changed.

---

# Example 2 – PostgreSQL

```sql
ALTER TABLE Student
RENAME COLUMN Name
TO StudentName;
```

---

# Example 3 – SQL Server

```sql
EXEC sp_rename
'Student.Name',
'StudentName',
'COLUMN';
```

---

# Example 4 – SQLite

```sql
ALTER TABLE Student
RENAME COLUMN Name
TO StudentName;
```

---

# Verify the Rename

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
sp_help Student;
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
Rename Column Command
   │
   ▼
DBMS Validates
(Table Exists?)
(Column Exists?)
(New Name Available?)
   │
   ▼
System Catalog Updated
   │
   ▼
Column Renamed
```

---

# Before and After

## Before

```text
Student
│
├── StudentID
├── Name
├── Age
└── Department
```

---

## Rename

```sql
ALTER TABLE Student
RENAME COLUMN Name
TO StudentName;
```

---

## After

```text
Student
│
├── StudentID
├── StudentName
├── Age
└── Department
```

---

# Database Compatibility

| Feature               | MySQL | PostgreSQL | SQL Server | SQLite |
| --------------------- | :---: | :--------: | :--------: | :----: |
| Rename Column         |   ✅   |      ✅     |      ✅     |    ✅   |
| Data Preserved        |   ✅   |      ✅     |      ✅     |    ✅   |
| Constraints Preserved |   ✅   |      ✅     |      ✅     |    ✅   |
| Data Type Preserved   |   ✅   |      ✅     |      ✅     |    ✅   |

---

# Real-World Applications

| Industry   | Example                    |
| ---------- | -------------------------- |
| School     | `Name` → `StudentName`     |
| Banking    | `AccNo` → `AccountNumber`  |
| Hospital   | `PatName` → `PatientName`  |
| E-Commerce | `ProdName` → `ProductName` |
| HR         | `EmpName` → `EmployeeName` |
| Library    | `BookName` → `BookTitle`   |

---

# Advantages

* Improves readability.
* Makes the schema more meaningful.
* Preserves existing data.
* Supports standard naming conventions.
* Easy to perform.

---

# Limitations

* Existing SQL queries may stop working until updated.
* Views, stored procedures, triggers, and reports may require changes.
* Application source code must also be updated.

---

# Common Mistakes

* Renaming a column that does not exist.
* Using a name that already exists in the same table.
* Forgetting to update application code.
* Ignoring dependent database objects.
* Not verifying the updated schema.

---

# Best Practices

* Use descriptive column names.
* Follow consistent naming conventions.
* Rename columns during planned maintenance whenever possible.
* Test all dependent queries after renaming.
* Verify the updated table structure.

---

# Interview Questions

### 1. What is the purpose of renaming a column?

**Answer:** It changes the name of an existing column without affecting its stored data.

---

### 2. Does renaming a column delete existing data?

**Answer:** No. Only the column name changes. The data remains unchanged.

---

### 3. Which command is used to rename a column in MySQL?

**Answer:**

```sql
ALTER TABLE Student
RENAME COLUMN Name
TO StudentName;
```

---

### 4. Which command is used in SQL Server?

**Answer:**

```sql
EXEC sp_rename
'Student.Name',
'StudentName',
'COLUMN';
```

---

### 5. What should developers update after renaming a column?

**Answer:**

* SQL queries
* Views
* Stored procedures
* Triggers
* Reports
* Application source code

---

# Practice Questions

## Easy

1. What is the purpose of renaming a column?
2. Write the MySQL syntax for renaming a column.
3. Does renaming affect existing data?
4. How do you verify that a column has been renamed?
5. Can a column be renamed to an existing column name?

---

## Medium

1. Rename the `Dept` column to `Department`.
2. Rename the `EmpName` column to `EmployeeName`.
3. Explain the internal working of a column rename operation.
4. Compare MySQL and SQL Server syntax for renaming columns.
5. List five real-world examples of column renaming.

---

## Hard

1. Explain how renaming a column affects applications and database objects.
2. Compare column renaming across MySQL, PostgreSQL, SQL Server, and SQLite.
3. Describe best practices for renaming columns in production databases.
4. Discuss the risks involved when renaming frequently used columns.
5. Design a migration strategy for renaming multiple columns in a production database.

---

# Key Takeaways

* Renaming a column changes only its name.
* Existing data, constraints, and data types remain unchanged.
* Different database systems use slightly different syntax.
* Application code and dependent database objects should be updated.
* Always verify the schema after renaming a column.

---

# Conclusion

Renaming columns is an important database maintenance task that improves clarity, consistency, and maintainability without affecting the stored data. By understanding the syntax used by different database systems and following best practices, developers can safely update database schemas as applications evolve. In the next chapter, you will learn how to **add, modify, and drop columns** using the **`ALTER TABLE`** statement.
