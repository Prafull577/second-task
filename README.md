-- 1. Create a sample table
CREATE TABLE Employees (
    EmpID INTEGER PRIMARY KEY AUTOINCREMENT,
    Name TEXT NOT NULL,
    Department TEXT DEFAULT 'Unassigned',
    Salary REAL,
    JoiningDate DATE DEFAULT (DATE('now'))
);

-- 2. INSERT examples
-- Insert with all columns
INSERT INTO Employees (Name, Department, Salary, JoiningDate)
VALUES ('prafull', 'HR', 45000, '2024-05-15');

-- Insert using default values for Department and JoiningDate
INSERT INTO Employees (Name, Salary)
VALUES ('Sumit', 50000);

-- Insert with NULL salary
INSERT INTO Employees (Name, Department, Salary)
VALUES ('harsh', 'IT', NULL);

-- 3. UPDATE examples
-- Update salary for a specific employee
UPDATE Employees
SET Salary = 55000
WHERE Name = 'Sumit';

-- Update department for employees with NULL salary
UPDATE Employees
SET Department = 'Intern'
WHERE Salary IS NULL;

-- 4. DELETE examples
-- Delete an employee by ID
DELETE FROM Employees
WHERE EmpID = 1;

-- Delete all employees in 'Intern' department
DELETE FROM Employees
WHERE Department = 'Intern';

-- 5. Check results
SELECT * FROM Employees;
