# Alternate Key

# Introduction

In the previous chapter, you learned that a table can have multiple **Candidate Keys**, but only one of them is chosen as the **Primary Key**.

The remaining Candidate Keys that are **not selected as the Primary Key** are called **Alternate Keys**.

Alternate Keys are still unique and can identify each record, but they are not used as the table's main identifier.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand what an Alternate Key is.
* Learn why Alternate Keys are used.
* Differentiate Alternate Key from Candidate Key and Primary Key.
* Identify Alternate Keys in a table.
* Answer interview questions related to Alternate Keys.

---

# Problem Statement

Consider the following **Employee** table.

| EmployeeID | Email                                             | PassportNumber | Name    |
| ---------- | ------------------------------------------------- | -------------- | ------- |
| E101       | [alice@company.com](mailto:alice@company.com)     | P123456        | Alice   |
| E102       | [bob@company.com](mailto:bob@company.com)         | P654321        | Bob     |
| E103       | [charlie@company.com](mailto:charlie@company.com) | P987654        | Charlie |

The following columns uniquely identify each employee:

* EmployeeID
* Email
* PassportNumber

Since only one Primary Key can exist, suppose **EmployeeID** is selected as the Primary Key.

The remaining unique columns become **Alternate Keys**.

---

# Why Do We Need Alternate Keys?

Without Alternate Keys:

* Other unique columns may contain duplicate values.
* Important business identifiers may lose uniqueness.
* Data integrity may be affected.

Alternate Keys ensure that all other unique attributes remain unique, even though they are not the Primary Key.

---

# Definition

An **Alternate Key** is a **Candidate Key that is not selected as the Primary Key**.

It can uniquely identify every row but is not used as the main identifier for the table.

---

# Characteristics of Alternate Key

* Uniquely identifies each record.
* Derived from Candidate Keys.
* Cannot contain duplicate values.
* Usually implemented using a **UNIQUE** constraint.
* A table can have multiple Alternate Keys.

---

# Example

## Employee Table

| EmployeeID | Email                                             | PassportNumber | Name    |
| ---------- | ------------------------------------------------- | -------------- | ------- |
| E101       | [alice@company.com](mailto:alice@company.com)     | P123456        | Alice   |
| E102       | [bob@company.com](mailto:bob@company.com)         | P654321        | Bob     |
| E103       | [charlie@company.com](mailto:charlie@company.com) | P987654        | Charlie |

### Candidate Keys

* EmployeeID
* Email
* PassportNumber

### Primary Key

* EmployeeID

### Alternate Keys

* Email
* PassportNumber

---

# SQL Syntax

## Creating an Alternate Key Using UNIQUE Constraint

```sql
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY,
    Email VARCHAR(100) UNIQUE,
    PassportNumber VARCHAR(20) UNIQUE,
    Name VARCHAR(100)
);
```

In this example:

* **EmployeeID** → Primary Key
* **Email** → Alternate Key
* **PassportNumber** → Alternate Key

---

# Internal Working

```text
Candidate Keys
      │
      ▼
Choose One
      │
      ▼
Primary Key
      │
Remaining Candidate Keys
      │
      ▼
Alternate Keys
```

---

# Alternate Key vs Candidate Key

| Alternate Key                           | Candidate Key                           |
| --------------------------------------- | --------------------------------------- |
| Candidate Key not chosen as Primary Key | Minimal unique identifier               |
| Cannot be the current Primary Key       | Can become the Primary Key              |
| Usually enforced using UNIQUE           | Used to determine possible Primary Keys |

---

# Alternate Key vs Primary Key

| Alternate Key                  | Primary Key                       |
| ------------------------------ | --------------------------------- |
| Multiple can exist             | Only one per table                |
| Not the main identifier        | Main identifier of the table      |
| Enforced using UNIQUE          | Enforced using PRIMARY KEY        |
| Used for additional uniqueness | Used to uniquely identify records |

---

# Real-World Example

## University Database

### Student Table

| StudentID | Email                                         | RollNumber | Name  |
| --------- | --------------------------------------------- | ---------- | ----- |
| 101       | [alice@college.edu](mailto:alice@college.edu) | 23CS001    | Alice |
| 102       | [bob@college.edu](mailto:bob@college.edu)     | 23CS002    | Bob   |

Here,

* **StudentID** → Primary Key
* **Email** → Alternate Key
* **RollNumber** → Alternate Key

Even though **Email** and **RollNumber** are not the Primary Key, they must remain unique.

---

# Advantages

* Maintains uniqueness of important columns.
* Prevents duplicate business data.
* Provides flexibility in database design.
* Supports data integrity.
* Helps identify records using multiple unique attributes.

---

# Limitations

* Cannot replace the Primary Key as the table's main identifier.
* Additional UNIQUE constraints may slightly increase storage and maintenance overhead.
* Selecting too many Alternate Keys can complicate database design.

---

# Common Mistakes

* Confusing Alternate Key with Candidate Key.
* Assuming Alternate Keys allow duplicate values.
* Forgetting to apply the UNIQUE constraint.
* Treating every unique column as an Alternate Key without first identifying Candidate Keys.

---

# Best Practices

* Choose a stable Candidate Key as the Primary Key.
* Apply UNIQUE constraints to Alternate Keys.
* Avoid using frequently changing columns as Alternate Keys.
* Clearly document Alternate Keys during database design.

---

# Interview Questions

### 1. What is an Alternate Key?

**Answer:** An Alternate Key is a Candidate Key that is not selected as the Primary Key.

---

### 2. Can a table have multiple Alternate Keys?

**Answer:** Yes. A table can have multiple Alternate Keys.

---

### 3. How is an Alternate Key implemented in SQL?

**Answer:** It is typically implemented using the **UNIQUE** constraint.

---

### 4. Can an Alternate Key uniquely identify a row?

**Answer:** Yes. Like a Candidate Key, it uniquely identifies each record.

---

### 5. What is the difference between a Primary Key and an Alternate Key?

**Answer:** A Primary Key is the selected Candidate Key used as the main identifier, while an Alternate Key is any remaining Candidate Key that is not selected.

---

# Practice Questions

## Easy

1. Define an Alternate Key.
2. How is an Alternate Key created in SQL?
3. Can a table have more than one Alternate Key?
4. Is every Alternate Key a Candidate Key?
5. Give two examples of Alternate Keys.

## Medium

1. Differentiate Alternate Key and Primary Key.
2. Explain Alternate Key with an Employee table.
3. Why are UNIQUE constraints used for Alternate Keys?
4. Compare Candidate Key and Alternate Key.
5. Can an Alternate Key become a Primary Key? Explain.

## Hard

1. Design Alternate Keys for a Hospital Management System.
2. Compare Candidate Key, Primary Key, and Alternate Key with examples.
3. Explain the role of Alternate Keys in maintaining data integrity.
4. Design Alternate Keys for an Online Shopping database.
5. Discuss when a business should choose one Candidate Key over another as the Primary Key.

---

# Key Takeaways

* An Alternate Key is a Candidate Key that is not selected as the Primary Key.
* A table can have multiple Alternate Keys.
* Alternate Keys are usually enforced using the **UNIQUE** constraint.
* They prevent duplicate values in important business columns.
* Alternate Keys improve database integrity and flexibility.

---

# Conclusion

Alternate Keys play an important role in relational database design by preserving the uniqueness of valuable business attributes that are not chosen as the Primary Key. They provide flexibility, improve data integrity, and ensure that multiple unique identifiers remain reliable throughout the database.
