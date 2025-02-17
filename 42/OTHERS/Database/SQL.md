## SQL (Structured Query Language) is the language used to interact with relational databases.

# CRUD
- **Create table:**
```
CREATE TABLE {table-name} (
	{field-name-1} {type} PRIMARY KEY,
	{field-name-2} {type} {options},
	...,
	FOREIGN KEY ({field-name-in-this-table}) REFERENCES {fkey-table-name}({fkey-field-name}),
)
```

- **SELECT Statement:**
```
SELECT * FROM {table-name};  //* means all

-- SELECT with JOIN to retrieve details along additional details
SELECT {table1}.{fkey-field}, {table2}.{pkey-field}
FROM {table1}
JOIN {table2} ON {table1}.{fkey-field} = {table2}.{pkey-field};
```

- **INSERT Statement:** 
```
INSERT INTO {table} ({f1},  {f2}, ...) VALUES
({value-f1}, {value-f2}, ...),
({value-f1}, {value-f2}, ...),
...;
```

- **UPDATE Statement:** Modifies existing records.
```
UPDATE {table}
SET {field} = {new-value}
WHERE {identifier} = {identifier-value};
```

- **DELETE Statement:** 
```
DELETE FROM {table} WHERE {identifier} = {identifier-value};
```
- **WHERE Clause:** Enables you to filter data based on specific conditions. For instance, you can retrieve books written by a particular author or published after a certain date.
```
EXAMPLES:
SELECT * FROM employees WHERE job_title = 'Manager';
SELECT * FROM employees WHERE job_title = 'Manager' AND department_id = 1;
SELECT * FROM employees WHERE job_title = 'Manager' OR department_id = 1;
SELECT * FROM employees WHERE department_id IN (1, 2, 3);
SELECT * FROM employees WHERE last_name LIKE 'S%';
SELECT * FROM employees WHERE salary BETWEEN 50000 AND 80000;
SELECT * FROM employees WHERE manager_id IS NULL;
SELECT * FROM employees WHERE manager_id IS NOT NULL;
SELECT * FROM employees WHERE job_title = 'Manager' AND (department_id = 1 OR department_id = 2);
```
# JOINS
- **Inner Join**: Returns the matches in both tables
```
SELECT * FROM Table1 INNER JOIN Table2 ON Table1.ID = Table2.ID;
```

- **Left Join/Outer Join OR Right Join/Outer Join**: Returns all records from 1 table plus only the matched values from the other table. If LEFT: Returns all left and matched right. If RIGHT: Returns all right then matched left.
```
SELECT * FROM Table1 LEFT/RIGHT JOIN Table2 ON Table1.ID = Table2.ID;
```

- **Full Join**: Returns all records where there is a match on either side of the table
```
SELECT * FROM Table1 FULL JOIN Table2 ON Table1.ID = Table2.ID;
```

# M:N (Many-to-Many) Relationships
- In a many-to-many relationship, each row in the first table can be related to one or more rows in the second table, and vice versa.
- To represent a many-to-many relationship, an intermediate or junction table is used.
- Example: A "Student" table can be related to multiple "Course" rows, and each course can have multiple students.
```
CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(50)
);

CREATE TABLE Course (
    CourseID INT PRIMARY KEY,
    CourseName VARCHAR(50)
);

CREATE TABLE Enrollment ( %% student_course - naming convention for junction table %%
    StudentID INT,
    CourseID INT,
    PRIMARY KEY (StudentID, CourseID),
    FOREIGN KEY (StudentID) REFERENCES Student(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Course(CourseID)
);

```
# Indexes and Optimization
- Indexes improve query speed by providing a quick lookup mechanism. Created on columns used frequently in WHERE clause or JOIN conditions.
- Include execution plan Ctrl+M before executing query to see details.
- Imagine a table with 100000 employeeID and employee names ranging from A-Z, but the table is first ordered with employee ID, to find a specifc employee name of Adam with ID 25479, it searches through all the employee ID to look for a match. But with Index, employeeID is still ordered but this time employeeName is in a way seperated in alphabetical order with a maximum of (100000/2 and so on). 
- You can get the index creation query by clicking on "Missing Index Details", can be found by right clicking the Missing Index message after you try to filter with WHERE clause.
- To read the execution plan, it starts from RIGHT to LEFT, TOP to BOTTOM
- You can also add an EXPLAIN statement infront of your query to see its details.

- **Create Index**:
```
CREATE INDEX idx_lastname ON employees(last_name);
```

# Aggregate Functions and Grouping
- **COUNT**, **SUM**, **AVG**, **MIN**, **MAX**
- **HAVING**
```
SELECT department_id, AVG(salary) FROM employees GROUP BY department_id HAVING AVG(salary) > 50000;
```
- **GROUP BY**
```
SELECT department_id, AVG(salary) FROM employees GROUP BY department_id;
```

# Subqueries
- Queries embedded within other queries
```
--EXAMPLES:
SELECT employee_name
FROM employees
WHERE employee_id = (SELECT manager_id FROM employees WHERE employee_name = 'John Doe');

SELECT employee_name
FROM employees
WHERE department_id IN (SELECT department_id FROM departments WHERE location = 'New York');

SELECT employee_name, salary, (SELECT AVG(salary) FROM employees) AS avg_salary
FROM employees;

--CORRELATED SUBQUERIES:
SELECT department_name, (SELECT COUNT(*) FROM employees WHERE department_id = d.department_id) AS num_employees
FROM departments d;

%% find employees whose salary is higher than the average salary in their department %%
SELECT employee_name
FROM employees e
WHERE salary > (SELECT AVG(salary) FROM employees WHERE department_id = e.department_id);

```
# Stored Procedures and Functions
## Stored Procedure
- **Creating**
```
-- Assuming 'employees' table structure: (employee_id INT, name VARCHAR(255), ...)

-- Create or replace the stored procedure
CREATE OR REPLACE PROCEDURE GetEmployeeDetails(
    IN employeeID INT,
    OUT employeeName VARCHAR(255),
    OUT employeeDepartment VARCHAR(50)
)
BEGIN
    -- Declare variables to store the retrieved data
    DECLARE empName VARCHAR(255);
    DECLARE empDept VARCHAR(50);

    -- Use a SELECT INTO statement to retrieve employee details
    SELECT name, department INTO empName, empDept
    FROM employees
    WHERE employee_id = employeeID;

    -- Set OUT parameters
    SET employeeName = empName;
    SET employeeDepartment = empDept;
END;
```
- **Calling
```
CALL GetEmployeeDetails(101);
```
## Functions
- **Creating
```
-- Create or replace the function
CREATE OR REPLACE FUNCTION CalculateTax(salary DECIMAL(10, 2)) RETURNS DECIMAL(10, 2)
BEGIN
    DECLARE tax DECIMAL(10, 2);

    -- Add validation for non-negative salary
    IF salary < 0 THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Salary must be non-negative';
    END IF;

    -- Example tax calculation
    SET tax = salary * 0.2;

    -- Ensure tax is not negative
    IF tax < 0 THEN
        SET tax = 0;
    END IF;

    RETURN tax;
END;
```
- **Calling**
```
SELECT employee_name, salary, CalculateTax(salary) AS tax FROM employees;
```

| Feature                   | Stored Procedure                           | Function                                   |
|---------------------------|--------------------------------------------|--------------------------------------------|
| **Return Value**          | Can use OUT or INOUT parameters, does not have a return statement. | Must have a return statement, returns a single value. |
| **Usage in Queries**      | Typically used for actions, not in expressions. | Used in SQL queries as part of an expression. |
| **Usage in SELECT Statements** | Cannot be directly used.                | Can be used in a SELECT statement.         |
| **Transaction Control**   | Can contain transaction control statements (e.g., COMMIT, ROLLBACK). | Does not contain transaction control statements. |
| **Calling Syntax**        | Called using the CALL statement or in control-of-flow structures. | Called as part of an expression or a SELECT statement. |
| **Exception Handling**    | Can use database-specific exception handling mechanisms (e.g., TRY...CATCH). | Generally does not handle exceptions in the same way. |
| **Purpose**               | Used for encapsulating a series of SQL statements that perform actions. | Used for calculations or tasks that return a single, scalar value. |
| **Examples**              | ```sql CREATE PROCEDURE MyProcedure() BEGIN ... END; ``` | ```sql CREATE FUNCTION MyFunction() RETURNS INT BEGIN ... END; ``` |
| **Return Type**           | Does not have a specific return type.    | Must specify a return type.                |
| **Use in Expressions**    | Typically not used in expressions.        | Used in expressions and queries.           |

# Triggers
## Types:
- **BEFORE:** Executed before a change.
- **AFTER:** Executed after a change.
- **INSTEAD OF:** Replaces the triggering action.
```
-- EXAMPLE:
CREATE TRIGGER BeforeEmployeeUpdate
BEFORE UPDATE ON employees
FOR EACH ROW
BEGIN
    -- Trigger logic here
    IF NEW.salary < OLD.salary THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Salary cannot be decreased.';
    END IF;
END;
```
