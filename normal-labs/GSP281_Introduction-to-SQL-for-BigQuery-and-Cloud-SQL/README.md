# GSP281 —— Introduction to SQL for BigQuery and Cloud SQL

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [BigQuery](#bigquery)
- [Cloud SQL](#cloud-sql)
- [SQL Basics](#sql-basics)
  - [Databases and Tables](#databases-and-tables)
  - [`SELECT` and `FROM`](#select-and-from)
  - [`WHERE`](#where)
  - [`GROUP BY`](#group-by)
  - [`COUNT`](#count)
  - [`AS`](#as)
  - [`ORDER BY`](#order-by)
  - [`CREATE`](#create)
  - [`DELETE`](#delete)
  - [`INSERT INTO`](#insert-into)
  - [`UNION`](#union)
- [References](#references)

</details>

## Overview

SQL (Structured Query Language) is a standard language for data operations that allows you to ask questions and get insights from structured datasets. It's commonly used in database management and allows you to perform tasks like transaction record writing into relational databases and petabyte-scale data analysis.

## BigQuery

[BigQuery](https://cloud.google.com/bigquery/) is a fully-managed petabyte-scale data warehouse that runs on the Google Cloud. Data analysts and data scientists can quickly query and filter large datasets, aggregate results, and perform complex operations without having to worry about setting up and managing servers. It comes in the form of a command line tool (preinstalled in cloudshell) or a web console—both ready for managing and querying data housed in Google Cloud projects.

## Cloud SQL

[Cloud SQL](https://cloud.google.com/sql/) is a fully-managed database service that makes it easy to set up, maintain, manage, and administer your relational PostgreSQL and MySQL databases in the cloud. There are two formats of data accepted by Cloud SQL: dump files (`.sql`) or CSV files (`.csv`).

## SQL Basics

### Databases and Tables

- Structured datasets have clear rules and are organized into **tables** (data that's formatted in **rows** and **columns**).
- Unstructured data is inoperable with SQL and cannot be stored in BigQuery datasets or tables. e.g. images, audios, videos...etc.
- A Database is a collection of one or more tables.

**Example**:

| **User** | **Price** | **Shipped** |
| :------- | :-------: | :---------: |
| Sean     |    $35    |     Yes     |
| Rocky    |    $50    |     NO      |

As we see, the table has columns for User, Price, and Shipped and two rows that are composed of filled in column values.

### `SELECT` and `FROM`

The most essential keywords are `SELECT` and `FROM`:

- Use `SELECT` to specify what fields you want to pull from your dataset.
- Use `FROM` to specify what table or tables we want to pull our data from.

```sql
SELECT [COLUMN_NAME] FROM [TABLE]
```

### `WHERE`

The `WHERE` keyword is the SQL command that filters tables for specific column values.

```sql
SELECT [COLUMN_NAME] FROM [TABLE] WHERE [CRITERIA]
```

### `GROUP BY`

The `GROUP BY` keyword will aggregate result-set rows that share common criteria (e.g. a column value) and will return all of the unique entries found for such criteria.

```sql
SELECT [COLUMN] FROM [TABLE] GROUP BY [COLUMN];
```

### `COUNT`

The `COUNT()` function will return the number of rows that share the same criteria (e.g. column value). This can be very useful in tandem with a `GROUP BY`.

```sql
SELECT [COLUMN], COUNT(*) FROM [TABLE] GROUP BY [COLUMN];
```

### `AS`

SQL also has an `AS` keyword, which creates an alias of a table or column. An alias is a new name that's given to the returned column or table—whatever AS specifies.

```sql
SELECT [COLUMN], COUNT(*) AS [ALIAS_NAME] FROM [TABLE] GROUP BY [COLUMN];
```

### `ORDER BY`

The `ORDER BY` keyword sorts the returned data from a query in ascending or descending order based on a specified criteria or column value.

```sql
SELECT [COLUMN], COUNT(*) FROM [TABLE] GROUP BY [COLUMN] ORDER BY [COLUMN];
```

### `CREATE`

The `CREATE` command create a database with given name.

```sql
CREATE DATABASE [DATABASE_NAME]
```

### `DELETE`

The `DELETE` keyword is the SQL command that help us with data management for deleting the rows.

```sql
DELETE FROM [TABLE] WHERE [CRITERIA];
```

### `INSERT INTO`

We can also insert values into tables with the `INSERT INTO` keyword.

```sql
INSERT INTO [TABLE] ([COLUMN_NAME], ...) VALUES ([VALUE], ...);
```

### `UNION`

The `UNION` keyword combines the output of two or more `SELECT` queries into a result-set.

```sql
SELECT [COLUMN] FROM [TABLE] WHERE [CRITERIA]
UNION
SELECT [COLUMN] FROM [TABLE] WHERE [CRITERIA]
ORDER BY [COLUMN] DESC;
```

## References

- [BigQuery Documentation](https://cloud.google.com/bigquery/docs)
- [Cloud SQL](https://cloud.google.com/sql/docs)
