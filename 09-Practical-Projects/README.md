# Part 09 — Practical Projects

**Target time:** 6 hours  
**Goal:** Combine the SQL skills from earlier parts in realistic tasks.

Do not copy a complete solution first. Design the tables, decide their relationships, and write the queries. Use the requirements below as a checklist.

## Project A — Student management

Create:
- students: student_id, full_name, email
- courses: course_id, course_name
- student_courses: student_id, course_id, enrollment_date

Requirements:
1. Use primary keys and foreign keys.
2. Make student email unique.
3. Insert at least five students and three courses.
4. Enroll students in multiple courses.
5. List all students.
6. Show each student with their courses using JOIN.
7. Include students who are not enrolled in a course using LEFT JOIN.
8. Count students per course.

## Project B — Simple banking database

Create:
- customers: customer_id, full_name, email
- accounts: account_id, customer_id, account_type, balance
- transactions: transaction_id, account_id, amount, transaction_type, created_at

Requirements:
1. Use primary keys and foreign keys.
2. Use NUMERIC for money values.
3. Add NOT NULL and CHECK constraints where appropriate.
4. Insert sample customers and accounts.
5. Display each customer's accounts.
6. Calculate each customer's total balance.
7. Show transactions for one account, newest first.
8. Use a transaction to simulate transferring money between two accounts. Test ROLLBACK before COMMIT.
9. Think about how you would prevent a negative balance.

**Important:** This is a learning model, not production banking software. Real financial systems need additional safeguards, auditing, concurrency handling, and carefully designed transfer logic.

## Project C — Query practice

Using either project database, write queries to:
- Find records matching multiple conditions.
- Sort and limit results.
- Count rows by category.
- Find records with no related rows.
- Use a subquery to compare a value to an average.
- Update one record safely.
- Delete one test record safely.

## Final self-check

Try to complete the projects without following a video step by step. Looking up syntax is fine. The goal is to understand what the query does and why.

- [ ] I can design related tables.
- [ ] I can insert realistic sample data.
- [ ] I can write CRUD queries.
- [ ] I can join tables correctly.
- [ ] I can summarize data with GROUP BY.
- [ ] I can use transactions safely.
- [ ] I can explain the purpose of my constraints.
## How to approach a project

Do not begin by writing every query at once. Design the data first:

1. Identify the nouns (for example, customers, accounts and transactions). These usually become tables.
2. Decide what uniquely identifies each row. This becomes the primary key.
3. Identify how tables connect. Put foreign keys on the many side or use a junction table for many-to-many.
4. Choose data types and constraints.
5. Create parent tables before child tables.
6. Insert a small amount of test data.
7. Test each query separately, then combine queries with JOIN and GROUP BY.

## Suggested order for Project B (banking)

Create customers first, accounts second, and transactions third. This order matters because accounts refer to customers, and transactions refer to accounts.

For the transfer exercise, use BEGIN, subtract from the sender, add to the receiver, and COMMIT only after checking that both operations affected the intended account. Test with ROLLBACK before committing. This is a learning exercise, not production banking logic.

## How to check your project

For every requirement, ask:
- Does the table contain the right columns?
- Are primary keys and foreign keys correct?
- Can invalid data enter?
- Does the query return the expected rows?
- What happens when related data is missing?
- Have I tested the query with more than one record?

There is no single correct naming style for every project. What matters is consistent names, valid relationships, and queries that return the intended result.
