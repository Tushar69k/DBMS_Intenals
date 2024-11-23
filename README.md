# DBMS_Intenals
Answers of Internal exams

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