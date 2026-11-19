# Part 05 — Relationships and JOINs

**Target time:** 5 hours  
**Goal:** Connect related information stored in separate tables.

## 1. Why relationships?

A relational database stores different kinds of information in separate tables. A foreign key connects a row in one table to a row in another.

### One-to-many

One department can have many employees. Each employee belongs to one department.

```text
departments
-----------
department_id (PK)
department_name

       1
       |
       | one department
       |
       *
employees
---------
employee_id (PK)
employee_name
department_id (FK)
```

The foreign key is stored on the many side: employees.department_id.

## 2. Create example tables and data

```sql
CREATE TABLE departments (
    department_id INTEGER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    department_name TEXT NOT NULL
);

CREATE TABLE employees (
    employee_id INTEGER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    employee_name TEXT NOT NULL,
    department_id INTEGER REFERENCES departments(department_id)
);

INSERT INTO departments (department_name)
VALUES ('Engineering'), ('Sales'), ('Support');

INSERT INTO employees (employee_name, department_id)
VALUES
    ('Sara', 1),
    ('Omar', 1),
    ('Lana', 2),
    ('Noor', NULL);
```

## 3. INNER JOIN

Returns only rows that match in both tables.

```sql
SELECT employees.employee_name, departments.department_name
FROM employees
INNER JOIN departments
    ON employees.department_id = departments.department_id;
```

Sara, Omar, and Lana appear. Noor does not have a matching department.

## 4. LEFT JOIN

Returns every row from the left table, even when there is no match on the right.

```sql
SELECT employees.employee_name, departments.department_name
FROM employees
LEFT JOIN departments
    ON employees.department_id = departments.department_id;
```

Noor appears with NULL for department_name.

## 5. Other JOIN types

- RIGHT JOIN: keeps every row from the right table.
- FULL OUTER JOIN: keeps matched and unmatched rows from both sides.
- CROSS JOIN: produces every possible combination of rows.

For everyday work, focus first on INNER JOIN and LEFT JOIN.

## 6. Many-to-many

Example: students can join many courses, and each course can have many students. Use a junction table:

```text
students 1 --- * student_courses * --- 1 courses
```

The junction table stores student_id and course_id, usually with a combined primary key:

```sql
CREATE TABLE student_courses (
    student_id INTEGER REFERENCES students(student_id),
    course_id INTEGER REFERENCES courses(course_id),
    PRIMARY KEY (student_id, course_id)
);
```

## Practice

1. Create customers and orders tables with a foreign key.
2. Insert customers, including one with no orders.
3. Use INNER JOIN to show customers with orders.
4. Use LEFT JOIN to show all customers, including those without orders.
5. Find customers who have no orders using LEFT JOIN and WHERE orders.order_id IS NULL.
6. Explain why a many-to-many relationship needs a junction table.

## Checklist

- [ ] I understand one-to-one, one-to-many, and many-to-many.
- [ ] I can identify the foreign key.
- [ ] I can write INNER JOIN.
- [ ] I can write LEFT JOIN.
- [ ] I understand why unmatched rows appear as NULL.
## Understand the relationship diagram

The symbol `1` means one row; `*` means many rows. In a one-to-many relationship, the foreign key belongs in the table on the many side. Here, many employees can refer to one department.

### How JOIN matches rows

The ON condition tells PostgreSQL which values connect the tables:

`employees.department_id = departments.department_id`

For each employee, PostgreSQL looks for a department with the same department_id.

### INNER JOIN vs LEFT JOIN

Imagine four employees: Sara and Omar belong to Engineering, Lana belongs to Sales, and Noor has no department.

- INNER JOIN returns Sara, Omar and Lana because they have a matching department.
- LEFT JOIN returns all four employees. Noor's department columns are NULL because no matching department exists.

The table written immediately after FROM is the **left table**. LEFT JOIN preserves all rows from that table.

### Why many-to-many needs a junction table

If one student can take many courses and one course can have many students, putting one course_id in students is not enough. A junction table stores one row for each student-course pairing. Its combined primary key prevents the same student from being enrolled in the same course twice.

**Note:** The student_courses example assumes the students and courses tables already exist. Create those two parent tables before creating student_courses.

### Debug a JOIN

1. Check that both tables exist with `\dt`.
2. Check their columns with `\d employees` and `\d departments`.
3. Confirm that the ON columns represent the same kind of identifier.
4. Run each table's SELECT separately.
5. Add the JOIN after confirming the individual data.
