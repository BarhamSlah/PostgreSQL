# Part 06 — Aggregate Functions

**Target time:** 2 hours  
**Goal:** Calculate summaries from multiple rows.

## 1. Common aggregate functions

| Function | Purpose |
|---|---|
| COUNT(*) | Count rows |
| SUM(column) | Add values |
| AVG(column) | Calculate average |
| MIN(column) | Smallest value |
| MAX(column) | Largest value |

Example:

```sql
SELECT
    COUNT(*) AS student_count,
    AVG(age) AS average_age,
    MIN(age) AS youngest,
    MAX(age) AS oldest
FROM students;
```

Most aggregate functions ignore NULL values. COUNT(*) counts rows; COUNT(column) counts non-NULL values in that column.

## 2. GROUP BY

GROUP BY creates one result row for each group.

```sql
SELECT age, COUNT(*) AS number_of_students
FROM students
GROUP BY age
ORDER BY age;
```

## 3. HAVING

WHERE filters rows before grouping. HAVING filters groups after grouping.

```sql
SELECT age, COUNT(*) AS number_of_students
FROM students
GROUP BY age
HAVING COUNT(*) >= 2;
```

## Practice

1. Count all students.
2. Calculate the average age.
3. Find the minimum and maximum age.
4. Count students for each age.
5. Show only age groups containing at least two students.
6. Explain WHERE vs HAVING.

## Checklist

- [ ] I can use COUNT, SUM, AVG, MIN, and MAX.
- [ ] I understand GROUP BY.
- [ ] I understand WHERE vs HAVING.
