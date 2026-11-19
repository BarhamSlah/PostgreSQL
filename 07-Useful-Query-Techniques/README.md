# Part 07 — Useful Query Techniques

**Target time:** 2 hours  
**Goal:** Learn a few useful techniques for clearer everyday queries.

## 1. Column aliases

```sql
SELECT full_name AS student_name, age AS student_age
FROM students;
```

AS gives a result column a temporary, readable name. It does not rename the table's real column.

## 2. CASE

CASE returns a value based on conditions.

```sql
SELECT
    full_name,
    age,
    CASE
        WHEN age < 18 THEN 'Under 18'
        WHEN age < 22 THEN '18 to 21'
        ELSE '22 or older'
    END AS age_group
FROM students;
```

## 3. COALESCE

COALESCE returns the first non-NULL value.

```sql
SELECT full_name, COALESCE(email, 'No email') AS email_display
FROM students;
```

## 4. Subquery

A subquery is a query inside another query.

```sql
SELECT full_name, age
FROM students
WHERE age > (
    SELECT AVG(age)
    FROM students
);
```

This finds students older than the average age.

## 5. CTE introduction

A Common Table Expression (CTE) gives a named temporary result for one query.

```sql
WITH average_age AS (
    SELECT AVG(age) AS value
    FROM students
)
SELECT full_name, age
FROM students
WHERE age > (SELECT value FROM average_age);
```

You do not need advanced CTEs or window functions yet.

## Practice

1. Give readable aliases to selected columns.
2. Use CASE to label students as 'Adult' or 'Under 18'.
3. Use COALESCE to display a message when email is NULL.
4. Find students older than the average age.
5. Rewrite that query using a CTE.

## Checklist

- [ ] I can use aliases.
- [ ] I can write a simple CASE expression.
- [ ] I understand COALESCE.
- [ ] I can read a simple subquery and CTE.
