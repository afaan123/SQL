
---

# 📘 SQL Learning Guide (Complete for Interviews)

---

## 🟢 1. Basics of SQL

### 📌 What is SQL?

SQL (Structured Query Language) is used to interact with relational databases – to store, retrieve, and manipulate data.

---

### ✅ Basic SQL Syntax

```sql
-- Create a table
CREATE TABLE students (
  id INT,
  name VARCHAR(50),
  age INT
);

-- Insert data
INSERT INTO students (id, name, age)
VALUES
  (1, 'Alice', 20),
  (2, 'Bob', 22),
  (3, 'Charlie', 19);

-- Retrieve data
SELECT * FROM students;

-- Select specific columns
SELECT name, age FROM students;

-- Filter records
SELECT * FROM students WHERE age > 20;

-- Using AND / OR
SELECT * FROM students WHERE age > 18 AND name = 'Bob';

-- Sorting
SELECT * FROM students ORDER BY age DESC;

-- Limit results
SELECT * FROM students LIMIT 2;

-- Update data
UPDATE students SET age = 23 WHERE name = 'Bob';

-- Delete data
DELETE FROM students WHERE id = 3;
```

---

## 🟡 2. Intermediate SQL

### 📌 DISTINCT, IN, BETWEEN, LIKE

```sql
-- Remove duplicates
SELECT DISTINCT age FROM students;

-- WHERE IN
SELECT * FROM students WHERE age IN (20, 22);

-- BETWEEN
SELECT * FROM students WHERE age BETWEEN 18 AND 22;

-- LIKE (Pattern Matching)
SELECT * FROM students WHERE name LIKE 'A%'; -- Starts with A
SELECT * FROM students WHERE name LIKE '%e'; -- Ends with e
```

---

### 📌 Aggregate Functions

```sql
-- COUNT
SELECT COUNT(*) FROM students;

-- SUM, AVG, MIN, MAX
SELECT SUM(age) FROM students;
SELECT AVG(age) FROM students;
SELECT MIN(age), MAX(age) FROM students;
```

---

### 📌 GROUP BY and HAVING

```sql
-- Group and aggregate
SELECT age, COUNT(*) as count
FROM students
GROUP BY age;

-- HAVING (like WHERE but after GROUP BY)
SELECT age, COUNT(*) as count
FROM students
GROUP BY age
HAVING COUNT(*) > 1;
```

---

### 📌 JOINS

#### 🧩 INNER JOIN

```sql
-- Tables
CREATE TABLE courses (
  student_id INT,
  course_name VARCHAR(50)
);

INSERT INTO courses VALUES
  (1, 'Math'),
  (2, 'Science'),
  (1, 'English');

-- Join students with courses
SELECT s.name, c.course_name
FROM students s
INNER JOIN courses c ON s.id = c.student_id;
```

#### 🧩 LEFT JOIN

```sql
SELECT s.name, c.course_name
FROM students s
LEFT JOIN courses c ON s.id = c.student_id;
```

#### 🧩 RIGHT JOIN *(not supported in SQLite)*

```sql
-- Syntax (works in MySQL/PostgreSQL)
SELECT s.name, c.course_name
FROM students s
RIGHT JOIN courses c ON s.id = c.student_id;
```

---

## 🟠 3. Advanced SQL

### 📌 Subqueries

```sql
-- Get students older than average age
SELECT * FROM students
WHERE age > (
  SELECT AVG(age) FROM students
);
```

---

### 📌 Common Table Expressions (CTE)

```sql
WITH adults AS (
  SELECT * FROM students WHERE age >= 18
)
SELECT * FROM adults;
```

---

### 📌 Window Functions

```sql
-- Add row numbers based on age
SELECT name, age,
ROW_NUMBER() OVER (ORDER BY age DESC) AS row_num
FROM students;

-- RANK example
SELECT name, age,
RANK() OVER (ORDER BY age DESC) AS age_rank
FROM students;
```

---

### 📌 CASE Statement

```sql
SELECT name, age,
  CASE
    WHEN age < 20 THEN 'Teen'
    WHEN age BETWEEN 20 AND 22 THEN 'Young Adult'
    ELSE 'Adult'
  END AS category
FROM students;
```

---

## 🔴 4. Interview Practice Tips

### ✅ Practice Platforms

* [LeetCode SQL](https://leetcode.com/problemset/database/)
* [HackerRank SQL](https://www.hackerrank.com/domains/tutorials/10-days-of-sql)
* [StrataScratch](https://www.stratascratch.com/)
* [Mode SQL Tutorial](https://mode.com/sql-tutorial/)
* [DB-Fiddle](https://www.db-fiddle.com/)



## ✅ Summary Cheat Sheet

| Command    | Purpose                   |
| ---------- | ------------------------- |
| `SELECT`   | Read data from a table    |
| `INSERT`   | Add new rows              |
| `UPDATE`   | Modify existing rows      |
| `DELETE`   | Remove rows               |
| `WHERE`    | Filter rows               |
| `JOIN`     | Combine tables            |
| `GROUP BY` | Group rows for aggregates |
| `ORDER BY` | Sort result set           |
| `LIMIT`    | Limit number of rows      |
| `CTE`      | Temporary result set      |
| `CASE`     | If-else logic             |
| `WINDOW`   | Row-wise ranking, stats   |

---

