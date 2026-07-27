# Create Table With All Constraints

# Introduction

In real-world database applications, a table rarely uses just one constraint. Instead, multiple constraints work together to ensure that the data stored is **accurate, consistent, secure, and reliable**.

For example, in an Employee Management System:

* Every employee should have a unique Employee ID.
* Every employee must have a name.
* Every email address should be unique.
* Salary should never be negative.
* Department should have a default value if none is provided.
* Every employee should belong to an existing department.

These requirements are enforced using a combination of SQL constraints.

This chapter demonstrates how to create tables using **all major SQL constraints together**.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Create tables using multiple constraints.
* Understand how constraints work together.
* Design robust database schemas.
* Apply best practices while creating tables.
* Understand constraint interactions.
* Build interview-ready SQL table definitions.

---

# Problem Statement

Suppose we are developing an **Employee Management System**.

Business Requirements:

* Every department must have a unique ID.
* Every employee must have a unique ID.
* Employee names are mandatory.
* Employee emails must be unique.
* Salary cannot be negative.
* Every employee belongs to an existing department.
* Employee status should default to **'Active'**.
* Employee IDs should be generated automatically.

To satisfy these requirements, multiple constraints must be used together.

---

# Constraints Used

| Constraint                  | Purpose                                |
| --------------------------- | -------------------------------------- |
| PRIMARY KEY                 | Uniquely identifies each row           |
| FOREIGN KEY                 | Maintains relationships between tables |
| NOT NULL                    | Prevents NULL values                   |
| UNIQUE                      | Prevents duplicate values              |
| CHECK                       | Validates values                       |
| DEFAULT                     | Assigns default values                 |
| AUTO_INCREMENT / Equivalent | Generates IDs automatically            |

---

# Step 1 – Create the Parent Table

The **Department** table is created first because the Employee table references it.

## MySQL

```sql
CREATE TABLE Department (
    DepartmentID INT AUTO_INCREMENT PRIMARY KEY,
    DepartmentName VARCHAR(100)
        NOT NULL
        UNIQUE
);
```

---

# Step 2 – Create the Employee Table

## MySQL

```sql
CREATE TABLE Employee (
    EmployeeID INT AUTO_INCREMENT PRIMARY KEY,

    EmployeeName VARCHAR(100)
        NOT NULL,

    Email VARCHAR(150)
        UNIQUE,

    Salary DECIMAL(10,2)
        CHECK (Salary >= 0),

    Status VARCHAR(20)
        NOT NULL
        DEFAULT 'Active',

    JoiningDate DATE
        DEFAULT CURRENT_DATE,

    DepartmentID INT
        NOT NULL,

    CONSTRAINT FK_Employee_Department
    FOREIGN KEY (DepartmentID)
    REFERENCES Department(DepartmentID)
);
```

---

# Understanding Each Constraint

| Column       | Constraint                   | Purpose                              |
| ------------ | ---------------------------- | ------------------------------------ |
| EmployeeID   | PRIMARY KEY + AUTO_INCREMENT | Unique employee identifier           |
| EmployeeName | NOT NULL                     | Name is mandatory                    |
| Email        | UNIQUE                       | Prevents duplicate emails            |
| Salary       | CHECK                        | Salary cannot be negative            |
| Status       | DEFAULT + NOT NULL           | Automatically sets status            |
| JoiningDate  | DEFAULT                      | Uses today's date if omitted         |
| DepartmentID | FOREIGN KEY + NOT NULL       | Employee must belong to a department |

---

# Example 1 – Insert Departments

```sql
INSERT INTO Department (DepartmentName)
VALUES
('HR'),
('Finance'),
('IT');
```

---

# Department Table

| DepartmentID | DepartmentName |
| -----------: | -------------- |
|            1 | HR             |
|            2 | Finance        |
|            3 | IT             |

---

# Example 2 – Valid Employee Insert

```sql
INSERT INTO Employee
(
    EmployeeName,
    Email,
    Salary,
    DepartmentID
)
VALUES
(
    'Rahul',
    'rahul@example.com',
    50000,
    3
);
```

---

# Result

| EmployeeID | EmployeeName | Email                                         | Salary   | Status | JoiningDate  | DepartmentID |
| ---------- | ------------ | --------------------------------------------- | -------- | ------ | ------------ | ------------ |
| 1          | Rahul        | [rahul@example.com](mailto:rahul@example.com) | 50000.00 | Active | Current Date | 3            |

Notice:

* EmployeeID is generated automatically.
* Status becomes **Active**.
* JoiningDate uses the current date.
* DepartmentID exists in the Department table.

---

# Example 3 – Duplicate Email

```sql
INSERT INTO Employee
(
    EmployeeName,
    Email,
    Salary,
    DepartmentID
)
VALUES
(
    'Priya',
    'rahul@example.com',
    45000,
    2
);
```

### Result

❌ Error

Reason:

The `UNIQUE` constraint prevents duplicate email addresses.

---

# Example 4 – Negative Salary

```sql
INSERT INTO Employee
(
    EmployeeName,
    Email,
    Salary,
    DepartmentID
)
VALUES
(
    'Arun',
    'arun@example.com',
    -1000,
    1
);
```

### Result

❌ Error

Reason:

The `CHECK (Salary >= 0)` constraint is violated.

---

# Example 5 – Invalid Department

```sql
INSERT INTO Employee
(
    EmployeeName,
    Email,
    Salary,
    DepartmentID
)
VALUES
(
    'Sneha',
    'sneha@example.com',
    40000,
    99
);
```

### Result

❌ Error

Reason:

Department **99** does not exist.

The `FOREIGN KEY` constraint rejects the operation.

---

# Example 6 – Missing Employee Name

```sql
INSERT INTO Employee
(
    EmployeeName,
    Email,
    Salary,
    DepartmentID
)
VALUES
(
    NULL,
    'test@example.com',
    35000,
    1
);
```

### Result

❌ Error

Reason:

`EmployeeName` is defined as `NOT NULL`.

---

# Internal Working

```text
User
   │
   ▼
INSERT Statement
   │
   ▼
Generate AUTO_INCREMENT Value
   │
   ▼
Check NOT NULL
   │
   ▼
Check UNIQUE
   │
   ▼
Check CHECK Constraint
   │
   ▼
Apply DEFAULT Values
   │
   ▼
Validate FOREIGN KEY
   │
   ▼
All Constraints Passed?
 │
 ├── Yes → Store Record
 │
 └── No → Reject Operation
```

---

# Constraint Validation Order

Although the exact implementation depends on the database system, the validation process generally follows this logical flow:

```text
INSERT
   │
   ▼
AUTO_INCREMENT
   │
   ▼
DEFAULT
   │
   ▼
NOT NULL
   │
   ▼
CHECK
   │
   ▼
UNIQUE / PRIMARY KEY
   │
   ▼
FOREIGN KEY
   │
   ▼
Record Stored
```

---

# Database Compatibility

| Feature                     | MySQL |       PostgreSQL      |  SQL Server  |       SQLite      |
| --------------------------- | :---: | :-------------------: | :----------: | :---------------: |
| PRIMARY KEY                 |   ✅   |           ✅           |       ✅      |         ✅         |
| FOREIGN KEY                 |   ✅   |           ✅           |       ✅      |         ✅         |
| NOT NULL                    |   ✅   |           ✅           |       ✅      |         ✅         |
| UNIQUE                      |   ✅   |           ✅           |       ✅      |         ✅         |
| CHECK                       |   ✅*  |           ✅           |       ✅      |         ✅         |
| DEFAULT                     |   ✅   |           ✅           |       ✅      |         ✅         |
| AUTO_INCREMENT / Equivalent |   ✅   | ✅ (SERIAL / IDENTITY) | ✅ (IDENTITY) | ✅ (AUTOINCREMENT) |

> *Modern MySQL versions enforce `CHECK` constraints.

---

# Real-World Applications

| Industry   | Example                               |
| ---------- | ------------------------------------- |
| School     | Student, Course, Enrollment tables    |
| Banking    | Customer, Account, Transaction tables |
| Hospital   | Patient, Doctor, Appointment tables   |
| HR         | Employee and Department tables        |
| E-Commerce | Customer, Product, Order tables       |
| Library    | Member, Book, Borrow tables           |

---

# Advantages

* Ensures high data integrity.
* Prevents invalid or inconsistent records.
* Reduces application-side validation.
* Improves database reliability.
* Enforces business rules directly in the database.
* Makes schemas easier to understand and maintain.

---

# Limitations

* Overusing constraints can reduce flexibility.
* Existing invalid data must be corrected before adding constraints.
* Constraint syntax differs slightly across database systems.
* Complex schemas require careful planning.

---

# Common Mistakes

* Creating child tables before parent tables.
* Forgetting to define primary keys.
* Using mismatched data types for foreign keys.
* Ignoring existing duplicate data before adding `UNIQUE`.
* Assuming `DEFAULT` replaces `NOT NULL`.
* Choosing inappropriate default values.

---

# Best Practices

* Create parent tables before child tables.
* Define a primary key for every table.
* Use meaningful names for constraints.
* Apply `NOT NULL` only to mandatory columns.
* Use `CHECK` to enforce business rules.
* Use `DEFAULT` for common values.
* Use auto-generated keys for surrogate identifiers.
* Test both valid and invalid inserts.

---

# Interview Questions

### 1. Why are multiple constraints used together?

**Answer:** Because different constraints enforce different rules such as uniqueness, mandatory values, valid ranges, relationships, and automatic default values.

---

### 2. Which constraint ensures an employee belongs to an existing department?

**Answer:** `FOREIGN KEY`

---

### 3. Which constraint automatically generates employee IDs?

**Answer:** `AUTO_INCREMENT` (or `IDENTITY`, `SERIAL`, or `GENERATED AS IDENTITY` depending on the database system).

---

### 4. Can a single column have multiple constraints?

**Answer:** Yes. For example:

```sql
Status VARCHAR(20)
NOT NULL
DEFAULT 'Active'
```

---

### 5. Which constraint prevents duplicate email addresses?

**Answer:** `UNIQUE`

---

# Practice Questions

## Easy

1. List all major SQL constraints.
2. Which constraint generates IDs automatically?
3. Which constraint prevents duplicate values?
4. Which constraint enforces relationships?
5. Which constraint provides default values?

---

## Medium

1. Create an Employee table using all major constraints.
2. Create Department and Employee tables with a foreign key relationship.
3. Explain how multiple constraints work together.
4. Write valid and invalid `INSERT` statements for the Employee table.
5. Explain the purpose of each constraint used in the Employee table.

---

## Hard

1. Design a complete HR database using multiple constraints.
2. Compare constraint support across MySQL, PostgreSQL, SQL Server, and SQLite.
3. Explain the logical validation process during an `INSERT`.
4. Discuss the advantages and limitations of combining multiple constraints.
5. Design a production-ready Employee table using industry best practices.

---

# Key Takeaways

* Real-world tables typically use multiple constraints together.
* `PRIMARY KEY` uniquely identifies records.
* `FOREIGN KEY` maintains relationships.
* `NOT NULL` ensures mandatory fields.
* `UNIQUE` prevents duplicate values.
* `CHECK` validates business rules.
* `DEFAULT` assigns predefined values automatically.
* `AUTO_INCREMENT` (or its equivalent) generates unique identifiers.

---

# Conclusion

Creating tables with multiple constraints is a fundamental skill in relational database design. By combining `PRIMARY KEY`, `FOREIGN KEY`, `NOT NULL`, `UNIQUE`, `CHECK`, `DEFAULT`, and `AUTO_INCREMENT`, you can build databases that enforce business rules, maintain data integrity, and reduce application-level validation. A well-designed schema not only improves reliability and performance but also makes future maintenance and development much easier. In the next chapter, you will learn about **SQL Comments**, which help document SQL scripts and improve code readability.
