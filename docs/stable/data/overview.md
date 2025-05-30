---
layout: docu
redirect_from:
- /docs/data/overview
title: Importing Data
---

The first step to using a database system is to insert data into that system.
DuckDB can directly connect to [many popular data sources]({% link docs/stable/data/data_sources.md %}) and offers several data ingestion methods that allow you to easily and efficiently fill up the database.
On this page, we provide an overview of these methods so you can select which one is best suited for your use case.

## `INSERT` Statements

`INSERT` statements are the standard way of loading data into a database system. They are suitable for quick prototyping, but should be avoided for bulk loading as they have significant per-row overhead.

```sql
INSERT INTO people VALUES (1, 'Mark');
```

For a more detailed description, see the [page on the `INSERT` statement]({% link docs/stable/data/insert.md %}).

## File Loading: Relative Paths

Use the configuration option [`file_search_path`]({% link docs/stable/configuration/overview.md %}#local-configuration-options) to configure to which “root directories” relative paths are expanded on.
If `file_search_path` is not set, the working directory is used as the basis for relative paths.

## File Formats

### CSV Loading

Data can be efficiently loaded from CSV files using several methods. The simplest is to use the CSV file's name:

```sql
SELECT * FROM 'test.csv';
```

Alternatively, use the [`read_csv` function]({% link docs/stable/data/csv/overview.md %}) to pass along options:

```sql
SELECT * FROM read_csv('test.csv', header = false);
```

Or use the [`COPY` statement]({% link docs/stable/sql/statements/copy.md %}#copy--from):

```sql
COPY tbl FROM 'test.csv' (HEADER false);
```

It is also possible to read data directly from **compressed CSV files** (e.g., compressed with [gzip](https://www.gzip.org/)):

```sql
SELECT * FROM 'test.csv.gz';
```

DuckDB can create a table from the loaded data using the [`CREATE TABLE ... AS SELECT` statement]({% link docs/stable/sql/statements/create_table.md %}#create-table--as-select-ctas):

```sql
CREATE TABLE test AS
    SELECT * FROM 'test.csv';
```

For more details, see the [page on CSV loading]({% link docs/stable/data/csv/overview.md %}).

### Parquet Loading

Parquet files can be efficiently loaded and queried using their filename:

```sql
SELECT * FROM 'test.parquet';
```

Alternatively, use the [`read_parquet` function]({% link docs/stable/data/parquet/overview.md %}):

```sql
SELECT * FROM read_parquet('test.parquet');
```

Or use the [`COPY` statement]({% link docs/stable/sql/statements/copy.md %}#copy--from):

```sql
COPY tbl FROM 'test.parquet';
```

For more details, see the [page on Parquet loading]({% link docs/stable/data/parquet/overview.md %}).

### JSON Loading

JSON files can be efficiently loaded and queried using their filename:

```sql
SELECT * FROM 'test.json';
```

Alternatively, use the [`read_json_auto` function]({% link docs/stable/data/json/overview.md %}):

```sql
SELECT * FROM read_json_auto('test.json');
```

Or use the [`COPY` statement]({% link docs/stable/sql/statements/copy.md %}#copy--from):

```sql
COPY tbl FROM 'test.json';
```

For more details, see the [page on JSON loading]({% link docs/stable/data/json/overview.md %}).

### Returning the Filename

Since DuckDB v1.3.0, the CSV, JSON and Parquet readers support the `filename` virtual column:

```sql
COPY (FROM (VALUES (42), (43)) t(x)) TO 'test.parquet';
SELECT *, filename FROM 'test.parquet';
```

## Appender

In several APIs (C, C++, Go, Java, and Rust), the [Appender]({% link docs/stable/data/appender.md %}) can be used as an alternative for bulk data loading.
This class can be used to efficiently add rows to the database system without using SQL statements.
