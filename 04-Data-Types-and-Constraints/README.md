# Part 04 — Data Types and Constraints

**Target time:** 3 hours  
**Goal:** Choose suitable column types and protect the correctness of stored data.

## 1. Common PostgreSQL data types

| Type | Use |
|---|---|
| INTEGER | Whole numbers |
| BIGINT | Larger whole numbers |
| NUMERIC(10,2) | Exact decimal values, such as money |
| VARCHAR(n) | Text with a maximum length |
| TEXT | Text without a declared length limit |
| BOOLEAN | TRUE or FALSE |
| DATE | Calendar date |
| TIMESTAMP | Date and time without time zone |
| TIMESTAMPTZ | Date and time with time zone handling |

For financial amounts, prefer NUMERIC over FLOAT/REAL because NUMERIC stores exact decimal values.

## 2. Constraints

Constraints are rules that PostgreSQL checks when data is inserted or changed.

- PRIMARY KEY: uniquely identifies each row; cannot be NULL.
- FOREIGN KEY: requires a matching referenced row (unless nullable).
- UNIQUE: prevents duplicate non-NULL values; PostgreSQL normally allows multiple NULLs.
- NOT NULL: requires a value.
- CHECK: requires a condition to be true.
- DEFAULT: supplies a value when one is not provided.

## 3. Example

```sql
CREATE TABLE accounts (
    account_id INTEGER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    owner_name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE,
    balance NUMERIC(12, 2) NOT NULL DEFAULT 0,
    is_active BOOLEAN NOT NULL DEFAULT TRUE,
    CHECK (balance >= 0)
);
```

## 4. Identity columns

`GENERATED ALWAYS AS IDENTITY` asks PostgreSQL to generate values for the column. It is the modern standard approach for auto-generated integer identifiers.

You may also see SERIAL in older tutorials. Understand it, but prefer identity columns for new tables.

## 5. Foreign key example

```sql
CREATE TABLE departments (
    department_id INTEGER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    department_name TEXT NOT NULL UNIQUE
);

CREATE TABLE employees (
    employee_id INTEGER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    employee_name TEXT NOT NULL,
    department_id INTEGER REFERENCES departments(department_id)
);
```

An employee's department_id must refer to an existing department, or be NULL because the column allows it.

## Practice

1. Create a products table with an identity primary key.
2. Add a non-empty product name using NOT NULL.
3. Add a non-negative price using NUMERIC and CHECK.
4. Add a unique SKU.
5. Create categories and products with a foreign key.
6. Try inserting a duplicate SKU and an invalid negative price. Read the errors.
7. Test what happens when you insert NULL into a NOT NULL column.

## Checklist

- [ ] I can choose common data types.
- [ ] I understand PRIMARY KEY and FOREIGN KEY.
- [ ] I can use UNIQUE, NOT NULL, CHECK, and DEFAULT.
- [ ] I understand how NULL behaves with UNIQUE.
- [ ] I can read a constraint error.
## How to choose a data type

Choose a type based on the kind of value, not just how the value looks.

- Use INTEGER for counts and ordinary whole-number identifiers.
- Use BIGINT when the possible whole-number range is much larger.
- Use NUMERIC(12,2) for exact decimal amounts such as money.
- Use TEXT for general text; use VARCHAR(n) when you want a maximum length.
- Use BOOLEAN for true/false facts.
- Use DATE for a date without a time.
- Use TIMESTAMPTZ for a moment in time where time-zone-aware handling matters.

### Constraint example in plain English

`CHECK (balance >= 0)` means PostgreSQL rejects a row if its balance is negative. A constraint is a rule enforced by the database, not merely a note for the programmer.

### Primary key vs UNIQUE

A primary key identifies a row. A table has one primary key constraint (which may contain multiple columns). A table can have several UNIQUE constraints. A primary key cannot contain NULL. By default, PostgreSQL UNIQUE constraints allow more than one NULL because NULL values are not treated as equal; PostgreSQL also supports special NULL uniqueness options, but those are not needed for this beginner course.

### Foreign key in plain English

If employees.department_id references departments.department_id, PostgreSQL checks that a non-NULL department_id in employees exists in departments. This prevents an employee from pointing to a department that does not exist.

### Read a constraint error

If you try to insert a duplicate email, PostgreSQL reports a unique-constraint violation. If you insert a negative balance, the CHECK constraint fails. These errors mean the database protected the data. Correct the supplied value or the table design; do not remove a useful constraint just to hide the error.
