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