# Normalization
- database design technique
- minimizes redundancy and dependency
- organizing data into well-structured tables
- **Goal**: 
	- reduce data duplication
	- ensure data integrity
	- improve database efficiency
	- prevent anomalies

- **Unnormalized Form (UNF)**
```
CREATE TABLE UnnormalizedBooks (
    AuthorID INT PRIMARY KEY,
    AuthorName VARCHAR(255) NOT NULL,
    BookID INT PRIMARY KEY,
    Title VARCHAR(255) NOT NULL,
    MainGenre VARCHAR(50),
    SubGenre VARCHAR(50),
    PublicationYear INT
);
```
- **1NF**
	- Eliminate data redundancy and ensure that each table contains only atomic (indivisible) values. (new AuthorTable, with AuthorID, AuthorName, UnnormalizedBooks need foreign key AuthorID)
- **2NF**
	- Achieve 1NF and ensure that non-prime attributes (attributes not part of the primary key) are fully functionally dependent on the entire primary key. (already true)
- **3NF**
	- Achieve 2NF and ensure that no transitive dependencies exist, meaning that non-prime attributes are not dependent on other non-prime attributes. (Create new table Genre, with GenreID, MainGenre, SubGenre, Books add on foreign key GenreID, remove MainGenre, SubGenre)
- **Final Result**
```
-- Authors table
CREATE TABLE Authors (
    AuthorID INT PRIMARY KEY,
    AuthorName VARCHAR(255) NOT NULL
);

-- Genres table
CREATE TABLE Genres (
    GenreID INT PRIMARY KEY,
    MainGenre VARCHAR(50) NOT NULL,
    SubGenre VARCHAR(50) NOT NULL
);

-- Books table with foreign key references to Authors and Genres
CREATE TABLE Books (
    BookID INT PRIMARY KEY,
    Title VARCHAR(255) NOT NULL,
    AuthorID INT,
    GenreID INT,
    PublicationYear INT,
    FOREIGN KEY (AuthorID) REFERENCES Authors(AuthorID),
    FOREIGN KEY (GenreID) REFERENCES Genres(GenreID)
);
```


# ACID Properties for Transactions
## Transaction
a unit or work that contains more than 1 database operation (CRUD).
```
EXAMPLE:
BEGIN/START TRANSACTION;

-- Deduct amount from sender's account
UPDATE accounts SET balance = balance - 100 WHERE account_number = 'sender_account';

-- Add the same amount to the recipient's account
UPDATE accounts SET balance = balance + 100 WHERE account_number = 'recipient_account';

-- Check for errors or conditions that warrant a rollback 
IF <some_condition> THEN 
	-- Rollback the transaction to undo changes 
	ROLLBACK;
ELSE 
	-- If no errors, commit the transaction to make changes permanent 
	COMMIT; 
END IF;
```

## Atomicity: 
- Ensures that a transaction is treated as a single, indivisible unit. It either completes entirely or has no effect at all.
- **Violation**
```
BEGIN TRANSACTION;

-- Valid operations within the transaction
UPDATE accounts SET balance = balance - 100 WHERE account_number = 'sender_account';
-- Simulating an error or failure
RAISE EXCEPTION 'Error occurred!';

COMMIT;  -- This will never be reached in case of an error, violating atomicity
```
- **Correct**
```
BEGIN TRANSACTION;

BEGIN TRY
    UPDATE accounts SET balance = balance - 100 WHERE account_number = 'sender_account';
    -- Simulate an error
    SELECT 1 / 0;
    UPDATE accounts SET balance = balance + 100 WHERE account_number = 'recipient_account';

    -- If no error, commit the transaction
    COMMIT;
END TRY
BEGIN CATCH
    -- If an error occurs, rollback the transaction
    ROLLBACK;
END CATCH;
```
## Consistency:
- Guarantees that a transaction brings the database from one valid state to another. It ensures that integrity constraints are not violated.
- **Violation**
```
BEGIN TRANSACTION;

-- Inconsistent update, more money is added to the recipient's account than deducted from the sender's account.
UPDATE accounts SET balance = balance - 100 WHERE account_number = 'sender_account';
UPDATE accounts SET balance = balance + 200 WHERE account_number = 'recipient_account';

-- This won't be reached due to the violation
COMMIT;
```
- **Correct**
```
-- Adhering to Consistency
BEGIN TRANSACTION;

BEGIN TRY
    -- Ensure consistency by deducting and adding the correct amounts
    UPDATE accounts SET balance = balance - 100 WHERE account_number = 'sender_account';
    UPDATE accounts SET balance = balance + 100 WHERE account_number = 'recipient_account';

    -- If no error, commit the transaction
    COMMIT;
END TRY
BEGIN CATCH
    -- If an error occurs, rollback the transaction
    ROLLBACK;
END CATCH;
```
## Isolation:
- Ensures that the execution of one transaction is isolated from the execution of other transactions. It prevents interference between transactions.
- **Violation
```
-- Violation of Isolation
-- Assume two transactions are running concurrently
-- Transaction 1
BEGIN TRANSACTION;
UPDATE accounts SET balance = balance - 50 WHERE account_number = 'sender_account';
-- ...

-- Transaction 2
BEGIN TRANSACTION;
UPDATE accounts SET balance = balance + 50 WHERE account_number = 'recipient_account';
-- ...

-- Concurrent execution without proper isolation
COMMIT; -- For both transactions
```
- **Correct**
```
-- Adhering to Isolation
-- Use proper isolation levels to control the visibility of changes between transactions
-- For example, using "SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;"

BEGIN TRANSACTION;

-- Transaction 1
UPDATE accounts SET balance = balance - 50 WHERE account_number = 'sender_account';
-- ...

-- Transaction 2
UPDATE accounts SET balance = balance + 50 WHERE account_number = 'recipient_account';
-- ...

-- Commit each transaction individually
COMMIT; -- For Transaction 1
COMMIT; -- For Transaction 2
```
## Durability:
- Once a transaction is committed, its effects are permanent, surviving subsequent failures.
- **Violation**
```
-- Violation of Durability
-- Assume a system failure occurs after the commit statement
BEGIN TRANSACTION;

-- Perform operations

-- This is committed to the database
COMMIT;

-- System failure occurs here before changes are actually written to durable storage, data is loss
```
- **Correct**
```
-- Adhering to Durability
-- Ensure that changes are durably stored before committing
BEGIN TRANSACTION;

-- Perform operations

-- This ensures that changes are durably stored
COMMIT;

```
# Security and Permissions
## Principle of Least Privilege:
Only grant the minimum level of access required for a user to perform their job.
## Regularly Review and Update Permissions:
Periodically review and update user permissions to ensure they align with current roles and responsibilities.
## Use Strong Authentication:
Encourage strong password policies and consider additional authentication mechanisms like multi-factor authentication.
## Audit and Monitor:
Implement logging and monitoring to track database activity and identify potential security issues.