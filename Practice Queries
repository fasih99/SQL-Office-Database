--Practice Questions 

--Find all employees
SELECT * FROM employee;

--Find all employees ordered by salary 

SELECT *
FROM employee
ORDER BY salary DESC;

--Find all employees ordered by sex then name
SELECT *
FROM employee
ORDER BY sex DESC, salary DESC;

--Find first 5 employees
SELECT * 
FROM employee
LIMIT 5;

--FIND ALL FORNAME AND SURNAMES
SELECT employee.first_name AS forename, employee.last_name AS surname
FROM employee;

--FIND all genders
SELECT DISTINCT employee.sex
FROM employee;

--FIND all clients 
SELECT DISTINCT client.client_name
FROM client;

--SQL AGGREGATE FUNCTIONS 
--COUNT FUNCTION
--FIND NUMBER OF EMPLOYEES
SELECT COUNT(employee.emp_id)
FROM employee;


--FIND NUMBER OF FEMALE EMPLOYEES BORN AFTER 1970
SELECT COUNT(employee.sex)
FROM employee
WHERE birth_date > '1971-01-01';


--AVG : AVERAGE
--FIND AVERAGE OF ALL EMPLOYEE SALARY
SELECT AVG(employee.salary)
FROM employee;

--FIND AVERAGE OF ALL EMPLOYEE SALARY WHO ARE MALES

SELECT AVG(employee.salary)
FROM employee
WHERE sex = 'M';

--FIND AVERAGE OF ALL EMPLOYEE SALARY WHO ARE MALES

SELECT AVG(employee.salary)
FROM employee
WHERE sex = 'F';

--SUM 

--FIND SUM OF ALL employees 
SELECT SUM(employee.salary)
FROM employee;

--GROUP BY 

--FIND HOW MANY MALES AND FEMALES WORK
SELECT COUNT(employee.sex), sex
FROM employee
GROUP BY sex;

--THIS ALLOW TO GET DISTINCT VALUES IN A ROW
--The GROUP BY statement groups rows that have the same values into summary rows,
--like "find the number of customers in each country".

-- The GROUP BY statement is often used with 
-- aggregate functions (COUNT, MAX, MIN, SUM, AVG) 
-- to group the result-set by one or more columns.


--FIND TOTAL SALES OF EACH sales employee 

SELECT SUM(total_sales), emp_id
FROM works_with
GROUP BY emp_id;

--Find highest sales of each employee

SELECT MAX(totat_sales), emp_id
FROM works_with
GROUP BY emp_id;

--Find lowest sales of each sales  employee

SELECT MIN(totat_sales), emp_id
FROM works_with
GROUP BY emp_id
ORDER BY emp_id DESC;

--LIKE and WILD CARDS 

-- The LIKE operator is used in a WHERE clause to search for a specified pattern in a column.

-- There are two wildcards often used in conjunction with the LIKE operator:
--A wildcard character is used to substitute one or more characters in a string.

--Wildcard characters are used with the SQL LIKE operator. 
--The LIKE operator is used in a WHERE clause to search for a specified pattern in a column.
-- % - The percent sign represents zero, one, or multiple characters
-- _ - The underscore represents a single character

--Q.FIND ANY CLIENT WHO ARE LLC I.E THEIR NAME ENDS WITH LLC

SELECT *
FROM client
WHERE client_name LIKE '%LLC';

-- WHERE CustomerName LIKE 'a%'	Finds any values that start with "a"
-- WHERE CustomerName LIKE '%a'	Finds any values that end with "a"
-- WHERE CustomerName LIKE '%or%'	Finds any values that have "or" in any position
-- WHERE CustomerName LIKE '_r%'	Finds any values that have "r" in the second position
-- WHERE CustomerName LIKE 'a_%'	Finds any values that start with "a" and are at least 2 characters in length
-- WHERE CustomerName LIKE 'a__%'	Finds any values that start with "a" and are at least 3 characters in length
-- WHERE ContactName LIKE 'a%o'	Finds any values that start with "a" and ends with "o"

--Q. FIND employees with 3 letter name.
SELECT employee.first_name
FROM employee
WHERE first_name LIKE '___';


-- Wild Cards in SQL Server (Not MYSQL)
-- %	Represents zero or more characters	bl% finds bl, black, blue, and blob
-- _	Represents a single character	h_t finds hot, hat, and hit
-- []	Represents any single character within the brackets	h[oa]t finds hot and hat, but not hit
-- ^	Represents any character not in the brackets	h[^oa]t finds hit, but not hot and hat
-- -	Represents a range of characters	c[a-b]t finds cat and cbt


--Q.Find any branch suppliers who are in the label business

SELECT *
FROM branch_supplier
WHERE supplier_name LIKE '%lab%';

--Q. Find an employee born in October
SELECT *
FROM employee
WHERE birth_date LIKE '____-02%';

-- UNION OPERATOR 
-- The UNION operator is used to combine the result-set of two or more SELECT statements.

-- Each SELECT statement within UNION must have the same number of columns
-- The columns must also have similar data types
-- The columns in each SELECT statement must also be in the same order

-- UNION only selects distinct values

-- UNION ALL on the otherhand selects duplicates as well.

--Q. Find a list of employee and branch names 

SELECT first_name AS List
FROM employee
UNION
SELECT branch_name
FROM branch;

--Q. Find all the money which the company spends and earns

SELECT SUM(salary),'Spends' AS 'Money'
FROM employee
UNION
SELECT SUM(totat_sales),'Earns' AS 'Money'
FROM works_with;

--Q. Find all money spend or earned

SELECT salary
FROM employee
UNION
SELECT totat_sales
FROM works_with;


-- JOINS 

--A JOIN clause is used to combine rows from two or more tables,
--based on a related column between them.

-- Here are the different types of the JOINs in SQL:

-- (INNER) JOIN: Returns records that have matching values in both tables
-- LEFT (OUTER) JOIN: Returns all records from the left table, and the matched records from the right table
-- RIGHT (OUTER) JOIN: Returns all records from the right table, and the matched records from the left table
-- FULL (OUTER) JOIN: Returns all records when there is a match in either left or right table
-- SELF JOIN : WHERE TABLE IS JOINED WITH ITSLEF
-- NOTE : FULL JOIN does not exist in mysql

-- Q. Find all branches and names of the manager

SELECT emp_id, first_name, last_name, branch_name
FROM employee
INNER JOIN branch
ON employee.emp_id=branch.mgr_id;


-- Nested Queries 

--Q. Find names of all who employees 
---  who sold more than 30k paper

SELECT *
FROM employee
WHERE emp_id IN (
    SELECT emp_id
    FROM works_with
    WHERE totat_sales>30000
);

--Q. FIND ALL client who buy from MICHAEL SCOTT's branch

SELECT client.client_name
FROM client
WHERE branch_id IN (
    SELECT branch.branch_id 
    FROM branch
    WHERE branch.mgr_id = (
        SELECT employee.emp_id
        FROM employee
        WHERE first_name='Michael'
        Limit 1
    )
);

--NOTE : USE ON DELETE CASCADE WHEN FOREIGN KEY IS A PK OR PART OF PK

-- Triggers 

-- A trigger in MySQL is a set of SQL statements that reside in a system catalog. 
-- It is a special type of stored procedure that is invoked automatically in response to an event.
-- Each trigger is associated with a table, which is activated on any DML statement such as INSERT, UPDATE, or DELETE.

 
 -- General Syntax CREATE TRIGGER trigger_name    
    -- (AFTER | BEFORE) (INSERT | UPDATE | DELETE)  
    --      ON table_name FOR EACH ROW    
    --      BEGIN    
    --     --variable declarations    
    --     --trigger code    
    --     END;      

-- Example RUN delimiter  CODE IN TERMINAL

CREATE TABLE my_trigger
( 
    message VARCHAR(100)
);


DELIMITER $$ (RUN in TERMINAL)
CREATE TRIGGER trig1
AFTER INSERT ON employee
FOR EACH ROW BEGIN
    INSERT INTO my_trigger VALUES("Employee added");
END$$ (in TERMINAL)

DELIMITER ; (in TERMINAL)

INSERT INTO employee
VALUES(109, 'Oscar', 'Martinez','1968-04-09','M',690000,102,3);

SELECT * FROM my_trigger;

DELIMITER $$
CREATE
    TRIGGER trig2 BEFORE INSERT
    ON employee
    FOR EACH ROW BEGIN
         IF NEW.sex = 'M' THEN
               INSERT INTO my_trigger VALUES('added male employee');
         ELSEIF NEW.sex = 'F' THEN
               INSERT INTO my_trigger VALUES('added female');
         ELSE
               INSERT INTO my_trigger VALUES('added other employee');
         END IF;
    END$$
DELIMITER ;
INSERT INTO employee
VALUES(111, 'Pam', 'Beesly', '1988-02-19', 'F', 69000, 106, 3);

DROP TRIGGER trig1;
