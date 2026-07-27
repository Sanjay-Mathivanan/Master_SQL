# Delete Data

# Introduction

As data changes over time, some records become unnecessary. For example, an employee may resign, a customer may close an account, or a product may be discontinued.

The **`DELETE`** statement is used to remove one or more records from a table. Unlike the `DROP` statement, `DELETE` removes only the data while keeping the table structure intact.

In this chapter, you will learn how to delete records safely, use the `WHERE` clause correctly, and understand the difference between deleting specific rows and deleting all rows.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand the purpose of the `DELETE` statement.
* Delete a single record.
* Delete multiple records.
* Delete all records from a table.
* Understand the importance of the `WHERE` clause.
* Follow best practices for deleting data safely.

---

# Problem Statement

Suppose the **Student** table contains the following records.

| StudentID | Name  | Age | Department | Email                                         |
| --------- | ----- | --- | ---------- | --------------------------------------------- |
| 101       | Rahul | 20  | CSE        | [rahul@example.com](mailto:rahul@example.com) |
| 102       | Priya | 19  | AI         | [priya@example.com](mailto:priya@example.com) |
| 103       | Arun  | 21  | ECE        | [arun@example.com](mailto:arun@example.com)   |
| 104       | Sneha | 20  | IT         | [sneha@example.com](mailto:sneha@example.com) |

Student **103** has completed the course and the record needs to be removed.

How can we delete only that student's record without affecting the remaining records?

The answer is the **`DELETE`** statement.

---

# Why Do We Need DELETE?

The `DELETE` statement allows us to:

* Remove unwanted records.
* Delete inactive users.
* Remove duplicate entries.
* Clean old or obsolete data.
* Maintain accurate information.

Without `DELETE`, unnecessary records would continue to occupy database storage.

---

# What is DELETE?

The **`DELETE`** statement removes one or more rows from a table.

It deletes only the data, **not** the table structure, column definitions, indexes, or constraints.

---

# Syntax

## Delete a Specific Record

```sql
DELETE FROM table_name
WHERE condition;
```

---

## Delete All Records

```sql
DELETE FROM table_name;
```

> **Warning:** This removes every row from the table while keeping the table structure.

---

# Example 1 – Delete a Single Record

```sql
DELETE FROM Student
WHERE StudentID = 103;
```

### Before Delete

| StudentID | Name  | Department |
| --------- | ----- | ---------- |
| 101       | Rahul | CSE        |
| 102       | Priya | AI         |
| 103       | Arun  | ECE        |
| 104       | Sneha | IT         |

### After Delete

| StudentID | Name  | Department |
| --------- | ----- | ---------- |
| 101       | Rahul | CSE        |
| 102       | Priya | AI         |
| 104       | Sneha | IT         |

---

# Example 2 – Delete Multiple Records

```sql
DELETE FROM Student
WHERE Department = 'AI';
```

### Before Delete

| StudentID | Name  | Department |
| --------- | ----- | ---------- |
| 102       | Priya | AI         |
| 105       | Kiran | AI         |
| 106       | Meena | AI         |

### After Delete

| StudentID                | Name | Department |
| ------------------------ | ---- | ---------- |
| No AI students remaining |      |            |

---

# Example 3 – Delete All Records

```sql
DELETE FROM Student;
```

After execution:

| StudentID        | Name | Age | Department | Email |
| ---------------- | ---- | --- | ---------- | ----- |
| No records found |      |     |            |       |

The table still exists and can accept new records.

---

# Internal Working

```text
User
   │
   ▼
DELETE Statement
   │
   ▼
DBMS Validates
(Table)
(WHERE Condition)
   │
   ▼
Matching Rows Found
   │
   ▼
Rows Deleted
```

---

# Importance of the WHERE Clause

## With WHERE

```sql
DELETE FROM Student
WHERE StudentID = 103;
```

Only the matching record is removed.

---

## Without WHERE

```sql
DELETE FROM Student;
```

Every record in the table is deleted.

> **Important:** The table itself remains available.

---

# DELETE vs DROP vs TRUNCATE (Overview)

| Feature                 | DELETE | TRUNCATE | DROP |
| ----------------------- | ------ | -------- | ---- |
| Removes rows            | ✅      | ✅        | ❌    |
| Removes table           | ❌      | ❌        | ✅    |
| WHERE clause supported  | ✅      | ❌        | ❌    |
| Table structure remains | ✅      | ✅        | ❌    |

> A detailed comparison is covered in the **Delete vs Drop vs Truncate** chapter.

---

# Common DELETE Scenarios

| Scenario                     | Example                                              |
| ---------------------------- | ---------------------------------------------------- |
| Remove a student             | `DELETE FROM Student WHERE StudentID = 101;`         |
| Delete an employee           | `DELETE FROM Employee WHERE EmployeeID = 25;`        |
| Remove discontinued products | `DELETE FROM Product WHERE Status = 'Discontinued';` |
| Delete inactive users        | `DELETE FROM Users WHERE Active = FALSE;`            |

---

# Database Compatibility

| Feature         | MySQL | PostgreSQL | SQL Server | SQLite |
| --------------- | :---: | :--------: | :--------: | :----: |
| DELETE          |   ✅   |      ✅     |      ✅     |    ✅   |
| WHERE Clause    |   ✅   |      ✅     |      ✅     |    ✅   |
| Delete All Rows |   ✅   |      ✅     |      ✅     |    ✅   |

---

# Real-World Applications

| Industry   | Example                          |
| ---------- | -------------------------------- |
| Banking    | Remove closed accounts           |
| Hospital   | Delete incorrect patient records |
| School     | Remove withdrawn students        |
| E-Commerce | Delete discontinued products     |
| HR System  | Remove resigned employees        |
| Library    | Delete outdated book records     |

---

# Advantages

* Removes only unwanted records.
* Supports deleting one or many rows.
* Preserves the table structure.
* Can target specific records using the `WHERE` clause.
* Supported by all major relational databases.

---

# Common Mistakes

* Forgetting the `WHERE` clause.
* Deleting the wrong records.
* Not checking data before deletion.
* Confusing `DELETE` with `DROP`.
* Deleting data without taking a backup.

---

# Best Practices

* Always execute a `SELECT` query before a `DELETE` query to verify the rows that will be removed.
* Always use a `WHERE` clause unless you intentionally want to remove all records.
* Back up important data before deleting records.
* Test deletion queries in a development environment first.
* Review the number of affected rows after execution.

---

# Interview Questions

### 1. What is the purpose of the `DELETE` statement?

**Answer:** It removes one or more records from a table while keeping the table structure unchanged.

---

### 2. What happens if the `WHERE` clause is omitted?

**Answer:** Every record in the table is deleted.

---

### 3. Does `DELETE` remove the table?

**Answer:** No. It removes only the data. The table structure remains.

---

### 4. Can multiple records be deleted in one query?

**Answer:** Yes.

```sql
DELETE FROM Student
WHERE Department = 'AI';
```

---

### 5. What is the difference between `DELETE` and `DROP`?

| DELETE            | DROP                     |
| ----------------- | ------------------------ |
| Removes data only | Removes the entire table |
| Table remains     | Table is deleted         |
| Can use `WHERE`   | No `WHERE` clause        |

---

# Practice Questions

## Easy

1. What is the purpose of the `DELETE` statement?
2. Write the syntax to delete a single record.
3. Why is the `WHERE` clause important?
4. Does `DELETE` remove the table?
5. Can all rows be deleted using `DELETE`?

---

## Medium

1. Delete a student whose `StudentID` is 105.
2. Delete all employees from the HR department.
3. Explain the importance of the `WHERE` clause.
4. Compare `DELETE` and `UPDATE`.
5. Explain how the database processes a `DELETE` statement.

---

## Hard

1. Explain the internal working of the `DELETE` statement.
2. Compare `DELETE`, `TRUNCATE`, and `DROP`.
3. Describe common mistakes made while using `DELETE` and how to avoid them.
4. Explain how `DELETE` behaves when foreign key constraints exist.
5. Discuss best practices for deleting large volumes of data in production databases.

---

# Key Takeaways

* `DELETE` removes records from a table.
* The table structure remains after deletion.
* The `WHERE` clause specifies which rows to remove.
* Omitting the `WHERE` clause deletes all rows.
* Always verify records before executing a `DELETE` statement.

---

# Conclusion

The `DELETE` statement is an essential SQL command for removing unwanted data while preserving the table structure. By using the `WHERE` clause carefully and following best practices, you can safely delete records without affecting unintended data. In the next chapter, you will learn how to **modify the structure of a table** using the **`ALTER TABLE`** statement.
