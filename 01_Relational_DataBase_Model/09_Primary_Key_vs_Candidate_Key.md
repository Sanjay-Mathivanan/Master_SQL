# Primary Key vs Candidate Key

# Introduction

Both **Primary Key** and **Candidate Key** are used to uniquely identify records in a table. Because they are closely related, beginners often confuse them.

The main difference is that a table can have **multiple Candidate Keys**, but **only one of them is selected as the Primary Key**.

Understanding this distinction is essential for designing efficient and well-structured relational databases.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand the difference between Primary Key and Candidate Key.
* Learn how a Primary Key is selected.
* Identify Candidate Keys in a table.
* Compare both keys using examples.
* Answer interview questions related to these concepts.

---

# Problem Statement

Consider the following **Employee** table.

| EmployeeID | Email                                             | PassportNumber | Name    |
| ---------- | ------------------------------------------------- | -------------- | ------- |
| E101       | [alice@company.com](mailto:alice@company.com)     | P123456        | Alice   |
| E102       | [bob@company.com](mailto:bob@company.com)         | P654321        | Bob     |
| E103       | [charlie@company.com](mailto:charlie@company.com) | P987654        | Charlie |

The following columns uniquely identify every employee:

* EmployeeID
* Email
* PassportNumber

These are all **Candidate Keys**.

Suppose the database designer chooses **EmployeeID** as the Primary Key.

Then:

* **Primary Key:** EmployeeID
* **Candidate Keys:** EmployeeID, Email, PassportNumber
* **Alternate Keys:** Email, PassportNumber

---

# Why Do We Need Both?

Candidate Keys help identify **all possible unique identifiers**.

The Primary Key is the **single Candidate Key selected** to identify records throughout the database.

This separation provides flexibility during database design.

---

# Definition

## Candidate Key

A **Candidate Key** is the **minimum set of one or more columns** that can uniquely identify each row in a table.

A table can have **multiple Candidate Keys**.

---

## Primary Key

A **Primary Key** is the **Candidate Key selected to uniquely identify every row** in a table.

A table can have **only one Primary Key**.

---

# Relationship

```text
All Candidate Keys
        │
        ▼
Choose One
        │
        ▼
Primary Key
        │
        ▼
Remaining Candidate Keys
        │
        ▼
Alternate Keys
```

---

# Example

## Student Table

| StudentID | Email                                             | RollNumber | Name    |
| --------- | ------------------------------------------------- | ---------- | ------- |
| 101       | [alice@college.edu](mailto:alice@college.edu)     | CS001      | Alice   |
| 102       | [bob@college.edu](mailto:bob@college.edu)         | CS002      | Bob     |
| 103       | [charlie@college.edu](mailto:charlie@college.edu) | CS003      | Charlie |

### Candidate Keys

* StudentID
* Email
* RollNumber

### Primary Key

* StudentID

### Alternate Keys

* Email
* RollNumber

---

# Comparison Table

| Feature                         | Primary Key                            | Candidate Key                                                           |
| ------------------------------- | -------------------------------------- | ----------------------------------------------------------------------- |
| Definition                      | Selected key used to identify each row | Minimal key that can uniquely identify each row                         |
| Number Allowed                  | Only one per table                     | One or more per table                                                   |
| Uniqueness                      | Must be unique                         | Must be unique                                                          |
| NULL Values                     | Not allowed                            | Generally not allowed because it must uniquely identify rows            |
| Selection                       | Chosen from Candidate Keys             | Identified during database design                                       |
| Purpose                         | Main identifier of the table           | Potential Primary Key                                                   |
| Relationship                    | Is a Candidate Key                     | May become the Primary Key                                              |
| Used for Foreign Key References | Yes                                    | Only if declared as a PRIMARY KEY or UNIQUE constraint (DBMS-dependent) |

---

# Selection Process

```text
Employee Table
      │
      ▼
Find All Candidate Keys
      │
      ▼
EmployeeID
Email
PassportNumber
      │
      ▼
Choose EmployeeID
      │
      ▼
Primary Key
      │
      ▼
Remaining Keys
      │
      ▼
Alternate Keys
```

---

# Real-World Example

## Banking System

### Customer Table

| CustomerID | AadhaarNumber | Email                             | CustomerName |
| ---------- | ------------- | --------------------------------- | ------------ |
| C101       | 123456789012  | [a@gmail.com](mailto:a@gmail.com) | Rahul        |
| C102       | 987654321098  | [b@gmail.com](mailto:b@gmail.com) | Priya        |

### Candidate Keys

* CustomerID
* AadhaarNumber
* Email

### Primary Key

* CustomerID

### Alternate Keys

* AadhaarNumber
* Email

---

# Advantages of Candidate Keys

* Provides multiple choices for selecting a Primary Key.
* Helps design flexible database schemas.
* Identifies all possible unique identifiers.

---

# Advantages of Primary Key

* Uniquely identifies every record.
* Prevents duplicate rows.
* Supports relationships between tables.
* Improves data integrity.

---

# Common Mistakes

* Thinking every Candidate Key is a Primary Key.
* Assuming a table can have multiple Primary Keys.
* Confusing Alternate Keys with Candidate Keys.
* Choosing a frequently changing column as the Primary Key.

---

# Best Practices

* Identify all Candidate Keys before selecting the Primary Key.
* Choose a stable and simple Candidate Key as the Primary Key.
* Avoid using long or frequently changing business values as the Primary Key.
* Apply `UNIQUE` constraints to remaining Candidate Keys when required.

---

# Interview Questions

### 1. What is the main difference between a Primary Key and a Candidate Key?

**Answer:** A Candidate Key is any minimal unique identifier, while a Primary Key is the Candidate Key chosen as the table's main identifier.

---

### 2. Can a table have multiple Candidate Keys?

**Answer:** Yes.

---

### 3. Can a table have multiple Primary Keys?

**Answer:** No.

---

### 4. Is every Primary Key a Candidate Key?

**Answer:** Yes.

---

### 5. Is every Candidate Key a Primary Key?

**Answer:** No. Only one Candidate Key is selected as the Primary Key.

---

# Practice Questions

## Easy

1. Define Candidate Key.
2. Define Primary Key.
3. How many Primary Keys can a table have?
4. Can a table have multiple Candidate Keys?
5. Is every Primary Key a Candidate Key?

## Medium

1. Differentiate Primary Key and Candidate Key.
2. Explain the relationship between Candidate Key and Alternate Key.
3. How is a Primary Key selected?
4. Explain with an Employee table example.
5. Why should a Primary Key be stable?

## Hard

1. Compare Primary Key, Candidate Key, and Alternate Key with examples.
2. Design Candidate Keys and Primary Keys for a Library Management System.
3. Explain why identifying Candidate Keys is important before creating a Primary Key.
4. Discuss the impact of choosing an inappropriate Primary Key.
5. Design keys for an Online Shopping database.

---

# Key Takeaways

* Every Primary Key is a Candidate Key.
* Every Candidate Key is **not** a Primary Key.
* A table can have multiple Candidate Keys.
* A table can have only one Primary Key.
* The Primary Key is selected from the available Candidate Keys.

---

# Conclusion

Candidate Keys represent all possible minimal unique identifiers in a table, while the Primary Key is the one chosen to serve as the main identifier. Understanding the relationship between these two concepts is fundamental for designing efficient, scalable, and reliable relational databases.
