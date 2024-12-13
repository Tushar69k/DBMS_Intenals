# DBMS_Intenals
Answers of Internal exams

                 IInd Internal

Q.) Diff. b/w Delete and Truncate. kk
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


___
___
___
### **1. Explain with Example:**

#### **a. Single-valued vs Multivalued Attribute**
- **Single-valued Attribute**: This attribute holds a single value for each entity.
  - **Example**: An employee's Social Security Number (SSN) is a single-valued attribute because it has only one value per employee.
    - `SSN: 123-45-6789`

- **Multivalued Attribute**: This attribute can hold multiple values for each entity.
  - **Example**: An employee's phone numbers are multivalued attributes because an employee can have more than one phone number.
    - `Phone Numbers: {123-456-7890, 098-765-4321}`

#### **b. Representation Data Model**
- **Representation Data Model**: A representation data model is used to describe the structure of a database. It includes data types, relationships, and constraints.
  - **Example**: An Entity-Relationship (ER) model represents data using entities, attributes, and relationships.
    - Entities: Employee, Department
    - Attributes: Employee (ID, Name, SSN), Department (ID, Name)
    - Relationships: Employee works in Department

#### **c. Total and Partial Participation**
- **Total Participation**: Every instance of the entity is involved in the relationship.
  - **Example**: In a university database, every student must be enrolled in at least one course. Thus, student participation in the "enrolls in" relationship is total.
  
- **Partial Participation**: Some instances of the entity are involved in the relationship, but not all.
  - **Example**: Not every employee manages a department. Thus, employee participation in the "manages" relationship is partial.

Let’s explain **Total Participation** and **Partial Participation** in a simpler way with examples so it’s easy to understand.

---

### **What is Total Participation?**
- **Meaning**: **Every entity** in a group must be involved in the relationship. No one is left out.  
- **Real-life example**:  
  Imagine a school. Every **student** in the school **must be enrolled** in at least one course.  
  - This means all students are part of the **"Enrolls" relationship**.  
  - In this case, the **Student** entity has **Total Participation** in the "Enrolls" relationship.

- **How it's shown in a diagram**:  
  In an ER diagram, this is drawn as a **double line** between the entity and the relationship.  
  Example:  
  ```
  Student ===== Enrolls
  ```

---

### **What is Partial Participation?**
- **Meaning**: **Not every entity** in a group is involved in the relationship. Some entities may not participate.  
- **Real-life example**:  
  Imagine a company. Some **employees** might manage a department, but others may not.  
  - This means only a few employees are part of the **"Manages" relationship**.  
  - In this case, the **Employee** entity has **Partial Participation** in the "Manages" relationship.

- **How it's shown in a diagram**:  
  In an ER diagram, this is drawn as a **single line** between the entity and the relationship.  
  Example:  
  ```
  Employee --- Manages
  ```

---

### **Key Differences in Simple Words**

| **Feature**            | **Total Participation**                       | **Partial Participation**                    |
|-------------------------|-----------------------------------------------|----------------------------------------------|
| **Who participates?**  | Everyone must participate in the relationship. | Only some entities participate in the relationship. |
| **Example**            | All students must enroll in a course.         | Only some employees manage a department.     |
| **Diagram**            | Double line (`====`)                          | Single line (`---`)                          |
| **Why?**               | The entity cannot exist without the relationship. | The entity can exist without the relationship. |

---

### **Examples for Better Understanding**
1. **Bank Account Example**:
   - Every **bank account** must belong to a **customer**.  
     - This is **Total Participation** because an account cannot exist without a customer.  

2. **Library Example**:
   - Not every **book** is borrowed by a member. Some books remain on shelves.  
     - This is **Partial Participation** because not all books are part of the **"Borrowed" relationship**.

---

### **Simple Explanation in One Line**
- **Total Participation**: **Everyone must be included**.  
- **Partial Participation**: **Some can stay out**. 

This should make it clearer and easier to understand! Let me know if you want more examples!

### **2. Types of Database Users and Their Activities**

#### **a. Database Administrator (DBA)**
- **Activities**: 
  - Managing database security
  - Backing up and restoring databases
  - Tuning database performance
  - Creating and managing database users

#### **b. Database Designer**
- **Activities**:
  - Designing the database schema
  - Defining tables, relationships, and constraints
  - Ensuring the database design supports application requirements

#### **c. End Users**
- **Activities**:
  - Running queries to retrieve data
  - Entering and updating data in the database
  - Generating reports based on the data

### **SQL Queries for the Given Schema**

#### **i. Create a table Catalog with Composite Primary Key and Cost Constraint**
```sql
CREATE TABLE Catalog (
    sid INT,
    pid INT,
    cost DECIMAL(10, 2) CHECK (cost > 500),
    PRIMARY KEY (sid, pid)
);
```

#### **ii. List all suppliers who have 's' as the second letter of their name**
```sql
SELECT * FROM Suppliers
WHERE sname LIKE '_s%';
```

#### **iii. Print the name of all suppliers whose turnover is greater than 50000 and live in Mumbai**
```sql
SELECT sname FROM Suppliers
WHERE turnover > 50000 AND city = 'Mumbai';
```

#### **iv. Increase the cost of all products in catalog by 10%**
```sql
UPDATE Catalog
SET cost = cost * 1.10;
```

#### **v. Delete all the products of blue color from product table**
```sql
DELETE FROM Parts
WHERE color = 'blue';
```

These queries cover the operations you need to perform on the database schema given.

















