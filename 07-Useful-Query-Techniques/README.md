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
## Understand each technique

- **Alias (AS):** gives a column or expression a readable label in the query result. It does not change the table definition.
- **CASE:** works like if / else if / else. PostgreSQL checks WHEN conditions from top to bottom and returns the result for the first true condition.
- **COALESCE:** checks values from left to right and returns the first value that is not NULL. The values should have compatible types.
- **Subquery:** a query nested inside another query. The inner query supplies a value or set of rows used by the outer query.
- **CTE (WITH):** gives a named result that can be referenced by the main query. It can make a long query easier to read; it is not automatically faster than a subquery.

### Read the average-age example

The inner query `SELECT AVG(age) FROM students` calculates one number. The outer query returns students whose age is greater than that number.

### Common mistakes

- Forgetting END in CASE.
- Comparing a value with NULL using = instead of IS NULL.
- Returning incompatible data types from different CASE branches.
- Using a subquery that returns multiple rows where the outer comparison expects one value.
