# Part 02 — SQL Basics (CRUD)

**Target time:** 4 hours  
**Goal:** Create tables and confidently perform the four everyday data operations: INSERT, SELECT, UPDATE, DELETE.

## 1. Create a table

A table stores records in rows and describes them with columns.

```sql
CREATE TABLE students (
    student_id INTEGER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    full_name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE,
    age INTEGER,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## 2. Insert records

```sql
INSERT INTO students (full_name, email, age)
VALUES
    ('Sara Ahmed', 'sara@example.com', 20),
    ('Omar Ali', 'omar@example.com', 22);
```

Always name the columns in an INSERT statement. It makes the query easier to read and safer if the table structure changes.

## 3. Read records with SELECT

```sql
SELECT * FROM students;
SELECT full_name, email FROM students;
```

Use `*` while exploring. In application queries, selecting only the columns you need is usually clearer.

## 4. Update records

```sql
UPDATE students
SET age = 21
WHERE student_id = 1;
```

**Safety habit:** First run `SELECT * FROM students WHERE student_id = 1;` and confirm the target row.

Without a WHERE condition, UPDATE changes every row.

## 5. Delete records

```sql
DELETE FROM students
WHERE student_id = 2;
```

First check the matching rows with SELECT. Without WHERE, DELETE removes every row from the table.

## 6. Remove or change database objects

- `ALTER TABLE` changes a table structure (Part 08).
- `TRUNCATE` removes all rows from a table.
- `DROP TABLE` removes the table itself, including its structure.

Do not use DROP or TRUNCATE on data you need.

## Practice

Create the `students` table above, then:

1. Insert at least five students.
2. Display every student.
3. Display only names and email addresses.
4. Change one student's age.
5. Check the row before and after the update.
6. Delete one student by ID.
7. Confirm the deleted row is gone.
8. Explain the difference between DELETE, TRUNCATE, and DROP TABLE.

## Common mistakes

- Forgetting single quotes around text values.
- Using double quotes for text values. In PostgreSQL, double quotes identify names such as columns and tables.
- Forgetting the semicolon.
- Updating or deleting without a WHERE condition.
- Inserting values in the wrong column order when column names are omitted.

## Checklist

- [ ] I can create a table.
- [ ] I can insert one or multiple rows.
- [ ] I can select specific columns.
- [ ] I can update one row safely.
- [ ] I can delete one row safely.
- [ ] I understand DELETE vs TRUNCATE vs DROP.
