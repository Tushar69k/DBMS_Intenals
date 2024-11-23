# DBMS_Intenals
Answers of Internal exams

                 IInd Internal

Q.) Diff. b/w Delete and Truncate.
Ans.)
| **Aspect**            | **`DELETE`**                                | **`TRUNCATE`**                            |
|-----------------------|---------------------------------------------|-------------------------------------------|
| **Command Type**      | DML (Data Manipulation Language)            | DDL (Data Definition Language)            |
| **Purpose**           | Removes specific rows based on a condition or all rows. | Removes all rows from a table.            |
| **Condition Support** | Supports `WHERE` clause for selective deletion. | Does not support conditions; removes all rows. |
| **Performance**       | Slower, as it logs each row deletion.       | Faster, as it deallocates data pages.      |
| **Triggers**          | Activates triggers defined on the table.    | Does not activate triggers.               |
| **Logging**           | Fully logged for every row deleted.         | Minimal logging; does not log row deletions. |
| **Rollback**          | Fully supports rollback within a transaction. | Supports rollback but logs minimally.     |
| **Identity Reset**    | Does not reset identity column values.      | Resets identity column values to the seed value. |
| **Table Structure**   | Preserves table structure, indexes, and constraints. | Preserves table structure, indexes, and constraints. |
| **Permission Required** | Requires `DELETE` permission.              | Requires `ALTER` permission.              |
| **Use Case**          | Used for selective or conditional row deletion. | Used to quickly remove all rows from a table. |
| **Impact on Storage** | Frees space row by row.                     | Frees entire table storage instantly.     |

This table simplifies the comparison and highlights key differences at a glance!

__________________________________________

Q.) Difference between Unique key and Primary key.
Ans.)

| Feature                     | **Primary Key**                                | **Unique Key**                                |
|-----------------------------|-----------------------------------------------|-----------------------------------------------|
| **Purpose**                 | Uniquely identifies each row in a table.      | Ensures uniqueness of values in the column(s). |
| **Number of Keys Allowed**  | Only one primary key per table.               | Multiple unique keys can exist in a table.    |
| **Null Values**             | Does not allow `NULL` values.                 | Allows one or more `NULL` values (depending on the database). |
| **Default Index**           | Creates a clustered index by default (in most databases). | Creates a non-clustered index by default.     |
| **Enforcement**             | Combination of uniqueness and non-null constraint. | Enforces only uniqueness constraint.         |
| **Relationship Use**        | Commonly used to define relationships between tables (e.g., foreign keys reference primary keys). | Rarely used in relationships.                |
| **Definition**              | Declared using `PRIMARY KEY` constraint.      | Declared using `UNIQUE` constraint.          |
| **Combination of Columns**  | Can consist of a single column or multiple columns (composite key). | Can also consist of a single or multiple columns. |
| **Use Case**                | Essential for uniquely identifying rows (mandatory for normalization). | Used for additional columns where uniqueness needs to be ensured. |

### Example:

#### **Primary Key**
```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

- `employee_id` must be unique and cannot be `NULL`.

#### **Unique Key**
```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

- `email` must be unique but can contain a `NULL` value.

___

                  Ist Internal

___ 

Q.) Single Valued Vs Multivalued Attributes.
Ans.) 

| **Aspect**                | **Single-Valued Attribute**                                     | **Multi-Valued Attribute**                                     |
|---------------------------|---------------------------------------------------------------|---------------------------------------------------------------|
| **Definition**            | Holds only one value for a specific entity instance.           | Holds multiple values for a specific entity instance.         |
| **Example**               | Phone number of a person (if only one number is allowed).      | Phone numbers of a person (if multiple numbers are allowed).  |
| **Cardinality**           | Fixed to 1.                                                   | Can have 0, 1, or more values.                                |
| **Storage**               | Typically stored as a single field in a database table.        | May require a separate table or a delimited list to store values. |
| **Complexity**            | Simple to implement and manage.                               | More complex as it requires additional handling for multiple values. |
| **Normalization**         | Does not require normalization.                               | Often requires normalization to store values in a separate table. |
| **Use Case**              | Used when only one value is logically or practically possible. | Used when multiple values are logically or practically needed. |
| **Real-World Example**    | Date of birth, Social Security Number (SSN).                  | Email addresses, hobbies, phone numbers.                     |
| **Database Design**       | Single column in the entity's table.                          | Often implemented with a relationship table to store multiple values. |
| **Constraints**           | Enforces uniqueness or limits to one value.                  | Can involve constraints to ensure no duplicate values per entity. |

### Example in Database:

**Single-Valued Attribute Example:**
```sql
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(50),
    DateOfBirth DATE
);
```

**Multi-Valued Attribute Example:**
```sql
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(50)
);

CREATE TABLE EmployeePhoneNumbers (
    EmployeeID INT,
    PhoneNumber VARCHAR(15),
    FOREIGN KEY (EmployeeID) REFERENCES Employee(EmployeeID)
);
``` 

### Summary:
- Use **single-valued attributes** for fields where only one value logically applies.
- Use **multi-valued attributes** when multiple values are required, ensuring proper database design practices to manage them.




















