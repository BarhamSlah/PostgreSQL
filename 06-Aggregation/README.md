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
## Understand aggregate results

An aggregate function takes values from multiple rows and returns a summary.

Example: if ages are 18, 20 and 22, AVG(age) is 20, MIN(age) is 18 and MAX(age) is 22.

### COUNT(*) vs COUNT(column)

- `COUNT(*)` counts every row.
- `COUNT(email)` counts only rows where email is not NULL.

Most aggregate functions ignore NULL values. This is important when calculating averages or totals.

### What GROUP BY does

GROUP BY puts rows with the same grouping value into a group. The query then returns one summary row per group. For example, grouping by age and counting produces one row for each distinct age.

### WHERE vs HAVING

The order to remember is:

`FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY`

- WHERE removes individual rows before groups are calculated.
- HAVING removes groups after the aggregate calculation.

Use WHERE for conditions on individual records; use HAVING for conditions involving a group or aggregate.
