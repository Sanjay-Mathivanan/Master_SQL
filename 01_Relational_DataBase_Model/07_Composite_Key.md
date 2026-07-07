# Composite Key

# Introduction

In the previous chapters, you learned about **Primary Keys** and **Alternate Keys**. In many real-world databases, a single column is not enough to uniquely identify a record. In such situations, we combine two or more columns to create a **Composite Key**.

A Composite Key ensures that the combination of multiple columns uniquely identifies each row in a table.

It is commonly used in **junction tables**, **many-to-many relationships**, and **transaction tables**.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand what a Composite Key is.
* Learn why Composite Keys are required.
* Create Composite Keys using SQL.
* Identify situations where Composite Keys should be used.
* Differentiate Composite Keys from Primary Keys.

---

# Problem Statement

Consider an **Attendance** table.

| StudentID | SubjectID | Attendance |
| --------- | --------- | ---------- |
| 101       | CS101     | Present    |
| 101       | CS102     | Absent     |
| 102       | CS101     | Present    |

Here,

* **StudentID** is repeated.
* **SubjectID** is repeated.

Neither column can uniquely identify a record.

However, the combination:

* StudentID + SubjectID

uniquely identifies each attendance record.

---

# Why Do We Need a Composite Key?

Without a Composite Key:

* Duplicate records may exist.
* Individual columns may not uniquely identify rows.
* Data integrity may be compromised.
* Many-to-many relationships become difficult to manage.

A Composite Key solves these problems by combining multiple columns into one unique identifier.

---

# Definition

A **Composite Key** is a **Primary Key made up of two or more columns** that together uniquely identify a row in a table.

Each individual column may contain duplicate values, but their combination must always be unique.

---

# Characteristics of Composite Key

* Consists of two or more columns.
* Uniquely identifies every record.
* Prevents duplicate combinations.
* Can be used as a Primary Key.
* Commonly used in relationship tables.

---

# SQL Syntax

## Creating a Composite Primary Key

```sql
CREATE TABLE Attendance (
    StudentID INT,
    SubjectID VARCHAR(10),
    Attendance VARCHAR(20),
    PRIMARY KEY (StudentID, SubjectID)
);
```

---

# Example 1

## Attendance Table

| StudentID | SubjectID | Attendance |
| --------- | --------- | ---------- |
| 101       | CS101     | Present    |
| 101       | CS102     | Absent     |
| 102       | CS101     | Present    |
| 103       | CS103     | Present    |

### Composite Key

* StudentID
* SubjectID

Together they uniquely identify each record.

---

# Example 2

## OrderDetails Table

| OrderID | ProductID | Quantity |
| ------- | --------- | -------- |
| 1001    | P101      | 2        |
| 1001    | P102      | 1        |
| 1002    | P101      | 3        |

Neither **OrderID** nor **ProductID** alone is unique.

The combination:

* OrderID
* ProductID

forms the Composite Key.

---

# Internal Working

```text
Insert New Record
        │
        ▼
Check Combination
(StudentID, SubjectID)
        │
        ├── Exists?
        │      │
        │      ├── Yes → Reject Record
        │      │
        │      └── No
        ▼
Insert Record
```

---

# Real-World Examples

| Application               | Composite Key         |
| ------------------------- | --------------------- |
| Student Attendance System | StudentID + SubjectID |
| Online Shopping           | OrderID + ProductID   |
| Library Management        | MemberID + BookID     |
| Hospital Management       | PatientID + DoctorID  |
| Movie Ticket Booking      | ShowID + SeatNumber   |

---

# Composite Key vs Primary Key

| Composite Key                        | Primary Key                 |
| ------------------------------------ | --------------------------- |
| Uses two or more columns             | May use one or more columns |
| Used when one column is insufficient | Main identifier of a table  |
| Combination must be unique           | Must always be unique       |
| Is a type of Primary Key             | General concept             |

---

# Composite Key vs Candidate Key

| Composite Key                             | Candidate Key                   |
| ----------------------------------------- | ------------------------------- |
| Can contain multiple columns              | May contain one or more columns |
| Often selected as the Primary Key         | Potential Primary Key           |
| Used when combined uniqueness is required | Minimal unique identifier       |

---

# Advantages

* Uniquely identifies records when one column is insufficient.
* Eliminates duplicate combinations.
* Represents real-world relationships naturally.
* Maintains data integrity.
* Reduces the need for artificial identifiers in some cases.

---

# Limitations

* Queries become longer because multiple columns are used.
* Indexes may consume more storage.
* Foreign Key relationships become more complex.
* Updating key values is more difficult.

---

# Common Mistakes

* Assuming each column in a Composite Key must be unique individually.
* Using unnecessary columns in the key.
* Creating Composite Keys with too many columns.
* Forgetting that the combination—not the individual columns—must be unique.

---

# Best Practices

* Use Composite Keys only when necessary.
* Keep the number of key columns as small as possible.
* Choose stable columns that rarely change.
* Consider using a Surrogate Key if the Composite Key becomes too large.
* Document Composite Keys clearly during database design.

---

# Interview Questions

### 1. What is a Composite Key?

**Answer:** A Composite Key is a Primary Key made up of two or more columns that together uniquely identify a row.

---

### 2. Why do we use a Composite Key?

**Answer:** When a single column cannot uniquely identify a record, multiple columns are combined to create a unique identifier.

---

### 3. Can a Composite Key contain duplicate values in individual columns?

**Answer:** Yes. Individual columns may contain duplicates, but the combination of all key columns must be unique.

---

### 4. Is a Composite Key a Primary Key?

**Answer:** Yes. It is a type of Primary Key that consists of multiple columns.

---

### 5. Where are Composite Keys commonly used?

**Answer:** They are commonly used in many-to-many relationship tables, transaction tables, and junction tables.

---

# Practice Questions

## Easy

1. Define a Composite Key.
2. How many columns can a Composite Key contain?
3. Can a Composite Key contain duplicate values in one column?
4. Write the SQL syntax for creating a Composite Key.
5. Give two real-world examples of Composite Keys.

## Medium

1. Explain Composite Key using an Attendance table.
2. Differentiate Composite Key and Primary Key.
3. Why are Composite Keys used in junction tables?
4. Explain Composite Key with an OrderDetails table.
5. What are the advantages of Composite Keys?

## Hard

1. Design Composite Keys for a Hospital Management System.
2. Compare Composite Key, Candidate Key, and Primary Key.
3. Explain the impact of Composite Keys on indexing.
4. Design Composite Keys for an Online Shopping database.
5. Discuss when a Surrogate Key should be preferred over a Composite Key.

---

# Key Takeaways

* A Composite Key consists of two or more columns.
* The combination of all columns must uniquely identify each record.
* Composite Keys are widely used in many-to-many relationships.
* They help maintain data integrity when a single column is insufficient.
* A Composite Key is a type of Primary Key.

---

# Conclusion

A Composite Key is an essential concept in relational database design, especially when multiple columns are required to uniquely identify a record. Understanding when and how to use Composite Keys helps create efficient, normalized, and reliable database structures for real-world applications.
