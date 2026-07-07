# Primary Key

# Introduction

In the previous chapters, you learned about **Super Keys** and **Candidate Keys**. A **Primary Key** is selected from the available Candidate Keys and is used as the **main identifier** for every record in a table.

A well-designed Primary Key ensures that each row is unique, prevents duplicate records, and helps establish relationships between tables.

Almost every relational database table should have a Primary Key.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand what a Primary Key is.
* Learn why a Primary Key is important.
* Create a Primary Key in SQL.
* Differentiate Primary Key from Candidate Key and Unique Key.
* Answer interview questions related to Primary Keys.

---

# Problem Statement

Consider the following **Student** table.

| StudentID | Name    | Department |
| --------- | ------- | ---------- |
| 101       | Alice   | CSE        |
| 102       | Bob     | ECE        |
| 101       | Charlie | IT         |

The **StudentID** is duplicated, making it impossible to uniquely identify each student.

To solve this problem, we declare **StudentID** as the **Primary Key**, ensuring that every student has a unique ID.

---

# Why Do We Need a Primary Key?

Without a Primary Key:

* Duplicate records may exist.
* Records cannot be uniquely identified.
* Relationships between tables become unreliable.
* Data integrity cannot be guaranteed.
* Updating or deleting records becomes difficult.

A Primary Key ensures that every row has a unique identity.

---

# Definition

A **Primary Key** is a column or a combination of columns that **uniquely identifies every row in a table**.

It is selected from the available **Candidate Keys**.

---

# Characteristics of a Primary Key

* Uniquely identifies every row.
* Cannot contain duplicate values.
* Cannot contain NULL values.
* Only one Primary Key is allowed per table.
* Can consist of one or more columns (Composite Primary Key).
* Used to establish relationships with other tables.

---

# SQL Syntax

## Creating a Primary Key During Table Creation

```sql
CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(100),
    Department VARCHAR(50)
);
```

---

## Adding a Primary Key to an Existing Table

```sql
ALTER TABLE Student
ADD CONSTRAINT PK_Student
PRIMARY KEY (StudentID);
```

---

# Example 1

## Student Table

| StudentID | Name    | Department |
| --------- | ------- | ---------- |
| 101       | Alice   | CSE        |
| 102       | Bob     | ECE        |
| 103       | Charlie | IT         |

Here,

**StudentID** is the Primary Key because it uniquely identifies every student.

---

# Example 2

## Employee Table

| EmployeeID | Name  | Email                                         |
| ---------- | ----- | --------------------------------------------- |
| E101       | Alice | [alice@company.com](mailto:alice@company.com) |
| E102       | Bob   | [bob@company.com](mailto:bob@company.com)     |

**EmployeeID** is the Primary Key.

---

# Composite Primary Key

Sometimes, a single column is not enough to uniquely identify a record.

In such cases, two or more columns together form a **Composite Primary Key**.

## Example

### Attendance Table

| StudentID | SubjectID | Attendance |
| --------- | --------- | ---------- |
| 101       | CS101     | Present    |
| 101       | CS102     | Absent     |
| 102       | CS101     | Present    |

Neither **StudentID** nor **SubjectID** alone is unique.

The combination:

* StudentID
* SubjectID

forms the Composite Primary Key.

### SQL Example

```sql
CREATE TABLE Attendance (
    StudentID INT,
    SubjectID VARCHAR(10),
    Attendance VARCHAR(20),
    PRIMARY KEY (StudentID, SubjectID)
);
```

---

# Internal Working

```text
New Record
     │
     ▼
Check Primary Key Value
     │
     ├── Already Exists?
     │       │
     │       ├── Yes → Reject Record
     │       │
     │       └── No
     │
     ▼
Insert Record
```

---

# Primary Key vs Candidate Key

| Primary Key                  | Candidate Key                  |
| ---------------------------- | ------------------------------ |
| Only one per table           | Multiple can exist             |
| Selected from Candidate Keys | All are potential Primary Keys |
| Cannot contain NULL values   | Must uniquely identify rows    |
| Main identifier              | Possible identifiers           |

---

# Primary Key vs Unique Key

| Primary Key                 | Unique Key                                   |
| --------------------------- | -------------------------------------------- |
| Only one per table          | Multiple Unique Keys allowed                 |
| NULL values are not allowed | NULL values may be allowed (depends on DBMS) |
| Used as the main identifier | Used to enforce uniqueness                   |
| Referenced by Foreign Keys  | Usually not referenced                       |

---

# Real-World Example

## Banking System

### Customer Table

| CustomerID | CustomerName | Phone      |
| ---------- | ------------ | ---------- |
| C101       | Rahul        | 9876543210 |
| C102       | Priya        | 9876543211 |

### Account Table

| AccountNumber | CustomerID | Balance |
| ------------- | ---------- | ------- |
| A1001         | C101       | 50000   |
| A1002         | C102       | 75000   |

Here,

* **CustomerID** is the Primary Key in the **Customer** table.
* **CustomerID** becomes a Foreign Key in the **Account** table.

---

# Advantages

* Prevents duplicate records.
* Ensures data integrity.
* Simplifies record retrieval.
* Enables relationships between tables.
* Improves query performance through indexing (implementation depends on the DBMS).

---

# Limitations

* Only one Primary Key is allowed per table.
* Changing Primary Key values can affect related tables.
* Poor Primary Key selection can make database maintenance difficult.

---

# Common Mistakes

* Using duplicate values.
* Allowing NULL values.
* Choosing a column whose value changes frequently.
* Confusing Primary Key with Unique Key.
* Creating unnecessarily large Composite Primary Keys.

---

# Best Practices

* Choose a stable column as the Primary Key.
* Keep the Primary Key as small as possible.
* Avoid using business data that changes frequently.
* Use integer-based Surrogate Keys when appropriate.
* Define the Primary Key during table creation whenever possible.

---

# Interview Questions

### 1. What is a Primary Key?

**Answer:** A Primary Key is a column or combination of columns that uniquely identifies every row in a table.

---

### 2. Can a table have multiple Primary Keys?

**Answer:** No. A table can have only one Primary Key.

---

### 3. Can a Primary Key contain NULL values?

**Answer:** No.

---

### 4. Can a Primary Key consist of multiple columns?

**Answer:** Yes. It is called a Composite Primary Key.

---

### 5. Is every Primary Key a Candidate Key?

**Answer:** Yes. A Primary Key is selected from the available Candidate Keys.

---

# Practice Questions

## Easy

1. Define a Primary Key.
2. Can a Primary Key contain NULL values?
3. How many Primary Keys can a table have?
4. What is a Composite Primary Key?
5. Why is a Primary Key important?

## Medium

1. Differentiate Primary Key and Candidate Key.
2. Compare Primary Key and Unique Key.
3. Explain Composite Primary Key with an example.
4. Why should a Primary Key be stable?
5. Write SQL to create a Primary Key.

## Hard

1. Design Primary Keys for a Hospital Management System.
2. Explain how Primary Keys maintain data integrity.
3. Compare Super Key, Candidate Key, and Primary Key.
4. Discuss the advantages of using Surrogate Keys as Primary Keys.
5. Design a Composite Primary Key for a College ERP database.

---

# Key Takeaways

* A Primary Key uniquely identifies every row in a table.
* It is selected from the available Candidate Keys.
* A table can have only one Primary Key.
* Primary Keys cannot contain NULL or duplicate values.
* Primary Keys are essential for maintaining relationships and ensuring data integrity.

---

# Conclusion

The Primary Key is the foundation of every relational database table. It guarantees uniqueness, supports relationships between tables, and ensures reliable data management. Choosing an appropriate Primary Key is one of the most important steps in designing a robust and scalable database.
