# Candidate Key

# Introduction

In the previous chapter, you learned about different types of keys used in a relational database. One of the most important among them is the **Candidate Key**.

A Candidate Key is the best possible choice for uniquely identifying each record because it contains **only the minimum required columns**. Every Primary Key is selected from the available Candidate Keys.

Understanding Candidate Keys is essential for designing efficient and well-structured databases.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand what a Candidate Key is.
* Learn why Candidate Keys are important.
* Identify Candidate Keys in a table.
* Differentiate Candidate Key from Super Key and Primary Key.
* Solve interview questions related to Candidate Keys.

---

# Problem Statement

Consider the following **Student** table.

| StudentID | Email                                         | Phone      | Name    |
| --------- | --------------------------------------------- | ---------- | ------- |
| 101       | [alice@gmail.com](mailto:alice@gmail.com)     | 9876543210 | Alice   |
| 102       | [bob@gmail.com](mailto:bob@gmail.com)         | 9876543211 | Bob     |
| 103       | [charlie@gmail.com](mailto:charlie@gmail.com) | 9876543212 | Charlie |

Each student must be uniquely identified.

Possible unique columns are:

* StudentID
* Email
* Phone

Which one should be chosen?

The answer is that **all of them are Candidate Keys** because each can uniquely identify a student.

---

# Why Do We Need Candidate Keys?

Without Candidate Keys:

* Multiple columns may unnecessarily be used to identify a row.
* Database design becomes inefficient.
* Selecting the best Primary Key becomes difficult.
* Data redundancy may increase.

Candidate Keys help us choose the most suitable Primary Key.

---

# Definition

A **Candidate Key** is the **minimum set of one or more columns** that can uniquely identify every record in a table.

It satisfies two important conditions:

* Every value must be unique.
* No unnecessary column should be included.

---

# Characteristics of Candidate Key

* Uniquely identifies every row.
* Cannot contain duplicate values.
* Should not contain unnecessary columns.
* Can consist of one or more columns.
* A table can have multiple Candidate Keys.
* One Candidate Key is selected as the Primary Key.

---

# Example 1

## Student Table

| StudentID | Email                                         | Phone      | Name    |
| --------- | --------------------------------------------- | ---------- | ------- |
| 101       | [alice@gmail.com](mailto:alice@gmail.com)     | 9876543210 | Alice   |
| 102       | [bob@gmail.com](mailto:bob@gmail.com)         | 9876543211 | Bob     |
| 103       | [charlie@gmail.com](mailto:charlie@gmail.com) | 9876543212 | Charlie |

### Candidate Keys

* StudentID
* Email
* Phone

Any one of these can uniquely identify a student.

---

# Example 2

## Employee Table

| EmployeeID | PassportNumber | Email                                         | Name  |
| ---------- | -------------- | --------------------------------------------- | ----- |
| E101       | P123456        | [alice@company.com](mailto:alice@company.com) | Alice |
| E102       | P654321        | [bob@company.com](mailto:bob@company.com)     | Bob   |

Candidate Keys:

* EmployeeID
* PassportNumber
* Email

The database designer can choose any one as the Primary Key.

---

# Candidate Key Selection

```text
All Unique Columns
        │
        ▼
Candidate Keys
        │
        ▼
Choose One
        │
        ▼
Primary Key
```

---

# Candidate Key vs Super Key

| Candidate Key             | Super Key                          |
| ------------------------- | ---------------------------------- |
| Minimum unique columns    | May contain extra columns          |
| No unnecessary attributes | May include unnecessary attributes |
| Can become Primary Key    | Cannot always become Primary Key   |
| Minimal                   | Not necessarily minimal            |

---

# Candidate Key vs Primary Key

| Candidate Key                      | Primary Key                     |
| ---------------------------------- | ------------------------------- |
| Many can exist                     | Only one per table              |
| All are potential Primary Keys     | Selected from Candidate Keys    |
| Must be unique                     | Must be unique                  |
| Cannot contain unnecessary columns | Also cannot contain NULL values |

---

# How to Identify a Candidate Key

Follow these steps:

1. Identify columns that contain unique values.
2. Check whether they uniquely identify every row.
3. Remove unnecessary columns.
4. The remaining minimal unique columns are Candidate Keys.

---

# Real-World Example

### Employee Management System

| Column          | Candidate Key? |
| --------------- | -------------- |
| EmployeeID      | ✅ Yes          |
| Company Email   | ✅ Yes          |
| Passport Number | ✅ Yes          |
| Department      | ❌ No           |
| Salary          | ❌ No           |

The company may choose **EmployeeID** as the Primary Key, while the remaining Candidate Keys become Alternate Keys.

---

# Advantages

* Helps select the best Primary Key.
* Ensures uniqueness of records.
* Improves database design.
* Reduces redundancy.
* Supports data integrity.

---

# Limitations

* Some Candidate Keys may contain business data that can change.
* Multiple Candidate Keys can make key selection more challenging.
* Choosing the wrong Candidate Key may affect database maintenance.

---

# Common Mistakes

* Confusing Candidate Key with Primary Key.
* Assuming a table has only one Candidate Key.
* Including unnecessary columns.
* Choosing a frequently changing column as a Primary Key.

---

# Best Practices

* Keep Candidate Keys as small as possible.
* Prefer stable columns.
* Avoid attributes that change frequently.
* Select a simple Candidate Key as the Primary Key.
* Document all Candidate Keys during database design.

---

# Interview Questions

### 1. What is a Candidate Key?

**Answer:** A Candidate Key is the minimum set of columns that uniquely identifies each row in a table.

---

### 2. Can a table have multiple Candidate Keys?

**Answer:** Yes. A table can have multiple Candidate Keys.

---

### 3. How many Primary Keys can a table have?

**Answer:** Only one Primary Key, selected from the available Candidate Keys.

---

### 4. Can a Candidate Key contain unnecessary columns?

**Answer:** No. It must be minimal.

---

### 5. Is every Candidate Key a Super Key?

**Answer:** Yes. Every Candidate Key is a Super Key, but not every Super Key is a Candidate Key.

---

# Practice Questions

## Easy

1. Define Candidate Key.
2. Can a table have more than one Candidate Key?
3. Is every Primary Key a Candidate Key?
4. What are the characteristics of a Candidate Key?
5. Give two examples of Candidate Keys.

## Medium

1. Differentiate Candidate Key and Super Key.
2. Explain Candidate Key with a Student table.
3. How is a Primary Key selected?
4. Why should unnecessary columns be avoided?
5. Explain Candidate Keys in an Employee database.

## Hard

1. Identify Candidate Keys in a Hospital Management System.
2. Compare Candidate Key, Primary Key, and Alternate Key.
3. Design Candidate Keys for an Online Shopping database.
4. Explain why Candidate Keys are important in normalization.
5. Discuss the role of Candidate Keys in maintaining data integrity.

---

# Key Takeaways

* A Candidate Key is the minimum unique identifier of a row.
* A table may contain multiple Candidate Keys.
* One Candidate Key is selected as the Primary Key.
* Every Candidate Key is a Super Key.
* Candidate Keys play a crucial role in designing efficient relational databases.

---

# Conclusion

A Candidate Key is one of the core concepts in relational database design. It provides the foundation for selecting the Primary Key and ensures that every record can be uniquely identified using the smallest possible set of columns. Mastering Candidate Keys will help you build efficient databases and answer common SQL and DBMS interview questions with confidence.
