# PostgreSQL  

A quick-reference guide for everyday PostgreSQL use.

---

## Table of Contents

1. [Basic Terminology](#1-basic-terminology)
2. [psql Basics](#2-psql-basics)
3. [CREATE TABLE](#3-create-table)
4. [Data Types](#4-common-data-types)
5. [SERIAL Data Type](#5-serial-data-type)
6. [INSERT](#6-insert)
7. [SELECT](#7-select)
8. [WHERE Clause](#8-where-clause)
9. [UPDATE](#9-update)
10. [DELETE](#10-delete)
11. [ORDER BY](#11-order-by)
12. [LIMIT and OFFSET](#12-limit-and-offset)
13. [GROUP BY](#13-group-by)
14. [HAVING](#14-having)
15. [Aggregate Functions](#15-aggregate-functions)
16. [ALTER TABLE](#16-alter-table)
17. [Constraints](#17-constraints)
18. [Multiple Tables and Foreign Keys](#18-multiple-tables-and-foreign-keys)
19. [Joins](#19-joins)
20. [Many-to-Many Relationships](#20-many-to-many-relationships)
21. [Other Important Things](#21-other-important-things)

---

## 1. Basic Terminology

| Term | Meaning |
|------|---------|
| **Database** | A collection of related tables |
| **Table** | Rows and columns that store data (like a spreadsheet) |
| **Row / Record / Tuple** | A single entry in a table |
| **Column / Field / Attribute** | A named piece of data in each row |
| **Primary Key (PK)** | Column that uniquely identifies each row |
| **Foreign Key (FK)** | Column that references the primary key of another table |
| **Schema** | A namespace inside a database that groups tables (default: `public`) |
| **Query** | A request for data, written in SQL |
| **Index** | A structure that makes lookups faster |
| **NULL** | Missing or unknown value (not the same as 0 or empty string) |
| **CRUD** | Create, Read, Update, Delete (INSERT, SELECT, UPDATE, DELETE) |

> SQL keywords are case-insensitive, but convention is UPPERCASE for keywords and lowercase for names. Every statement ends with `;`.

---

## 2. psql Basics

Connect from the terminal:

```bash
psql -U postgres                  # connect as user postgres
psql -U postgres -d mydb          # connect to a specific database
psql -h localhost -p 5432 -U user -d mydb
```

Useful psql meta-commands (these are not SQL, no semicolon needed):

| Command | What it does |
|---------|--------------|
| `\l` | List databases |
| `\c dbname` | Connect to a database |
| `\dt` | List tables |
| `\d tablename` | Describe a table (columns, keys, constraints) |
| `\dn` | List schemas |
| `\du` | List users/roles |
| `\x` | Toggle expanded output (good for wide rows) |
| `\i file.sql` | Run SQL from a file |
| `\timing` | Show query execution time |
| `\q` | Quit |
| `\?` | Help for psql commands |

Database commands:

```sql
CREATE DATABASE shop;
DROP DATABASE shop;
```

---

## 3. CREATE TABLE

```sql
CREATE TABLE students (
    id        SERIAL PRIMARY KEY,
    name      VARCHAR(100) NOT NULL,
    email     VARCHAR(150) UNIQUE,
    age       INT,
    city      VARCHAR(50) DEFAULT 'Unknown',
    created_at TIMESTAMP DEFAULT NOW()
);
```

Only create if it doesn't exist yet:

```sql
CREATE TABLE IF NOT EXISTS students ( ... );
```

Delete a table:

```sql
DROP TABLE students;
DROP TABLE IF EXISTS students;
DROP TABLE students CASCADE;   -- also drops dependent objects
```

Remove all rows but keep the table:

```sql
TRUNCATE TABLE students;
TRUNCATE TABLE students RESTART IDENTITY;  -- also resets SERIAL counter
```

---

## 4. Common Data Types

| Type | Use for | Example |
|------|---------|---------|
| `INT` / `INTEGER` | Whole numbers | `42` |
| `BIGINT` | Very large whole numbers | `9000000000` |
| `SMALLINT` | Small whole numbers | `12` |
| `NUMERIC(p,s)` / `DECIMAL` | Exact decimals (money) | `NUMERIC(10,2)` -> `1234.56` |
| `REAL` / `DOUBLE PRECISION` | Approximate decimals | `3.14` |
| `VARCHAR(n)` | Text up to n characters | `'Alice'` |
| `CHAR(n)` | Fixed-length text | `'IN'` |
| `TEXT` | Unlimited text | `'Long description...'` |
| `BOOLEAN` | true / false | `TRUE` |
| `DATE` | Date only | `'2026-10-21'` |
| `TIME` | Time only | `'14:30:00'` |
| `TIMESTAMP` | Date and time | `'2026-10-21 14:30:00'` |
| `TIMESTAMPTZ` | Date and time with timezone | `NOW()` |
| `UUID` | Unique identifiers | `gen_random_uuid()` |
| `JSON` / `JSONB` | JSON data (JSONB is faster to query) | `'{"a": 1}'` |
| `ARRAY` | Array of values | `INT[]`, `TEXT[]` |

---

## 5. SERIAL Data Type

`SERIAL` creates an auto-incrementing integer, commonly used for primary keys.

```sql
CREATE TABLE products (
    id    SERIAL PRIMARY KEY,   -- 1, 2, 3, ... automatically
    name  TEXT NOT NULL
);
```

| Type | Range |
|------|-------|
| `SMALLSERIAL` | 1 to 32,767 |
| `SERIAL` | 1 to 2,147,483,647 |
| `BIGSERIAL` | 1 to 9,223,372,036,854,775,807 |

Modern alternative (recommended in new projects):

```sql
id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY
```

Notes:
- Don't insert a value for the serial column; let Postgres do it.
- Deleted rows leave gaps; the counter never goes backwards.

---

## 6. INSERT

```sql
-- One row
INSERT INTO students (name, email, age)
VALUES ('Alice', 'alice@example.com', 21);

-- Multiple rows
INSERT INTO students (name, email, age)
VALUES
    ('Bob',   'bob@example.com',   22),
    ('Carol', 'carol@example.com', 20);

-- Insert and get the new row back
INSERT INTO students (name, age)
VALUES ('Dave', 23)
RETURNING *;          -- or RETURNING id;

-- Insert from another table
INSERT INTO alumni (name, email)
SELECT name, email FROM students WHERE age > 25;

-- Upsert: insert, or update if it already exists
INSERT INTO students (email, name)
VALUES ('alice@example.com', 'Alice Smith')
ON CONFLICT (email)
DO UPDATE SET name = EXCLUDED.name;

-- Insert, or silently skip on conflict
INSERT INTO students (email, name)
VALUES ('alice@example.com', 'Alice')
ON CONFLICT DO NOTHING;
```

---

## 7. SELECT

```sql
SELECT * FROM students;                    -- all columns
SELECT name, age FROM students;            -- specific columns
SELECT DISTINCT city FROM students;        -- unique values only
SELECT name AS student_name FROM students; -- alias
SELECT COUNT(*) FROM students;             -- count rows
SELECT name, age + 1 AS next_age FROM students;  -- expressions
```

String and date helpers:

```sql
SELECT UPPER(name), LOWER(name), LENGTH(name) FROM students;
SELECT name || ' from ' || city AS info FROM students;  -- concatenate
SELECT NOW(), CURRENT_DATE, CURRENT_TIMESTAMP;
SELECT COALESCE(city, 'N/A') FROM students;             -- replace NULL
```

---

## 8. WHERE Clause

Filters rows.

```sql
SELECT * FROM students WHERE age = 21;
SELECT * FROM students WHERE age > 20 AND city = 'Mumbai';
SELECT * FROM students WHERE city = 'Delhi' OR city = 'Pune';
SELECT * FROM students WHERE NOT age = 20;
```

| Operator | Meaning |
|----------|---------|
| `=` | Equal |
| `<>` or `!=` | Not equal |
| `>`, `<`, `>=`, `<=` | Comparisons |
| `AND`, `OR`, `NOT` | Combine conditions |
| `BETWEEN a AND b` | In a range (inclusive) |
| `IN (a, b, c)` | Matches any value in the list |
| `LIKE` | Pattern match (case-sensitive) |
| `ILIKE` | Pattern match (case-insensitive) |
| `IS NULL` / `IS NOT NULL` | Check for NULL |

```sql
SELECT * FROM students WHERE age BETWEEN 18 AND 25;
SELECT * FROM students WHERE city IN ('Mumbai', 'Delhi');
SELECT * FROM students WHERE name LIKE 'A%';      -- starts with A
SELECT * FROM students WHERE name LIKE '%a';      -- ends with a
SELECT * FROM students WHERE name LIKE '%li%';    -- contains li
SELECT * FROM students WHERE name LIKE '_ob';     -- _ = exactly one character
SELECT * FROM students WHERE name ILIKE 'alice';  -- ignore case
SELECT * FROM students WHERE email IS NULL;       -- never use = NULL
```

---

## 9. UPDATE

```sql
UPDATE students SET age = 22 WHERE id = 1;

-- Multiple columns
UPDATE students SET age = 23, city = 'Pune' WHERE name = 'Bob';

-- Using an expression
UPDATE products SET price = price * 1.10;   -- +10% on every row

-- See what changed
UPDATE students SET age = 25 WHERE id = 2 RETURNING *;
```

> **Always use WHERE** with UPDATE, otherwise every row is changed.

---

## 10. DELETE

```sql
DELETE FROM students WHERE id = 3;
DELETE FROM students WHERE age < 18;
DELETE FROM students WHERE id = 4 RETURNING *;   -- see what was deleted
DELETE FROM students;                            -- deletes ALL rows (careful!)
```

> **Always use WHERE** with DELETE. Tip: run a `SELECT` with the same WHERE first to preview affected rows.

---

## 11. ORDER BY

Sorts results. Default is ascending (`ASC`).

```sql
SELECT * FROM students ORDER BY age;              -- ascending
SELECT * FROM students ORDER BY age DESC;         -- descending
SELECT * FROM students ORDER BY city, age DESC;   -- multiple columns
SELECT * FROM students ORDER BY name ASC NULLS LAST;
```

---

## 12. LIMIT and OFFSET

```sql
SELECT * FROM students LIMIT 5;                   -- first 5 rows
SELECT * FROM students ORDER BY age DESC LIMIT 3; -- top 3 oldest
SELECT * FROM students LIMIT 5 OFFSET 10;         -- skip 10, then take 5
```

Pagination formula: `OFFSET = (page_number - 1) * page_size`

```sql
-- Page 3, 10 rows per page
SELECT * FROM students ORDER BY id LIMIT 10 OFFSET 20;
```

---

## 13. GROUP BY

Groups rows with the same value so you can run aggregates on each group.

```sql
-- Students per city
SELECT city, COUNT(*) AS total
FROM students
GROUP BY city;

-- Average age per city
SELECT city, AVG(age) AS avg_age
FROM students
GROUP BY city
ORDER BY avg_age DESC;

-- Multiple grouping columns
SELECT city, age, COUNT(*)
FROM students
GROUP BY city, age;
```

Rule: every column in `SELECT` must either be in `GROUP BY` or be inside an aggregate function.

---

## 14. HAVING

Filters **groups** (after `GROUP BY`). `WHERE` filters **rows** (before grouping).

```sql
SELECT city, COUNT(*) AS total
FROM students
GROUP BY city
HAVING COUNT(*) > 5;

-- WHERE + GROUP BY + HAVING together
SELECT city, AVG(age) AS avg_age
FROM students
WHERE age >= 18
GROUP BY city
HAVING AVG(age) > 20
ORDER BY avg_age DESC
LIMIT 3;
```

Query execution order:

```
FROM -> WHERE -> GROUP BY -> HAVING -> SELECT -> ORDER BY -> LIMIT
```

---

## 15. Aggregate Functions

| Function | Purpose |
|----------|---------|
| `COUNT(*)` | Number of rows |
| `COUNT(col)` | Number of non-NULL values |
| `COUNT(DISTINCT col)` | Number of unique values |
| `SUM(col)` | Total |
| `AVG(col)` | Average |
| `MIN(col)` | Smallest value |
| `MAX(col)` | Largest value |
| `STRING_AGG(col, ', ')` | Join values into one string |

```sql
SELECT COUNT(*), MIN(age), MAX(age), AVG(age) FROM students;
SELECT STRING_AGG(name, ', ') FROM students;
```

---

## 16. ALTER TABLE

```sql
-- Add a column
ALTER TABLE students ADD COLUMN phone VARCHAR(15);

-- Drop a column
ALTER TABLE students DROP COLUMN phone;

-- Rename a column
ALTER TABLE students RENAME COLUMN name TO full_name;

-- Rename a table
ALTER TABLE students RENAME TO learners;

-- Change a column's data type
ALTER TABLE students ALTER COLUMN age TYPE SMALLINT;

-- Set / remove a default
ALTER TABLE students ALTER COLUMN city SET DEFAULT 'Mumbai';
ALTER TABLE students ALTER COLUMN city DROP DEFAULT;

-- Set / remove NOT NULL
ALTER TABLE students ALTER COLUMN email SET NOT NULL;
ALTER TABLE students ALTER COLUMN email DROP NOT NULL;

-- Add / drop constraints
ALTER TABLE students ADD CONSTRAINT age_check CHECK (age >= 0);
ALTER TABLE students ADD CONSTRAINT email_unique UNIQUE (email);
ALTER TABLE students DROP CONSTRAINT age_check;
```

---

## 17. Constraints

Rules that keep your data valid.

| Constraint | Purpose |
|------------|---------|
| `PRIMARY KEY` | Unique and NOT NULL; identifies a row |
| `FOREIGN KEY` | Must match a value in another table |
| `UNIQUE` | No duplicate values |
| `NOT NULL` | Value is required |
| `CHECK` | Value must satisfy a condition |
| `DEFAULT` | Value used if none is given |

```sql
CREATE TABLE employees (
    id        SERIAL PRIMARY KEY,
    email     VARCHAR(150) UNIQUE NOT NULL,
    name      VARCHAR(100) NOT NULL,
    salary    NUMERIC(10,2) CHECK (salary > 0),
    status    VARCHAR(10) DEFAULT 'active',
    age       INT,
    CONSTRAINT age_range CHECK (age BETWEEN 18 AND 65)
);
```

Composite (multi-column) keys and uniqueness:

```sql
PRIMARY KEY (student_id, course_id)
UNIQUE (first_name, last_name)
```

---

## 18. Multiple Tables and Foreign Keys

A foreign key links a row in one table to a row in another. This is a **one-to-many** relationship (one customer has many orders).

```sql
CREATE TABLE customers (
    id    SERIAL PRIMARY KEY,
    name  VARCHAR(100) NOT NULL
);

CREATE TABLE orders (
    id          SERIAL PRIMARY KEY,
    order_date  DATE DEFAULT CURRENT_DATE,
    amount      NUMERIC(10,2),
    customer_id INT NOT NULL,
    FOREIGN KEY (customer_id) REFERENCES customers(id)
);

-- Shorter inline form
CREATE TABLE orders (
    id          SERIAL PRIMARY KEY,
    customer_id INT REFERENCES customers(id)
);
```

Referential actions (what happens when the parent row is deleted or updated):

```sql
customer_id INT REFERENCES customers(id)
    ON DELETE CASCADE      -- delete child rows too
    -- ON DELETE SET NULL  -- set FK to NULL
    -- ON DELETE RESTRICT  -- block the delete
    -- ON DELETE NO ACTION -- default; error if children exist
    ON UPDATE CASCADE
```

Add a foreign key to an existing table:

```sql
ALTER TABLE orders
ADD CONSTRAINT fk_customer
FOREIGN KEY (customer_id) REFERENCES customers(id);
```

Order matters: create the parent table first, and insert parent rows before child rows.

---

## 19. Joins

Combine rows from two or more tables based on a related column.

Sample tables used below: `customers(id, name)` and `orders(id, customer_id, amount)`.

| Join | Returns |
|------|---------|
| `INNER JOIN` | Only rows with a match in both tables |
| `LEFT JOIN` | All rows from the left table, plus matches from the right (NULL if none) |
| `RIGHT JOIN` | All rows from the right table, plus matches from the left |
| `FULL JOIN` | All rows from both tables |
| `CROSS JOIN` | Every combination of rows (cartesian product) |

```sql
-- INNER JOIN: customers who have orders
SELECT c.name, o.amount
FROM customers c
INNER JOIN orders o ON c.id = o.customer_id;

-- LEFT JOIN: all customers, even those with no orders
SELECT c.name, o.amount
FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id;

-- Find customers with NO orders
SELECT c.name
FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id
WHERE o.id IS NULL;

-- RIGHT JOIN
SELECT c.name, o.amount
FROM customers c
RIGHT JOIN orders o ON c.id = o.customer_id;

-- FULL JOIN
SELECT c.name, o.amount
FROM customers c
FULL JOIN orders o ON c.id = o.customer_id;

-- CROSS JOIN
SELECT * FROM sizes CROSS JOIN colors;

-- Joining 3 tables
SELECT c.name, o.id AS order_id, p.name AS product
FROM customers c
JOIN orders o       ON c.id = o.customer_id
JOIN order_items oi ON o.id = oi.order_id
JOIN products p     ON oi.product_id = p.id;

-- Join + aggregate
SELECT c.name, COUNT(o.id) AS order_count, SUM(o.amount) AS total_spent
FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id
GROUP BY c.name
ORDER BY total_spent DESC;

-- USING shortcut (when column names are identical)
SELECT * FROM orders JOIN customers USING (customer_id);
```

Tip: `JOIN` alone means `INNER JOIN`. Use short table aliases (`c`, `o`) to keep queries readable.

---

## 20. Many-to-Many Relationships

When many rows on one side relate to many on the other (students and courses), use a **junction table** (also called a bridge or linking table) that holds a foreign key to each side.

```sql
CREATE TABLE students (
    id   SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);

CREATE TABLE courses (
    id    SERIAL PRIMARY KEY,
    title VARCHAR(100) NOT NULL
);

-- Junction table
CREATE TABLE enrollments (
    student_id  INT REFERENCES students(id) ON DELETE CASCADE,
    course_id   INT REFERENCES courses(id)  ON DELETE CASCADE,
    enrolled_on DATE DEFAULT CURRENT_DATE,
    PRIMARY KEY (student_id, course_id)   -- prevents duplicate pairs
);
```

Insert data:

```sql
INSERT INTO students (name) VALUES ('Alice'), ('Bob');
INSERT INTO courses (title) VALUES ('SQL'), ('Python');

INSERT INTO enrollments (student_id, course_id)
VALUES (1, 1), (1, 2), (2, 1);
```

Query across all three tables:

```sql
-- Courses for each student
SELECT s.name, c.title
FROM students s
JOIN enrollments e ON s.id = e.student_id
JOIN courses c     ON c.id = e.course_id;

-- Students in a given course
SELECT s.name
FROM students s
JOIN enrollments e ON s.id = e.student_id
JOIN courses c     ON c.id = e.course_id
WHERE c.title = 'SQL';

-- Number of students per course
SELECT c.title, COUNT(e.student_id) AS students
FROM courses c
LEFT JOIN enrollments e ON c.id = e.course_id
GROUP BY c.title;
```

Relationship summary:

| Type | Example | How |
|------|---------|-----|
| One-to-One | user and profile | FK with `UNIQUE` |
| One-to-Many | customer and orders | FK on the "many" side |
| Many-to-Many | students and courses | Junction table with two FKs |

---

## 21. Other Important Things

### Indexes (speed up searches)

```sql
CREATE INDEX idx_students_city ON students(city);
CREATE UNIQUE INDEX idx_students_email ON students(email);
DROP INDEX idx_students_city;
```

### Views (saved queries)

```sql
CREATE VIEW active_students AS
SELECT id, name FROM students WHERE age >= 18;

SELECT * FROM active_students;
DROP VIEW active_students;
```

### Subqueries

```sql
-- Students older than the average
SELECT * FROM students
WHERE age > (SELECT AVG(age) FROM students);

-- Customers who placed at least one order
SELECT * FROM customers
WHERE id IN (SELECT customer_id FROM orders);

-- EXISTS
SELECT * FROM customers c
WHERE EXISTS (SELECT 1 FROM orders o WHERE o.customer_id = c.id);
```

### CTE (WITH clause: readable temporary result)

```sql
WITH big_orders AS (
    SELECT * FROM orders WHERE amount > 1000
)
SELECT customer_id, COUNT(*) FROM big_orders GROUP BY customer_id;
```

### Set operations

```sql
SELECT name FROM students
UNION            -- combine, remove duplicates (UNION ALL keeps them)
SELECT name FROM teachers;

-- also: INTERSECT (in both), EXCEPT (in first but not second)
```

### CASE (if/else in SQL)

```sql
SELECT name,
    CASE
        WHEN age < 18 THEN 'Minor'
        WHEN age < 60 THEN 'Adult'
        ELSE 'Senior'
    END AS category
FROM students;
```

### Transactions (all-or-nothing)

```sql
BEGIN;
UPDATE accounts SET balance = balance - 500 WHERE id = 1;
UPDATE accounts SET balance = balance + 500 WHERE id = 2;
COMMIT;      -- save changes
-- ROLLBACK; -- undo everything since BEGIN
```

### Date and time

```sql
SELECT NOW();                                  -- current timestamp
SELECT CURRENT_DATE;                           -- today
SELECT CURRENT_DATE + INTERVAL '7 days';       -- 7 days from now
SELECT EXTRACT(YEAR FROM created_at) FROM students;
SELECT DATE_TRUNC('month', created_at) FROM students;
SELECT AGE(NOW(), created_at) FROM students;
```

### Users and permissions

```sql
CREATE USER dev WITH PASSWORD 'secret';
GRANT SELECT, INSERT ON students TO dev;
GRANT ALL PRIVILEGES ON DATABASE shop TO dev;
REVOKE INSERT ON students FROM dev;
```

### Backup and restore (run in the terminal, not in psql)

```bash
pg_dump -U postgres mydb > backup.sql          # backup
psql -U postgres -d mydb < backup.sql          # restore
pg_dump -U postgres -Fc mydb > backup.dump     # compressed backup
pg_restore -U postgres -d mydb backup.dump     # restore compressed
```

### Import / export CSV

```sql
\copy students TO 'students.csv' CSV HEADER
\copy students FROM 'students.csv' CSV HEADER
```

### Performance: EXPLAIN

```sql
EXPLAIN SELECT * FROM students WHERE city = 'Pune';
EXPLAIN ANALYZE SELECT * FROM students WHERE city = 'Pune';  -- actually runs it
```

---

## Quick Tips and Common Mistakes

- Forgot the semicolon: psql waits with a `-#` prompt. Type `;` to finish.
- Use **single quotes** for text values (`'Alice'`); double quotes are for identifiers.
- Test `UPDATE` / `DELETE` with a `SELECT` first.
- Use `IS NULL`, never `= NULL`.
- Use `NUMERIC` (not `FLOAT`) for money.
- Add indexes on columns you filter or join on often (including foreign keys).
- Wrap risky changes in `BEGIN; ... ROLLBACK;` to test safely.

---

## One-Page Summary

```sql
-- CREATE
CREATE TABLE t (id SERIAL PRIMARY KEY, name TEXT NOT NULL);

-- READ
SELECT col FROM t WHERE cond GROUP BY col HAVING cond ORDER BY col LIMIT n;

-- INSERT
INSERT INTO t (name) VALUES ('x');

-- UPDATE
UPDATE t SET name = 'y' WHERE id = 1;

-- DELETE
DELETE FROM t WHERE id = 1;

-- ALTER
ALTER TABLE t ADD COLUMN age INT;

-- JOIN
SELECT * FROM a JOIN b ON a.id = b.a_id;

-- DROP
DROP TABLE t;
```
