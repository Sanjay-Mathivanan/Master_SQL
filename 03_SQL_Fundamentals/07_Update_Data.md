# Update Data

# Introduction

Data stored in a database is not always permanent. Employee salaries increase, student addresses change, product prices are updated, and customer contact details need correction.

The **`UPDATE`** statement is used to modify existing records in a table without deleting and recreating them.

In this chapter, you will learn how to update one or more records, update multiple columns, use the `WHERE` clause effectively, and avoid common mistakes.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand the purpose of the `UPDATE` statement.
* Update a single record.
* Update multiple records.
* Update multiple columns.
* Understand the importance of the `WHERE` clause.
* Follow best practices while updating data.

---

# Problem Statement

Suppose the **Student** table contains the following records.

| StudentID | Name  | Age | Department | Email                                         |
| --------- | ----- | --- | ---------- | --------------------------------------------- |
| 101       | Rahul | 20  | CSE        | [rahul@example.com](mailto:rahul@example.com) |
| 102       | Priya | 19  | AI         | [priya@example.com](mailto:priya@example.com) |
| 103       | Arun  | 21  | ECE        | [arun@example.com](mailto:arun@example.com)   |
| 104       | Sneha | 20  | IT         | [sneha@example.com](mailto:sneha@example.com) |

Now assume Rahul has moved from the **CSE** department to the **AI** department.

How can we update this information without deleting and inserting the record again?

The answer is the **`UPDATE`** statement.

---

# Why Do We Need UPDATE?

The `UPDATE` statement is used to:

* Correct incorrect information.
* Modify existing records.
* Update prices and salaries.
* Change addresses and contact details.
* Maintain accurate and up-to-date data.

Without `UPDATE`, modifying existing information would be difficult and inefficient.

---

# What is UPDATE?

The **`UPDATE`** statement modifies one or more existing rows in a table.

Unlike `INSERT`, which adds new records, `UPDATE` changes the values of records that already exist.

---

# Syntax

## Update a Single Column

```sql
UPDATE table_name
SET column_name = value
WHERE condition;
```

---

## Update Multiple Columns

```sql
UPDATE table_name
SET column1 = value1,
    column2 = value2
WHERE condition;
```

---

# Example 1 – Update a Single Record

```sql
UPDATE Student
SET Department = 'AI'
WHERE StudentID = 101;
```

### Before Update

| StudentID | Name  | Department |
| --------- | ----- | ---------- |
| 101       | Rahul | CSE        |

### After Update

| StudentID | Name  | Department |
| --------- | ----- | ---------- |
| 101       | Rahul | AI         |

---

# Example 2 – Update Multiple Columns

```sql
UPDATE Student
SET Age = 21,
    Email = 'rahul.kumar@example.com'
WHERE StudentID = 101;
```

### Result

| StudentID | Age | Email                                                     |
| --------- | --: | --------------------------------------------------------- |
| 101       |  21 | [rahul.kumar@example.com](mailto:rahul.kumar@example.com) |

---

# Example 3 – Update Multiple Records

```sql
UPDATE Student
SET Department = 'Computer Science'
WHERE Department = 'CSE';
```

### Before Update

| StudentID | Department |
| --------- | ---------- |
| 101       | CSE        |
| 105       | CSE        |

### After Update

| StudentID | Department       |
| --------- | ---------------- |
| 101       | Computer Science |
| 105       | Computer Science |

---

# Example 4 – Update All Records

```sql
UPDATE Student
SET Age = 20;
```

> **Warning:** This updates **every row** in the table because no `WHERE` clause is specified.

---

# Internal Working

```text
User
   │
   ▼
UPDATE Statement
   │
   ▼
DBMS Validates
(Table)
(Columns)
(WHERE Condition)
   │
   ▼
Matching Rows Found
   │
   ▼
Data Updated
```

---

# Importance of the WHERE Clause

The `WHERE` clause specifies which records should be updated.

### With WHERE

```sql
UPDATE Student
SET Department = 'AI'
WHERE StudentID = 101;
```

Only one record is updated.

---

### Without WHERE

```sql
UPDATE Student
SET Department = 'AI';
```

All records in the table are updated.

---

# Common UPDATE Scenarios

| Scenario                  | Example                                                            |
| ------------------------- | ------------------------------------------------------------------ |
| Change student department | `UPDATE Student SET Department='AI' WHERE StudentID=101;`          |
| Increase employee salary  | `UPDATE Employee SET Salary=60000 WHERE EmployeeID=5;`             |
| Correct customer email    | `UPDATE Customer SET Email='new@example.com' WHERE CustomerID=12;` |
| Update product price      | `UPDATE Product SET Price=499.99 WHERE ProductID=20;`              |

---

# Database Compatibility

| Feature                | MySQL | PostgreSQL | SQL Server | SQLite |
| ---------------------- | :---: | :--------: | :--------: | :----: |
| UPDATE                 |   ✅   |      ✅     |      ✅     |    ✅   |
| Multiple Column Update |   ✅   |      ✅     |      ✅     |    ✅   |
| WHERE Clause           |   ✅   |      ✅     |      ✅     |    ✅   |

---

# Real-World Applications

| Industry   | Example                    |
| ---------- | -------------------------- |
| Banking    | Update account details     |
| Hospital   | Update patient information |
| School     | Update student marks       |
| E-Commerce | Update product prices      |
| HR System  | Update employee salary     |
| Logistics  | Update shipment status     |

---

# Advantages

* Modifies existing data efficiently.
* Supports updating one or multiple columns.
* Can update one or many rows.
* Works with all major relational databases.
* Preserves existing records.

---

# Common Mistakes

* Forgetting the `WHERE` clause.
* Updating the wrong column.
* Using an incorrect condition.
* Assigning incompatible data types.
* Not verifying data before updating.

---

# Best Practices

* Always execute a `SELECT` query first to verify the rows that will be updated.
* Always use a `WHERE` clause unless every row should be modified.
* Test updates on sample data before running them in production.
* Back up important data before performing large updates.
* Keep SQL queries properly formatted and readable.

---

# Interview Questions

### 1. What is the purpose of the `UPDATE` statement?

**Answer:** It is used to modify existing records in a table.

---

### 2. Which clause is commonly used with `UPDATE`?

**Answer:** The `WHERE` clause.

---

### 3. What happens if `WHERE` is omitted?

**Answer:** Every record in the table is updated.

---

### 4. Can multiple columns be updated in one statement?

**Answer:** Yes.

```sql
UPDATE Student
SET Age = 21,
    Department = 'AI'
WHERE StudentID = 101;
```

---

### 5. What is the difference between `INSERT` and `UPDATE`?

| INSERT            | UPDATE                    |
| ----------------- | ------------------------- |
| Adds new records  | Modifies existing records |
| Creates new rows  | Changes existing rows     |
| Used for new data | Used for existing data    |

---

# Practice Questions

## Easy

1. What is the purpose of the `UPDATE` statement?
2. Write the syntax for updating one column.
3. Why is the `WHERE` clause important?
4. Can multiple columns be updated in one query?
5. What happens if the `WHERE` clause is omitted?

---

## Medium

1. Update the department of a student.
2. Update the salary of an employee.
3. Update two columns in a single query.
4. Explain how the database processes an `UPDATE` statement.
5. Compare `INSERT` and `UPDATE`.

---

## Hard

1. Explain the internal working of the `UPDATE` statement.
2. Compare `UPDATE` behaviour across MySQL, PostgreSQL, SQL Server, and SQLite.
3. Describe common mistakes made while using `UPDATE` and how to avoid them.
4. Explain why the `WHERE` clause is critical in production databases.
5. Discuss best practices for updating large volumes of data.

---

# Key Takeaways

* `UPDATE` is used to modify existing records.
* The `WHERE` clause determines which rows are updated.
* Omitting the `WHERE` clause updates every row in the table.
* Multiple columns can be updated in a single statement.
* Verify records before updating to avoid accidental changes.

---

# Conclusion

The `UPDATE` statement is an essential SQL command for maintaining accurate and current information in a database. By using the `WHERE` clause carefully and following best practices, you can safely modify records without affecting unintended data. In the next chapter, you will learn how to **remove records** from a table using the **`DELETE`** statement.
