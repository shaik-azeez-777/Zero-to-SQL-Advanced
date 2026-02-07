# Day 5 – SQL Advanced Basics

## 1. NULL Values

### What is NULL?
- NULL is not zero
- NULL is not an empty string
- It represents missing or unknown data

```sql
SELECT *
FROM customers
WHERE phone_no IS NULL;
```

```sql
SELECT COUNT(state)
FROM customers
WHERE state = '';
```

```sql
UPDATE customers
SET state = NULL
WHERE state = '';
```

```sql
UPDATE customers
SET phone_no = 0
WHERE phone_no IS NULL;
```

---

## 2. DISTINCT

```sql
SELECT DISTINCT trns_type
FROM transactions;
```

---

## 3. CASE Statement

```sql
SELECT column_name,
       CASE
           WHEN salary > 6000 THEN 'High'
           ELSE 'Low'
       END AS salary_category
FROM table_name;
```

---

## 4. CONCAT Function

```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM customers;
```

---

## 5. COALESCE Function

```sql
SELECT COALESCE(tracking_number, internal_id, 'Unknown')
FROM Shipments;
```

---

## 6. ORDER BY & LIMIT

```sql
SELECT *
FROM accounts
ORDER BY acc_type, balance DESC;
```

```sql
SELECT *
FROM customers
LIMIT 5;
```
