# DAY 4 – SQL Assignment (Basics)

```sql
-- Fetch all transaction data.

-- Fetch account_number and acc type from all accounts.

-- Fetch customer id and name of all active customers.

-- Fetch customer id and name of all active customers who were born after 2000.

-- Find employees whose salary ranges from 50k to 70k

-- Find customers who have not provided basic information such as address or phone number.

-- Find customers having "oo" in their name.

-- Identify the total no of wire transfer transactions.

-- Identify the unique transaction type.

-- Fetch the first 5 transactions

-- Fetch the inactive customers name, phone no, address and dob. Display the the oldest customer first.

-- Find the customers who are from either "77 Lien Park", "337 Westend Park" or "9 Troy Plaza".

-- Fetch all customers who have "Park" or "Plaza" in their address.

-- Would you like me to help you write the SQL queries for any of these questions?

select * from BRANCH;
select * from CUSTOMERS;
select * from ACCOUNTS;
select * from TRANSACTIONS;
select * from EMPLOYEES;

-- 1)Fetch all transaction data.
select * from transactions;

-- 2)Fetch account_number and acc type from all accounts.
 select account_number,acc_type from accounts;


-- Fetch customer id and name of all active customers who were born after 2000.

select customer_Id , CONCAT(first_Name,' ',last_name),is_active from customers
where is_active = 'true';



-- Find employees whose salary ranges from 50k to 70k
select * from EMPLOYEES;
select * from employees
where salary between 50000 and 70000;


-- Find customers who have not provided basic information such as address or phone number.
select * from CUSTOMERS;

select customer_Id from customers
where address is NULL;


-- Find customers having "oo" in their name.
select * from CUSTOMERS;
SELECT * FROM CUSTOMERS
WHERE first_name like '%oo%' or last_name like '%oo%'
;


-- Identify the total no of wire transfer transactions.
select * from TRANSACTIONS;
select count(trns_type) from transactions
where trns_type = 'wire transfer';


-- Identify the unique transaction type.
select distinct trns_type from transactions;


-- Fetch the first 5 transactions
select * FROM TRANSACTIONS
order by trns_id
limit 5;


-- Fetch the inactive customers name, phone no, address and dob. Display the the oldest customer first.
select concat(first_name , ' ', last_name), phone_no, address, dob from customers
where is_active = 'false'
order by dob asc;

-- Find the customers who are from either "77 Lien Park", "337 Westend Park" or "9 Troy Plaza".
select * from customers
where address in ('77 Lien Park' ,'337 Westend Park','9 Troy Plaza');


-- Fetch all customers who have "Park" or "Plaza" in their address.
select * from customers
where address like '%Park' OR address like '%Plaza'
```