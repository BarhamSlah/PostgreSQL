# Part 03 — Filtering and Sorting

**Target time:** 3 hours  
**Goal:** Find exactly the records you need.

Use the `students` table from Part 02.

## 1. WHERE

```sql
SELECT *
FROM students
WHERE age >= 20;
```

Common comparison operators: `=`, `<>`, `!=`, `>`, `<`, `>=`, `<=`.

## 2. Combine conditions

```sql
SELECT *
FROM students
WHERE age >= 18 AND age <= 25;

SELECT *
FROM students
WHERE age = 20 OR age = 22;

SELECT *
FROM students
WHERE NOT age = 20;
```

Use parentheses when combining AND and OR so the intended logic is clear.

## 3. IN and BETWEEN

```sql
SELECT * FROM students
WHERE age IN (18, 20, 22);

SELECT * FROM students
WHERE age BETWEEN 18 AND 25;
```

BETWEEN includes both endpoints.

## 4. Search text with LIKE and ILIKE

```sql
SELECT * FROM students
WHERE full_name LIKE 'S%';

SELECT * FROM students
WHERE full_name ILIKE '%ahmed%';
```

- `%` means any number of characters.
- `_` means exactly one character.
- LIKE is case-sensitive in PostgreSQL.
- ILIKE is case-insensitive (PostgreSQL-specific).

## 5. NULL

```sql
SELECT * FROM students WHERE email IS NULL;
SELECT * FROM students WHERE email IS NOT NULL;
```

Do not write `email = NULL`. NULL represents an unknown or missing value, so use IS NULL.

## 6. Sort and limit results

```sql
SELECT * FROM students ORDER BY age ASC;
SELECT * FROM students ORDER BY age DESC;
SELECT * FROM students ORDER BY age DESC LIMIT 3;
SELECT * FROM students ORDER BY full_name ASC LIMIT 5 OFFSET 5;
```

ASC is ascending; DESC is descending. Without ORDER BY, row order is not guaranteed.

## 7. DISTINCT

```sql
SELECT DISTINCT age FROM students;
```

Returns unique age values.

## Practice

1. Find students older than 20.
2. Find students whose age is between 18 and 25.
3. Find students whose names begin with A.
4. Find students whose email is missing.
5. Show the three oldest students.
6. Show distinct ages.
7. Show the second page of results with LIMIT and OFFSET.

## Checklist

- [ ] I can filter with WHERE.
- [ ] I can combine conditions.
- [ ] I can search text with LIKE and ILIKE.
- [ ] I understand NULL checks.
- [ ] I can sort, limit, and remove duplicates.
## Understand how filtering works

WHERE tests each row. A row appears in the result only when the condition is TRUE. Rows where the condition is FALSE or UNKNOWN are not returned.

### Operator guide

| Operator | Meaning | Example |
|---|---|---|
| `=` | Equal to | `age = 20` |
| `<>` or `!=` | Not equal to | `age <> 20` |
| `>` / `<` | Greater / less than | `age > 18` |
| `>=` / `<=` | Greater-or-equal / less-or-equal | `age <= 25` |
| `AND` | Both conditions must be true | `age >= 18 AND age <= 25` |
| `OR` | At least one condition must be true | `age = 18 OR age = 20` |
| `IN` | Matches one value in a list | `age IN (18, 20, 22)` |

### LIKE patterns

- `'S%'`: starts with S, followed by any number of characters.
- `'%son'`: ends with son.
- `'%ah%'`: contains ah.
- `'_a%'`: the second character is a.

### Why NULL needs special handling

NULL does not mean zero, an empty string, or the word 'NULL'. It means the value is missing or unknown. A comparison such as `email = NULL` cannot test for missing values correctly. Use `IS NULL` and `IS NOT NULL`.

### Sorting and pagination

ORDER BY sorts the result; it does not change how rows are stored. LIMIT controls how many rows are returned. OFFSET skips rows before returning results. For consistent pagination, sort by a unique column too, for example `ORDER BY age DESC, student_id ASC`.

### Common mistake: AND and OR together

Use parentheses to make your intention clear:

```sql
SELECT *
FROM students
WHERE age >= 18
  AND (age = 20 OR age = 22);
```
