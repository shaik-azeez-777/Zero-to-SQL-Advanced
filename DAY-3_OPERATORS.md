# DAY-3 OPERATORS

```sql
---getting more familiar with Foundation
select * from BRANCH;
select * from CUSTOMERS;
select * from ACCOUNTS;
select * from TRANSACTIONS;
select * from EMPLOYEES;

select ---columns either one / all * 
from ---from which table ? we need to specify table name
where --- to filter conditions like i need records from branch bangalore

----alias----
table alias , column alias

select branch_name as bn from branch b ---ALIAS = SHORTNAME here i used alias for both table and column 
where branch_code = 'BR1';



--------------------------------OPERATORS---------------------------------
LOGICAL OPERATORS:

AND
OR 
NOT
BETWEEN
LIKE (WILD CARDS %,_)

                ----TRUTH TABLE----
Condition A	|Condition B	|AND Result	  |  OR Result
TRUE	      TRUE	         TRUE (Pass)	TRUE (Pass)
TRUE	      FALSE	         FALSE (Fail)	TRUE (Pass)
FALSE	      TRUE	         FALSE (Fail)	TRUE (Pass)
FALSE	      FALSE	         FALSE (Fail)	FALSE (Fail


TRUE AND TRUE -> TRUE
TRUE AND FALSE -> FALSE
FALSE AND TRUE ->FLASE
FALSE AND FALSE ->FALSE

TRUE OR TRUE -> TRUE
TRUE OR FALSE -> TRUE
FALSE OR TRUE ->TRUE
FALSE OR FALSE ->FALSE


--1) WRITE A QUERY TO FETCH EMPLOYEE NAME,SALARY GREATER THAN 50000 AND BRANCH_CODE IS BR1?

select concat(first_name,' ',last_name) as employee_name, salary 
from employees
where salary > 50000
	and branch_code = 'BR1';

--2)"I need a list of all employees who are in Branch BR1. However, I only want to see them if they earn less than 40,000 OR more than 90,000."

select * from employees
where branch_code = 'br1'
and (salary < 40000 or salary > 90000); ----if the logic is inside the parantheses it will the first priority else AND is first , then or 

*/3)"I need a list of employees who work in Branch 'BR1'. 
From that branch, I only want to see people whose Last Name is 'Diggin' OR anyone (still in BR1) who earns more than 90,000."--/*

select * from employees
where branch_code = 'br1'
and (last_name like 'Diggin' or salary > 90000);


4)"I want to find employees who are either in Branch 'BR1' earning over 80,000 OR in Branch 'BR2' earning over 20,000."

select * from employees
where (branch_code = 'br1'
and salary > 80000) or (branch_code = 'br2' and salary > 20000);

5)"I want a list of employees who belong to Branch 'BR2'. However, within that branch, 
I only want to see people if their Last Name is 'McWard' OR if they earn more than 60,000."

select * from employees
where branch_code = 'br2' and (last_name like 'McWard' or salary > 60000);


6)The Request:
"I need a list of employees who are in Branch 'BR1'. Inside that branch, I only want people who meet one of these two rules:

They earn exactly 39,000.

Their First Name is 'Meredith'."

select * from employees
where branch_code = 'br1' and (salary = 39000 or first_name like 'Meredith');


7) "I need a list of employees in Branch 'BR1' who meet either of these conditions:

Their Last Name starts with 'Mc' (like McNuff or McGiffie).

Their Salary is between 60,000 and 70,000 (inclusive)."

select * from employees
where (branch_code = 'br1' and last_name like 'Mc%') or (salary between 60000 and 70000);



------COMPARISON OPERATORS-----
<,>,<=,>=,<>,=

--Find all employees who are in Branch 'BR1' and have a salary greater than 80,000.
SELECT 
BRANCH_CODE,SALARY from employees
where branch_code = 'BR1' 
	and salary > 80000;

--Write a query to find all employees who are NOT in branch 'BR1'.
SELECT 
BRANCH_CODE,SALARY from employees
where branch_code != 'BR1'


--Write a query to find all employees who earn 30,000 or more.

select * from employees
where salary >= 30000;


--Find employees who are in branch 'BR1' AND whose salary is less than 40,000.

select * from employees
where branch_code = 'BR1' AND salary < 40000;



-----------NOT and like-----------------
NOT can be used as :
!=,<>,NOT

LIKE can be used as :
like 'wildcards' %,_
ex: firs_name like 'a%' this means start with a first_name no matter how many letter can be later
	first_name not like 'a%' this means names which not starts with a

ex: for '_' wildcard first_name like 'a___z' means if need only name where total letters count is 5 and starts with A and ends with Z
	first_name like '_____' means it need names with exact 5 letters
	


NOT is often used with IN, BETWEEN, or NULL (e.g., IS NOT NULL).

--not is like a vise versa if condition is true it returns false , if false returns true

--BRANCH_CODE is NOT 'BR1'

--AND SALARY is NOT between 40000 and 60000

--AND FIRST_NAME is exactly 5 letters (Use _____)

select * from employees
where (not branch_code = 'BR1'
AND SALARY NOT BETWEEN 40000 AND 60000 ) AND (FIRST_NAME LIKE '_____');
---HERE FIVE UNDERSCORES MEANS THE FIRST_NAME SIZE IS EXACTLY 5 LETTERS.
---AND ALSO IF WRITE LIKE THIS ('______%') AFTER 5 IT CAN BE 6,7,8,9 MANY OR ALL 


1)The Scenario:
You are looking for employees to help with a weekend shift. You want a list of employees who meet both of these criteria:
They are NOT in Branch 'BR1'.
They meet either of these specific sub-conditions:
Their salary is BETWEEN 30000 and 50000.
Their first name starts with any letter, but the second letter must be 'a' (like "Raleigh" or "Carlotta").

sElect * FROM EMPLOYEES
where branch_code <> 'BR1' and (salary between 30000 and 50000 or first_name like '_a%');--here <> means NOT

2)The Request:
"I want to find employees who are NOT in Branch 'BR2', but I also want to exclude anyone whose Last Name starts with 'M'."

Goal: You want people who are in any branch except BR2, and their names cannot start with M.

SELECT * FROM EMPLOYEES
WHERE NOT BRANCH_CODE = 'BR2'
or LAST_NAME LIKE 'M%';



                   -------------BETWEEN------------
---BETWEEN is used within specific range including start and end values---

Write a single query to find employees who meet these three criteria:

1)Their Salary is between 35,000 and 75,000.

2)Their Hire Date is between '2022-01-01' and '2023-12-31'.

3)Their Last Name is NOT between the letters 'A' and 'M' (This means you want people whose names start with N, O, P... all the way to Z).

SELECT * FROM EMPLOYEES
WHERE SALARY BETWEEN 35000 AND 75000;


SELECT * FROM EMPLOYEES
WHERE LAST_NAME NOT BETWEEN 'A' AND 'M';


----arithmetic operators (+,-,*,/,%)-------


-- 1. Create the table
CREATE TABLE applications (
    application_id INT PRIMARY KEY,
    job_title VARCHAR(100),
    company_name VARCHAR(100),
    offered_salary INT,
    application_date DATE
);

-- 2. Insert practice values
INSERT INTO applications (application_id, job_title, company_name, offered_salary, application_date)
VALUES 
(1, 'Data Analyst', 'TechCorp', 65000, '2026-01-10'),
(2, 'SQL Developer', 'DataSystems', 82000, '2026-01-12'),
(3, 'Junior Engineer', 'CloudNet', 55000, '2026-01-15'),
(4, 'BI Specialist', 'Insightly', 95000, '2026-01-18'),
(5, 'Database Admin', 'StoreSafe', 72000, '2026-01-20');

select * from applications;

SELECT
	JOB_TITLE,
	OFFERED_SALARY,
	(OFFERED_SALARY - 5000) AS TAKE_HOME_PAY,
	(OFFERED_SALARY / 52) AS WEEKLY_PAY
FROM
	APPLICATIONS;


2)

📝 The Challenge:
Write a query that selects the company_name and then creates those three calculated columns with the exact names mentioned above.

Rules for your SQL:

Use * 0.20 for the 20% tax.

Use parentheses () to make sure your math stays organized.

Give every calculation an AS alias.

select * from applications;


SELECT 
    company_name,
    (offered_salary * 0.20) AS tax_cut,
    (2000 - 1500) AS net_bonus,
    (offered_salary + (2000 - 1500) - (offered_salary * 0.20)) AS final_total
FROM applications;

select (95000-55000) as salary_gap from applications;
```