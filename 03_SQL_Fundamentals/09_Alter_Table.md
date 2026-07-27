# ALTER TABLE

# Introduction

After creating a table, you may need to modify its structure as your application evolves. For example, you might need to add a new column, change a column's data type, rename a column, or remove an unnecessary column.

The **`ALTER TABLE`** statement is used to modify the structure of an existing table without deleting the table or its data (although some operations may affect existing data).

In this chapter, you will learn how to use the `ALTER TABLE` statement to make structural changes to database tables.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand the purpose of the `ALTER TABLE` statement.
* Add new columns.
* Modify existing columns.
* Rename columns.
* Drop columns.
* Rename a table.
* Follow best practices while modifying tables.

---

# Problem Statement

Suppose your **Student** table currently has the following columns:

| StudentID | Name | Age | Department |
| --------- | ---- | --- | ---------- |

Later, your application requires storing each student's **Email Address**.

Should you delete the table and create it again?

**No.**

Instead, use the **`ALTER TABLE`** statement to modify the existing table.

---

# Why Do We Need ALTER TABLE?

As software applications grow, database requirements also change.

Examples include:

* Add a new column.
* Remove an unused column.
* Increase the length of a text column.
* Rename a column.
* Rename a table.
* Change a column's data type.

The `ALTER TABLE` statement allows these changes without recreating the table.

---

# What is ALTER TABLE?

The **`ALTER TABLE`** statement modifies the structure of an existing table.

Unlike `INSERT`, `UPDATE`, and `DELETE`, which work with data, `ALTER TABLE` changes the **schema** of the table.

---

# Basic Syntax

```sql
ALTER TABLE table_name
operation;
```

The **operation** can be:

* ADD COLUMN
* MODIFY COLUMN
* ALTER COLUMN
* RENAME COLUMN
* DROP COLUMN
* RENAME TO

---

# Example Table

Assume the following table already exists.

```sql
CREATE TABLE Student (
    StudentID INT,
    Name VARCHAR(100),
    Age INT,
    Department VARCHAR(50)
);
```

---

# Operation 1 – Add a New Column

## Syntax

```sql
ALTER TABLE table_name
ADD column_name data_type;
```

### Example

```sql
ALTER TABLE Student
ADD Email VARCHAR(100);
```

### Result

| StudentID | Name | Age | Department | Email |
| --------- | ---- | --- | ---------- | ----- |

---

# Operation 2 – Add Multiple Columns

Some database systems support adding multiple columns in one statement.

```sql
ALTER TABLE Student
ADD Phone VARCHAR(15),
ADD Address VARCHAR(200);
```

> **Note:** The syntax for adding multiple columns varies between database systems.

---

# Operation 3 – Modify a Column

Used to change the data type or size of a column.

## MySQL

```sql
ALTER TABLE Student
MODIFY Name VARCHAR(150);
```

## SQL Server

```sql
ALTER TABLE Student
ALTER COLUMN Name VARCHAR(150);
```

---

# Operation 4 – Rename a Column

## MySQL

```sql
ALTER TABLE Student
RENAME COLUMN Name TO StudentName;
```

## SQL Server

```sql
EXEC sp_rename
'Student.Name',
'StudentName',
'COLUMN';
```

---

# Operation 5 – Drop a Column

## Syntax

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

### Example

```sql
ALTER TABLE Student
DROP COLUMN Age;
```

### Result

| StudentID | Name | Department | Email |
| --------- | ---- | ---------- | ----- |

---

# Operation 6 – Rename a Table

## MySQL

```sql
RENAME TABLE Student
TO Students;
```

## PostgreSQL

```sql
ALTER TABLE Student
RENAME TO Students;
```

## SQL Server

```sql
EXEC sp_rename
'Student',
'Students';
```

---

# Before and After Example

### Before

| StudentID | Name | Age | Department |
| --------- | ---- | --- | ---------- |

### Execute

```sql
ALTER TABLE Student
ADD Email VARCHAR(100);
```

### After

| StudentID | Name | Age | Department | Email |
| --------- | ---- | --- | ---------- | ----- |

---

# Internal Working

```text
User
   │
   ▼
ALTER TABLE Statement
   │
   ▼
DBMS Validates
(Table Exists?)
(Column Exists?)
(Data Type?)
   │
   ▼
Update Table Schema
   │
   ▼
Modified Table Ready
```

---

# Common ALTER TABLE Operations

| Operation     | Purpose                          |
| ------------- | -------------------------------- |
| ADD COLUMN    | Add a new column                 |
| MODIFY COLUMN | Change data type or size (MySQL) |
| ALTER COLUMN  | Change data type (SQL Server)    |
| RENAME COLUMN | Rename a column                  |
| DROP COLUMN   | Remove a column                  |
| RENAME TO     | Rename a table                   |

---

# Database Compatibility

| Feature       | MySQL | PostgreSQL |    SQL Server   |  SQLite  |
| ------------- | :---: | :--------: | :-------------: | :------: |
| ADD COLUMN    |   ✅   |      ✅     |        ✅        |     ✅    |
| DROP COLUMN   |   ✅   |      ✅     |        ✅        | Limited* |
| MODIFY COLUMN |   ✅   |      ❌     |        ❌        |     ❌    |
| ALTER COLUMN  |   ❌   |      ❌     |        ✅        |     ❌    |
| RENAME COLUMN |   ✅   |      ✅     | Via `sp_rename` |     ✅    |
| RENAME TABLE  |   ✅   |      ✅     | Via `sp_rename` |     ✅    |

> *Older SQLite versions have limited support for some `ALTER TABLE` operations.

---

# Real-World Applications

| Industry   | Example                  |
| ---------- | ------------------------ |
| School     | Add ParentPhone column   |
| Banking    | Add AadhaarNumber column |
| Hospital   | Add BloodGroup column    |
| E-Commerce | Add ProductImage column  |
| HR         | Add JoiningDate column   |
| Library    | Add BookCategory column  |

---

# Advantages

* Modifies existing tables without recreating them.
* Preserves existing data in most operations.
* Supports schema evolution.
* Saves development time.
* Essential for maintaining production databases.

---

# Common Mistakes

* Modifying the wrong table.
* Dropping important columns accidentally.
* Changing a data type that is incompatible with existing data.
* Forgetting to back up production databases.
* Assuming the same syntax works across all database systems.

---

# Best Practices

* Back up important tables before altering them.
* Test structural changes in a development environment.
* Use meaningful column names.
* Verify existing data before changing data types.
* Document all schema changes.

---

# Interview Questions

### 1. What is the purpose of the `ALTER TABLE` statement?

**Answer:** It is used to modify the structure of an existing table.

---

### 2. Can `ALTER TABLE` add a new column?

**Answer:** Yes.

```sql
ALTER TABLE Student
ADD Email VARCHAR(100);
```

---

### 3. Can `ALTER TABLE` change a column's data type?

**Answer:** Yes. The syntax depends on the database system.

---

### 4. Does `ALTER TABLE` delete existing data?

**Answer:** Generally, no. However, certain operations, such as dropping a column, permanently remove the data stored in that column.

---

### 5. Why should `ALTER TABLE` be used carefully in production?

**Answer:** Structural changes may affect applications, indexes, constraints, and existing data. Always test and back up the database before making changes.

---

# Practice Questions

## Easy

1. What is the purpose of `ALTER TABLE`?
2. Write the syntax to add a column.
3. Write the syntax to drop a column.
4. Can `ALTER TABLE` rename a column?
5. Can it rename a table?

---

## Medium

1. Add an `Email` column to the `Student` table.
2. Change the size of the `Name` column.
3. Remove the `Age` column.
4. Rename the `Department` column to `Branch`.
5. Explain the internal working of `ALTER TABLE`.

---

## Hard

1. Compare `ALTER TABLE` syntax across MySQL, PostgreSQL, SQL Server, and SQLite.
2. Explain how schema changes affect existing applications.
3. Discuss the risks of dropping columns in production.
4. Describe best practices for modifying database schemas.
5. Design a migration plan to add new columns to a large production table.

---

# Key Takeaways

* `ALTER TABLE` modifies the structure of an existing table.
* It can add, modify, rename, and remove columns.
* Some syntax differs between database systems.
* Structural changes should be tested before applying them in production.
* Always back up important data before making schema changes.

---

# Conclusion

The `ALTER TABLE` statement is one of the most powerful DDL commands because it allows database schemas to evolve as application requirements change. Understanding how to safely modify tables is an essential skill for every SQL developer. In the next chapter, you will learn how to **rename tables and columns** in greater detail and explore additional schema modification techniques.
