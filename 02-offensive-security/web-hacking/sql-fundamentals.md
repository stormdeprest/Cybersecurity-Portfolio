# SQL fundamentals

## Databases 101

A database is a structured, organised collection of data (logins, posts, orders, etc.) that can be easily queried, changed and analysed.

**There are two main types:**

- **Relational (SQL):** fixed structure, data in tables (rows/columns), good for consistent, accurate data (e.g. e‑commerce transactions).

- **Non‑relational (NoSQL):** non‑tabular, flexible formats (e.g. JSON/documents), good when data shape varies a lot (e.g. social media content).

**Relational basics:**

- **Table:** collection of related records (e.g. a Books table).

- **Columns:** fields/attributes with a defined data type (string, integer, float/decimal, date/time).

- **Row:** one record in the table (e.g. a single book with id, name, published_date).

**Keys:**

- **Primary key:** a column whose values are unique per row, used to identify each record (e.g. id in Books); only one primary key column per table.

- **Foreign key:** a column that refers to a primary key in another table (e.g. author_id in Books → id in Authors), creating a relationship between tables.

## What is SQL?

**SQL (Structured Query Language)** is a programming language used to query, define, and manipulate data stored in relational databases. It acts as the interface between users and the database through a Database Management System (DBMS).

**Database Management Systems (DBMS):**

A DBMS is software that allows users to retrieve, update, and manage data. It serves as an interface between end users and the database.

**Examples:** MySQL, MongoDB, Oracle Database, MariaDB

## Benefits of SQL

**Why SQL is widely used:**

- Fast: Returns massive batches of data almost instantaneously due to efficient storage and high processing speeds.

- Easy to Learn: Written in plain English, making it much easier to pick up than many programming languages. Highly readable syntax lets you focus on functions rather than complex grammar.

- Reliable: Guarantees data accuracy by enforcing strict structure rules—data must match the defined schema to be inserted.

- Flexible: Provides extensive querying capabilities for complex data analysis tasks efficiently.

## Getting Started with MySQL

**Connect to MySQL:**

`mysql -u root -p`

## Database Statements

**CREATE DATABASE**

Creates a new database.

`CREATE DATABASE database_name;`

**Example:**

`CREATE DATABASE thm_bookmarket_db;`

**SHOW DATABASES**

Lists all databases present in MySQL.

`SHOW DATABASES;`

**USE DATABASE**

Sets the active database for subsequent queries.

`USE thm_bookmarket_db;`

**DROP DATABASE**

Removes a database permanently.

`DROP DATABASE database_name;`

## Table Statements

**CREATE TABLE**

Creates a new table with specified columns and data types within the active database.

```
CREATE TABLE example_table_name (

example_column1 data_type,

example_column2 data_type,

example_column3 data_type
); 
```

**Example:**

```
CREATE TABLE book_inventory (

book_id INT AUTO_INCREMENT PRIMARY KEY,

book_name VARCHAR(255) NOT NULL,

publication_date DATE

);
```

**Column properties:**

- **INT:** Integer data type
- **AUTO_INCREMENT:** Automatically assigns incrementing numbers (1, 2, 3...)
- **PRIMARY KEY:** Unique identifier for each record
- **VARCHAR(255):** Variable character field with max 255 characters
- **NOT NULL:** Field cannot be empty
- **DATE:** Date data type

**SHOW TABLES**

Lists all tables in the currently active database.

`SHOW TABLES;`

**DESCRIBE / DESC**

Shows the structure of a table (columns, data types, keys, etc.).

`DESCRIBE book_inventory;`

or

`DESC book_inventory;`

**ALTER TABLE**

Modifies an existing table structure (add/remove/change columns).

**Add a column:**

```
ALTER TABLE book_inventory
ADD page_count INT;
```

**DROP TABLE**

Removes a table permanently.

`DROP TABLE table_name;`

## CRUD Operations

**CRUD** stands for **Create, Read, Update, and Delete** – the four basic operations for managing data in any database system.

**Access the practice database:**

`USE thm_books;`

## Create Operation (INSERT)

Adds new records to a table.

**Syntax:**

```
INSERT INTO table_name (column1, column2, column3)

VALUES (value1, value2, value3);
```

**Example:**

```
INSERT INTO books (id, name, published_date, description)

VALUES (1, "Android Security Internals", "2014-10-14", "An In-Depth Guide to Android's Security Architecture");
```


## Read Operation (SELECT)

Retrieves data from a table.

**Select all columns:**

`SELECT * FROM books;`

**Select specific columns:**

`SELECT name, description FROM books;`


**Notes:**

- **`*`** retrieves all columns
- Specify column names to retrieve only those columns

## Update Operation (UPDATE)

Modifies existing records in a table.

**Syntax:**

```
UPDATE table_name
SET column_name = new_value
WHERE condition;
```

**Example:**

```
UPDATE books
SET description = "An In-Depth Guide to Android's Security Architecture."
WHERE id = 1;
```

**Important:** Always use `WHERE` clause to specify which row(s) to update, otherwise all rows will be modified.

## Delete Operation (DELETE)

Removes records from a table.

**Syntax:**

```
DELETE FROM table_name
WHERE condition;
```

**Example:**

`DELETE FROM books WHERE id = 1;`

**Important:** Always use `WHERE` clause to specify which row(s) to delete, otherwise all rows will be removed.

## Summary

- **CREATE (INSERT):** Adds new records to a table
- **READ (SELECT):** Retrieves records from a table
- **UPDATE (UPDATE):** Modifies existing data in a table
- **DELETE (DELETE):** Removes records from a table

## SQL Clauses

**Clauses** are parts of SQL statements that specify criteria for data manipulation, retrieval, or sorting.

**Access the practice database:**

`USE thm_books;`

## DISTINCT Clause

Removes duplicate records from query results, returning only unique values.

**Example:**

`SELECT DISTINCT name FROM books;`

**Result:** Returns only unique book names (eliminates duplicate "Ethical Hacking" entries).

## GROUP BY Clause

Aggregates data from multiple records and groups query results by columns. Useful with aggregate functions like COUNT, SUM, AVG.

**Example:**

```
SELECT name, COUNT(*)
FROM books
GROUP BY name;
```

**Result:** Shows each unique book name with the count of how many times it appears in the table.

## ORDER BY Clause

Sorts query results in ascending or descending order.

**Ascending order (ASC):**

```
SELECT *
FROM books
ORDER BY published_date ASC;
```

**Descending order (DESC):**

```
SELECT *
FROM books
ORDER BY published_date DESC;
```

**Notes:**

- **ASC:** Sorts from lowest to highest (oldest to newest for dates)
- **DESC:** Sorts from highest to lowest (newest to oldest for dates)

## HAVING Clause

Filters groups or aggregated results based on a condition. Used with GROUP BY to filter **after** aggregation.

**Difference from WHERE:**

- **WHERE:** Filters rows **before** aggregation
- **HAVING:** Filters groups **after** aggregation

**Example:**

```
SELECT name, COUNT(*)
FROM books
GROUP BY name
HAVING name LIKE '%Hack%';
```

**Result:** Returns only book names containing "Hack" with their counts.

## Summary

- **DISTINCT:** Removes duplicate records
- **GROUP BY:** Groups rows that have the same values (used with aggregate functions)
- **ORDER BY:** Sorts results (ASC/DESC)
- **HAVING:** Filters aggregated results (used after GROUP BY)

## SQL Operators

Operators filter and manipulate data in SQL queries through logic and comparisons.

**Access the practice database:**

`USE thm_books2;`

## Logical Operators

**LIKE** - Matches patterns (use `%` as wildcard):

`SELECT * FROM books WHERE description LIKE "%guide%";`

**AND** - All conditions must be TRUE:

`SELECT * FROM books WHERE category = "Offensive Security" AND name = "Bug Bounty Bootcamp";`

**OR** - At least one condition must be TRUE:

`SELECT * FROM books WHERE name LIKE "%Android%" OR name LIKE "%iOS%";`

**NOT** - Reverses/excludes a condition:

`SELECT * FROM books WHERE NOT description LIKE "%guide%";`

**BETWEEN** - Tests if value is within a range:

`SELECT * FROM books WHERE id BETWEEN 2 AND 4;`

## Comparison Operators

**= (Equal to)** - Exact match:

`SELECT * FROM books WHERE name = "Designing Secure Software";`

**!= (Not equal to)** - Excludes matches:

`SELECT * FROM books WHERE category != "Offensive Security";`

**< (Less than)** - Values less than specified:

`SELECT * FROM books WHERE published_date < "2020-01-01";`

**> (Greater than)** - Values greater than specified:

`SELECT * FROM books WHERE published_date > "2020-01-01";`

**<= (Less than or equal to)** - Values less than or equal to specified:

`SELECT * FROM books WHERE published_date <= "2021-11-15";`

**>= (Greater than or equal to)** - Values greater than or equal to specified:

`SELECT * FROM books WHERE published_date >= "2021-11-02";`

## Quick Reference

- **LIKE** with `%` for wildcards (`%guide%` finds "guide" anywhere)
- **AND/OR/NOT** for combining conditions
- **BETWEEN** for ranges (inclusive)
- **=, !=, <, >, <=, >=** for comparisons

## SQL Functions

Functions help manipulate data and streamline queries.

## String Functions

**CONCAT()** - Combines two or more strings:

`SELECT CONCAT(name, " is a type of ", category, " book.") AS book_info FROM books;`

**GROUP_CONCAT()** - Concatenates data from multiple rows into one field:

```
SELECT category, GROUP_CONCAT(name SEPARATOR ", ") AS books
FROM books
GROUP BY category;
```


**SUBSTRING()** - Extracts part of a string (position, length):

`SELECT SUBSTRING(published_date, 1, 4) AS published_year FROM books;`

**LENGTH()** - Returns number of characters in a string (includes spaces/punctuation):

`SELECT LENGTH(name) AS name_length FROM books;`

## Aggregate Functions

**COUNT()** - Returns total number of records:

`SELECT COUNT(*) AS total_books FROM books;`

**SUM()** - Adds all non-NULL values in a column:

`SELECT SUM(price) AS total_price FROM books;`

**MAX()** - Returns the maximum value in a column:

`SELECT MAX(published_date) AS latest_book FROM books;`

**MIN()** - Returns the minimum value in a column:

`SELECT MIN(published_date) AS earliest_book FROM books;`

## Quick Reference

**String Functions:**
- **CONCAT()** - combine strings
- **GROUP_CONCAT()** - combine rows into one string
- **SUBSTRING()** - extract part of string
- **LENGTH()** - count characters

**Aggregate Functions:**
- **COUNT()** - count rows
- **SUM()** - add values
- **MAX()** - highest value
- **MIN()** - lowest value
