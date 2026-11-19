# Part 01 — Getting Started

**Target time:** 2 hours  
**Goal:** Understand PostgreSQL, connect with SQL Shell (psql), and navigate confidently.

## 1. Know the tools

- PostgreSQL: the database server.
- SQL: the language for working with relational data.
- psql: the terminal client that sends SQL to PostgreSQL.
- pgAdmin 4: a graphical client. It is useful, but this course uses psql for hands-on practice.

## 2. Connect using SQL Shell (psql)

When SQL Shell opens, it asks for:
- Server: usually `localhost` for a local installation.
- Database: usually `postgres` for the first connection.
- Port: commonly `5432`, unless you changed it.
- Username: commonly `postgres`, unless you created another role.
- Password: the password configured for that PostgreSQL role.

Press Enter to accept a displayed default. Enter the password when prompted; psql normally does not show password characters while you type.

A successful connection gives you a prompt similar to:

```text
postgres=#
```

The exact prompt can differ. `=#` commonly indicates a superuser; `=>` commonly indicates a normal role.

## 3. Essential psql commands

| Command | Meaning |
|---|---|
| `\l` | List databases |
| `\c postgres` | Connect to database postgres |
| `\dt` | List tables |
| `\d table_name` | Show table columns and details |
| `\dn` | List schemas |
| `\du` | List roles |
| `\conninfo` | Show current connection |
| `\q` | Quit psql |
| `\?` | Help for psql commands |
| `\h CREATE TABLE` | SQL syntax help |

These are **psql meta-commands**, not SQL statements. They start with a backslash and normally do not end with a semicolon.

## 4. Your first SQL commands

```sql
SELECT version();
SELECT current_database();
SELECT current_user;
SELECT now();
```

SQL statements end with a semicolon.

## 5. Create your practice database

```sql
CREATE DATABASE postgres_learning;
```

Then connect to it:

```text
\c postgres_learning
```

## Practice — do these in psql

1. Connect to the default `postgres` database.
2. Display the PostgreSQL version.
3. List all databases.
4. Create `postgres_learning`.
5. Connect to `postgres_learning`.
6. Display the current database and user.
7. Exit psql, then open it and reconnect to your practice database.

## Common problems

- **Password authentication failed:** check that you are using the password for the PostgreSQL role shown in the prompt. The Windows login password is not necessarily the PostgreSQL password.
- **Connection refused:** check that the PostgreSQL server is running and that the host/port are correct.
- **Command does not run:** SQL needs a semicolon. psql meta-commands begin with a backslash.
- **Prompt changes to `postgres_learning-#`:** psql may be waiting for the rest of an unfinished SQL statement. Enter `;` to finish it or use `\r` to clear the query buffer.

## Checklist

- [ ] I can connect through SQL Shell.
- [ ] I know the difference between SQL and psql commands.
- [ ] I can list databases and connect to one.
- [ ] I can identify the current database and user.
- [ ] I can exit and reconnect.
