# Codd's Rules (Relational Database Model)

## Introduction

The **Relational Database Model** was introduced by **Dr. Edgar F. Codd** in 1970. Before relational databases, most database systems stored data using hierarchical or network models, making data retrieval complex and difficult to maintain.

To ensure that a database management system truly follows the **Relational Model**, Dr. Codd proposed a set of **13 rules (Rule 0 to Rule 12)**. These rules define the characteristics of an ideal Relational Database Management System (RDBMS).

Although no commercial database satisfies all the rules completely, modern RDBMSs such as **MySQL**, **PostgreSQL**, **Oracle Database**, **Microsoft SQL Server**, and **SQLite** implement most of the important principles.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand the purpose of Codd's Rules.
* Learn why these rules are important for relational databases.
* Explain each rule in simple language.
* Differentiate an RDBMS from a non-relational database system.
* Answer interview questions related to Codd's Rules.

---

# Problem Statement

Suppose an organization stores employee records in different file formats.

Problems include:

* Duplicate data
* Difficult data retrieval
* Inconsistent information
* Poor security
* Limited data independence

To overcome these issues, a standard database model was required.

Dr. Edgar F. Codd proposed rules that define how a true relational database should behave.

---

# Why Do We Need Codd's Rules?

Without standards:

* Every database vendor could implement databases differently.
* Applications would become difficult to migrate.
* Data consistency could not be guaranteed.
* Relationships between data would become unreliable.

Codd's Rules provide a common foundation for designing reliable relational database systems.

---

# What is a Relational Database?

A relational database stores data in the form of **tables (relations)**.

Each table consists of:

* Rows (Tuples)
* Columns (Attributes)

Example:

| StudentID | Name    | Age |
| --------- | ------- | --- |
| 101       | Alice   | 20  |
| 102       | Bob     | 21  |
| 103       | Charlie | 22  |

---

# ASCII Diagram

```
                    Relational Database

                          Database
                              |
        -----------------------------------------
        |                   |                   |
     Student             Course             Faculty
        |                   |                   |
      Rows                Rows                Rows
      Columns             Columns             Columns
```

---

# What are Codd's Rules?

Codd's Rules are a collection of **13 rules** used to determine whether a DBMS can be considered a true Relational Database Management System.

The rules are numbered:

* Rule 0
* Rule 1
* Rule 2
* Rule 3
* Rule 4
* Rule 5
* Rule 6
* Rule 7
* Rule 8
* Rule 9
* Rule 10
* Rule 11
* Rule 12

---

# Rule 0 – Foundation Rule

## Definition

A database system must manage the database entirely using relational capabilities.

### Meaning

If a system claims to be an RDBMS, every operation should follow relational principles.

### Example

✔ Correct

```
Store data using tables
Retrieve data using SQL
Maintain relationships
```

✘ Incorrect

```
Store some data in proprietary files
Bypass relational rules internally
```

---

# Rule 1 – Information Rule

## Definition

All information in a database must be represented only as values stored in tables.

### Example

Employee

| ID  | Name  |
| --- | ----- |
| 101 | Alice |
| 102 | Bob   |

Everything is stored as table values.

---

# Rule 2 – Guaranteed Access Rule

## Definition

Every individual value must be accessible using:

* Table Name
* Primary Key
* Column Name

Example

```
Employee(ID=101).Name
```

The value "Alice" can be accessed uniquely.

---

# Rule 3 – Systematic Treatment of NULL Values

## Definition

NULL should represent missing, unknown, or inapplicable information.

Example

| ID  | Name  | Phone |
| --- | ----- | ----- |
| 101 | Alice | NULL  |

NULL is different from:

* 0
* Empty String ("")
* False

---

# Rule 4 – Dynamic Online Catalog

The database metadata should be stored as relational tables.

This allows users to query metadata using SQL.

Example:

* Table names
* Column names
* Constraints
* Views

---

# Rule 5 – Comprehensive Data Sublanguage Rule

The database must support one complete language capable of:

* Data Definition (DDL)
* Data Manipulation (DML)
* Querying (DQL)
* Security
* Transactions
* Constraints

Example:

SQL

---

# Rule 6 – View Updating Rule

All theoretically updatable views should also be updatable by the database.

Example

```
Original Table

Employee

↓

View

ActiveEmployees

↓

UPDATE View

↓

Employee Table Updated
```

---

# Rule 7 – High-Level Insert, Update and Delete

The DBMS should allow operations on multiple rows at once.

Example

Instead of updating one row at a time,

```
UPDATE Employee
SET Salary = Salary + 1000;
```

Every employee gets updated simultaneously.

---

# Rule 8 – Physical Data Independence

Changes in physical storage should not affect applications.

Example

```
Before

Hard Disk

↓

After

SSD

↓

Application Works Normally
```

---

# Rule 9 – Logical Data Independence

Changes in table structure should have minimal impact on applications.

Example

Adding a new column should not break existing queries that do not depend on it.

---

# Rule 10 – Integrity Independence

Integrity constraints should be defined within the database itself.

Examples

* PRIMARY KEY
* FOREIGN KEY
* UNIQUE
* CHECK
* NOT NULL

Applications should not be solely responsible for enforcing data integrity.

---

# Rule 11 – Distribution Independence

Users should access the database in the same way regardless of whether the data is stored on one server or distributed across multiple servers.

```
Application

      |

      v

+-------------------+
|      DBMS         |
+-------------------+
      |
 -------------
 |           |
Server A   Server B
```

The application's interaction remains unchanged.

---

# Rule 12 – Non-Subversion Rule

If the DBMS provides low-level access, it must not bypass relational integrity rules.

Example

Even internal utilities should respect:

* Constraints
* Security
* Relationships

---

# Summary Table

| Rule | Name                              | Purpose                                           |
| ---- | --------------------------------- | ------------------------------------------------- |
| 0    | Foundation Rule                   | Entire DBMS must follow relational principles     |
| 1    | Information Rule                  | Store all data in tables                          |
| 2    | Guaranteed Access Rule            | Access every value uniquely                       |
| 3    | NULL Rule                         | Handle missing data correctly                     |
| 4    | Dynamic Online Catalog            | Metadata stored as tables                         |
| 5    | Comprehensive Data Sublanguage    | Support complete SQL operations                   |
| 6    | View Updating Rule                | Updatable views should remain updatable           |
| 7    | High-Level Insert, Update, Delete | Set-based operations                              |
| 8    | Physical Data Independence        | Storage changes shouldn't affect applications     |
| 9    | Logical Data Independence         | Schema changes should minimize application impact |
| 10   | Integrity Independence            | Constraints managed by DBMS                       |
| 11   | Distribution Independence         | Same interface for distributed databases          |
| 12   | Non-Subversion Rule               | Low-level access cannot violate relational rules  |

---

# Advantages

* Defines the characteristics of a true RDBMS.
* Encourages data consistency.
* Improves portability across database systems.
* Promotes data independence.
* Supports reliable application development.
* Establishes standardized database behavior.

---

# Limitations

* No commercial RDBMS fully satisfies all 13 rules.
* Some rules are theoretical and difficult to implement completely.
* Modern databases sometimes prioritize performance over strict adherence.

---

# Common Mistakes

* Thinking there are only 12 rules (there are **13**, including Rule 0).
* Assuming every SQL database fully follows Codd's Rules.
* Confusing NULL with 0 or an empty string.
* Believing data integrity should be enforced only in application code.

---

# Best Practices

* Design normalized relational tables.
* Use appropriate constraints to enforce integrity.
* Prefer SQL for interacting with relational data.
* Keep business rules in the database where appropriate.
* Understand Codd's Rules as design principles rather than a checklist for vendor selection.

---

# Interview Questions

### 1. Who proposed Codd's Rules?

**Answer:** Dr. Edgar F. Codd.

---

### 2. How many Codd's Rules are there?

**Answer:** 13 rules (Rule 0 to Rule 12).

---

### 3. Why is Rule 0 important?

**Answer:** It states that a system can claim to be an RDBMS only if it manages the database entirely through relational capabilities.

---

### 4. Which rule discusses NULL values?

**Answer:** Rule 3.

---

### 5. Which rule focuses on physical data independence?

**Answer:** Rule 8.

---

### 6. Which rule ensures constraints are managed by the database?

**Answer:** Rule 10 (Integrity Independence).

---

# Practice Questions

## Easy

1. Who is known as the father of the Relational Database Model?
2. What is the purpose of Codd's Rules?
3. What is Rule 1 called?
4. What is the meaning of NULL in a database?
5. Why is SQL important in a relational database?

## Medium

1. Explain Rule 7 with an example.
2. Differentiate Physical and Logical Data Independence.
3. Why are integrity constraints important?
4. Explain Rule 4 in your own words.
5. What is the role of Rule 6?

## Hard

1. Why do modern RDBMSs not fully satisfy all Codd's Rules?
2. Discuss the practical significance of Rule 12.
3. Compare Rule 8 and Rule 9 with real-world examples.
4. How do Codd's Rules contribute to database reliability?
5. Evaluate whether strict compliance with all rules is necessary in modern database systems.

---

# Key Takeaways

* Dr. Edgar F. Codd introduced the Relational Database Model and the 13 Codd's Rules.
* The rules define the principles of a true RDBMS.
* Data should be stored as tables with well-defined relationships.
* SQL provides the language for managing relational databases.
* Data independence, integrity, and consistency are central goals of the relational model.
* Modern RDBMSs implement most of these principles, even if they do not fully satisfy every rule.

---

# Conclusion

Codd's Rules laid the foundation for modern relational databases and continue to influence database design today. While complete compliance is rare in commercial systems, understanding these rules helps developers build well-structured, reliable, and maintainable databases. They remain an essential topic for academic study, technical interviews, and professional database development.
