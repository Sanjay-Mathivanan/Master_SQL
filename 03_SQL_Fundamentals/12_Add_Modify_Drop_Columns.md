# Add, Modify, and Drop Columns

# Introduction

As applications evolve, database requirements also change. A table created today may require additional columns tomorrow, existing columns may need a larger size, or some columns may become obsolete.

The **`ALTER TABLE`** statement provides operations to:

* Add new columns
* Modify existing columns
* Drop unwanted columns

These operations allow developers to update the database schema without recreating the entire table.

In this chapter, you will learn how to add, modify, and drop columns in different Database Management Systems (DBMS), understand their internal working, and follow best practices.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Add new columns to an existing table.
* Modify the data type or size of existing columns.
* Drop unnecessary columns.
* Understand differences between database systems.
* Follow best practices while changing table structures.

---

# Problem Statement

Suppose the following **Student** table already exists.

| StudentID | Name | Age | Department |
| --------- | ---- | --- | ---------- |

After a few months, new requirements arise.

* Store each student's email address.
* Increase the length of the **Name** column.
* Remove the **Age** column because it is no longer required.

Instead of creating a new table, these changes can be performed using **ALTER TABLE**.

---

# Why Do We Need These Operations?

Database structures frequently change due to:

* New business requirements.
* Additional application features.
* Improved database design.
* Removal of unused fields.
* Better data storage.
* Schema optimisation.

---

# Understanding ALTER TABLE

The **ALTER TABLE** statement modifies the structure (schema) of an existing table.

It allows developers to:

* Add columns
* Modify columns
* Drop columns
* Rename columns
* Rename tables

This chapter focuses on **Add**, **Modify**, and **Drop** operations.

---

# Operation 1 – Add Column

## Definition

The **ADD COLUMN** operation adds a new column to an existing table.

Existing rows remain unchanged. The newly added column usually contains `NULL` values unless a default value is specified.

---

## Syntax

```sql
ALTER TABLE table_name
ADD column_name data_type;
```

---

## Example

```sql
ALTER TABLE Student
ADD Email VARCHAR(100);
```

---

## Table Before

| StudentID | Name | Age | Department |
| --------- | ---- | --- | ---------- |

---

## Table After

| StudentID | Name | Age | Department | Email |
| --------- | ---- | --- | ---------- | ----- |

The new **Email** column is added to the table.

---

# Adding Multiple Columns

Some database systems support adding multiple columns in one statement.

## Example

```sql
ALTER TABLE Student
ADD Phone VARCHAR(15),
ADD Address VARCHAR(200);
```

> **Note:** The syntax for adding multiple columns differs slightly between database systems.

---

# Operation 2 – Modify Column

## Definition

The **MODIFY** (or **ALTER COLUMN**) operation changes the properties of an existing column.

Common changes include:

* Increasing column length
* Changing the data type
* Changing nullability (database dependent)

---

# MySQL Syntax

```sql
ALTER TABLE Student
MODIFY Name VARCHAR(150);
```

---

# SQL Server Syntax

```sql
ALTER TABLE Student
ALTER COLUMN Name VARCHAR(150);
```

---

# PostgreSQL Syntax

```sql
ALTER TABLE Student
ALTER COLUMN Name TYPE VARCHAR(150);
```

---

## Result

The **Name** column size increases from 100 characters to 150 characters.

---

# Operation 3 – Drop Column

## Definition

The **DROP COLUMN** operation permanently removes a column from the table.

> **Important:** Both the column definition and all data stored in that column are permanently deleted.

---

## Syntax

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

---

## Example

```sql
ALTER TABLE Student
DROP COLUMN Age;
```

---

## Table Before

| StudentID | Name | Age | Department | Email |
| --------- | ---- | --- | ---------- | ----- |

---

## Table After

| StudentID | Name | Department | Email |
| --------- | ---- | ---------- | ----- |

The **Age** column has been removed permanently.

---

# Complete Example

Suppose we perform all three operations.

## Step 1 – Add Email

```sql
ALTER TABLE Student
ADD Email VARCHAR(100);
```

---

## Step 2 – Modify Name

```sql
ALTER TABLE Student
MODIFY Name VARCHAR(150);
```

(MySQL syntax)

---

## Step 3 – Drop Age

```sql
ALTER TABLE Student
DROP COLUMN Age;
```

---

## Final Table

| StudentID | Name | Department | Email |
| --------- | ---- | ---------- | ----- |

---

# Internal Working

```text
User
   │
   ▼
ALTER TABLE Statement
   │
   ▼
DBMS Validation
(Table Exists?)
(Column Exists?)
(Data Type Valid?)
   │
   ▼
Update Table Schema
   │
   ▼
Metadata Updated
   │
   ▼
Modified Table Ready
```

---

# Database Compatibility

| Operation     | MySQL | PostgreSQL | SQL Server | SQLite |
| ------------- | :---: | :--------: | :--------: | :----: |
| ADD COLUMN    |   ✅   |      ✅     |      ✅     |    ✅   |
| MODIFY COLUMN |   ✅   |      ❌     |      ❌     |    ❌   |
| ALTER COLUMN  |   ❌   |     ✅*     |      ✅     |    ❌   |
| DROP COLUMN   |   ✅   |      ✅     |      ✅     |   ✅**  |

> *PostgreSQL uses `ALTER COLUMN ... TYPE` for changing a data type.

> **Modern SQLite versions support `DROP COLUMN`. Older versions require recreating the table.

---

# Real-World Applications

| Industry   | Example                            |
| ---------- | ---------------------------------- |
| School     | Add ParentPhone column             |
| Banking    | Increase AccountHolderName length  |
| Hospital   | Remove obsolete InsuranceID column |
| E-Commerce | Add ProductImage column            |
| HR         | Add JoiningDate column             |
| Library    | Remove unused ShelfCode column     |

---

# Advantages

* Modifies existing tables without recreating them.
* Saves development time.
* Preserves existing data in most operations.
* Supports evolving business requirements.
* Works efficiently on production databases when planned properly.

---

# Limitations

* Dropping a column permanently removes its data.
* Some operations may lock the table temporarily.
* Syntax differs across database systems.
* Schema changes may affect dependent applications.

---

# Common Mistakes

* Dropping the wrong column.
* Changing a data type that is incompatible with existing data.
* Forgetting to back up important tables.
* Using database-specific syntax in another DBMS.
* Not checking dependencies before modifying columns.

---

# Best Practices

* Always back up production databases before making structural changes.
* Test schema modifications in a development environment.
* Use descriptive column names.
* Verify existing data before changing data types.
* Review dependent applications, views, triggers, and stored procedures.
* Document all schema modifications for future maintenance.

---

# Interview Questions

### 1. What is the purpose of the `ALTER TABLE` statement?

**Answer:** It is used to modify the structure of an existing table.

---

### 2. Which operation is used to add a new column?

**Answer:**

```sql
ALTER TABLE Student
ADD Email VARCHAR(100);
```

---

### 3. What is the difference between `ADD COLUMN` and `MODIFY COLUMN`?

| ADD COLUMN                      | MODIFY COLUMN                           |
| ------------------------------- | --------------------------------------- |
| Adds a new column               | Changes an existing column              |
| Existing data remains unchanged | Existing column properties are modified |

---

### 4. What happens when a column is dropped?

**Answer:** The column definition and all data stored in that column are permanently removed.

---

### 5. Why should developers be careful while dropping columns?

**Answer:** Because the operation permanently removes data and may affect applications, reports, views, triggers, and stored procedures.

---

# Practice Questions

## Easy

1. What is the purpose of `ADD COLUMN`?
2. Write the syntax to add a new column.
3. What is the purpose of `MODIFY COLUMN`?
4. What happens when a column is dropped?
5. Can existing data remain after adding a new column?

---

## Medium

1. Add an `Email` column to the `Student` table.
2. Increase the size of the `Name` column to 150 characters.
3. Remove the `Age` column from the `Student` table.
4. Compare `ADD COLUMN` and `DROP COLUMN`.
5. Explain the internal working of `ALTER TABLE`.

---

## Hard

1. Compare `ADD`, `MODIFY`, and `DROP` operations across MySQL, PostgreSQL, SQL Server, and SQLite.
2. Explain the risks of dropping columns in a production database.
3. Describe how schema changes affect existing applications.
4. Design a migration strategy to safely modify a production database.
5. Explain best practices for maintaining database schema changes.

---

# Key Takeaways

* `ADD COLUMN` adds new columns to an existing table.
* `MODIFY` or `ALTER COLUMN` changes the properties of existing columns.
* `DROP COLUMN` permanently removes a column and its data.
* Different database systems use slightly different syntax.
* Always test schema changes and take backups before applying them to production databases.

---

# Conclusion

Adding, modifying, and dropping columns are among the most common database maintenance tasks. These operations allow developers to adapt the database schema as business requirements change without recreating entire tables. Understanding the syntax differences across database systems and following best practices helps ensure safe and reliable schema modifications. In the next chapter, you will learn the important differences between **`DELETE`**, **`TRUNCATE`**, and **`DROP`**, including when each command should be used.
