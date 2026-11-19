# Part 08 — Everyday Database Management

**Target time:** 4 hours  
**Goal:** Make safe, basic changes to databases and understand transactions and indexes.

## 1. ALTER TABLE

Add a column:

```sql
ALTER TABLE students
ADD COLUMN phone_number VARCHAR(25);
```

Rename a column:

```sql
ALTER TABLE students
RENAME COLUMN phone_number TO phone;
```

Change a column type (check existing data first):

```sql
ALTER TABLE students
ALTER COLUMN full_name TYPE VARCHAR(150);
```

## 2. Rename and remove objects

```sql
ALTER TABLE students RENAME TO learners;
ALTER TABLE learners DROP COLUMN phone;
```

Be careful: dropping a column removes its data.

## 3. Transactions

A transaction groups statements so they can succeed or fail as one unit.

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 100
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 100
WHERE account_id = 2;

COMMIT;
```

If something goes wrong before COMMIT, use:

```sql
ROLLBACK;
```

For safe practice, try a transaction and ROLLBACK first. Confirm that the data returned to its original state.

## 4. Index basics

An index can help PostgreSQL find rows faster, especially for columns used often in filters or joins. Indexes also take storage and can make inserts/updates/deletes slower.

```sql
CREATE INDEX idx_students_email ON students(email);
```

A primary key and UNIQUE constraint automatically create their supporting unique indexes. Do not add duplicate indexes without a reason.

## 5. Basic inspection

```sql
EXPLAIN
SELECT * FROM students WHERE email = 'sara@example.com';
```

EXPLAIN shows the planned execution strategy. Learn to recognize that it exists; detailed query-plan tuning can wait.

## 6. Backup and restore basics

PostgreSQL commonly provides `pg_dump` and `pg_restore` for backups. These are separate command-line programs, not SQL statements typed at the psql prompt.

- `pg_dump` creates a logical backup.
- `pg_restore` restores backups created in custom/archive formats.
- For a plain SQL dump, you can use psql to execute the dump file.

Practice backup and restore only with a test database and follow the installed PostgreSQL version's documentation.

## Practice

1. Add a column to your practice table.
2. Rename that column.
3. Start a transaction, change data, then ROLLBACK.
4. Repeat the change and COMMIT it.
5. Create an index on a column you search frequently.
6. Run EXPLAIN on a SELECT query.
7. Learn where pg_dump and pg_restore are installed on your computer.

## Checklist

- [ ] I can add and rename columns.
- [ ] I understand BEGIN, COMMIT, and ROLLBACK.
- [ ] I understand the basic purpose and cost of an index.
- [ ] I know what EXPLAIN is for.
- [ ] I know the difference between SQL backup tools and psql commands.
