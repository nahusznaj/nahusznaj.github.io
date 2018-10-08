---
layout: article
title: Exploring indexes in SQL
categories: projects
modified: 2018-06-01T16:28:11-04:00
tags: [python, SQL, SQLite]
comments: true
share: true
read_time: true
---

This project explores indexes with SQL and it is part of my course at dataquest.io.

In this project I will explore indexing. I will work with `factbook.db`, a SQLite database that contains information about each country in the world. I'll be working with the facts table in the database. Each row in facts represents a single country, and contains several columns, including:

`name` -- the name of the country.

`area` -- the total land and sea area of the country.

`population` -- the population of the country.

`birth_rate` -- the birth rate of the country.

`created_at` -- the date the record was created.

`updated_at` -- the date the record was updated.


Let's import sqlite and load the database.


IN
```python
import sqlite3
conn = sqlite3.connect("factbook.db")
```
which, if you have the file `factbook.db` in the same directory where you are running python, won't give any output.


Now, let's have a quick look at the first two rows of `facts` table:

IN
```python
conn.execute("SELECT * FROM facts LIMIT 2;").fetchall()
```

OUT
```
[(1, 'af', 'Afghanistan', 652230, 652230, 0, 32564342, 2.32, 38.57, 13.89, 1.51, '2015-11-01 13:19:49.461734', '2015-11-01 13:19:49.461734'), (2, 'al', 'Albania', 28748, 27398, 1350, 3029278, 0.3, 12.92, 6.58, 3.3, '2015-11-01 13:19:54.431082', '2015-11-01 13:19:54.431082')]
```

Using PRAGMA statement with table_info, returns one row for each column in the named table

```python
schema = conn.execute("PRAGMA table_info(facts);").fetchall()
```

Then, let's print out each row in a separate line

IN:
```python
for s in schema:
    print(s)
```

OUT:
```python
(0, 'id', 'INTEGER', 1, None, 1)
(1, 'code', 'varchar(255)', 1, None, 0)
(2, 'name', 'varchar(255)', 1, None, 0)
(3, 'area', 'integer', 0, None, 0)
(4, 'area_land', 'integer', 0, None, 0)
(5, 'area_water', 'integer', 0, None, 0)
(6, 'population', 'integer', 0, None, 0)
(7, 'population_growth', 'float', 0, None, 0)
(8, 'birth_rate', 'float', 0, None, 0)
(9, 'death_rate', 'float', 0, None, 0)
(10, 'migration_rate', 'float', 0, None, 0)
(11, 'created_at', 'datetime', 0, None, 0)
(12, 'updated_at', 'datetime', 0, None, 0)
```

So that's some information about the facts table.

In this project I will explore indexing. The statement `EXPLAIN QUERY PLAN SELECT * FROM facts;` will not return the result of the `SELECT` query, but the high level query plan instead:

```
[(0, 0, 0, 'SCAN TABLE facts')]
```

The `SCAN TABLE facts` is what matters now. `SCAN TABLE` means that every row in entire table (facts) had to be accessed to evaluate the query. Since the `SELECT` query we wrote returns all of the columns and rows in the facts table, the entire table had to be accessed to get the results we requested.

Let's return the query plan for the query that returns all columns and rows where area exceeds 40000:

IN
```python
query_plan_one = conn.execute("EXPLAIN QUERY PLAN SELECT * FROM facts WHERE area > 40000;").fetchall()
print(query_plan_one)
```

OUT
```python
[(2, 0, 0, 'SCAN TABLE facts')]
```


Let's return the query plan for the query that returns all rows and the column "area" where area exceeds 40000:

IN
```python
query_plan_two = conn.execute("EXPLAIN QUERY PLAN SELECT area FROM facts WHERE area > 40000;").fetchall()
print(query_plan_two)
```

OUT
```python
[(2, 0, 0, 'SCAN TABLE facts')]
```


Let's return the query plan for the query that returns the row for the country `Czech Republic`:

IN
```python
query_plan_three = conn.execute("EXPLAIN QUERY PLAN SELECT * FROM facts WHERE name = 'Czech Republic';").fetchall()
print(query_plan_three)
```

OUT
```python
[(2, 0, 0, 'SCAN TABLE facts')]
```


This shows a relevant aspect of the primary key: SQLite has to scan the whole table even # when we are asking to select only when area is greater than 40000. This is because SQLite has to check the whole row to look at the area value. If instead we are selecting # where ID (the primary key) has a value, SQLite will search first where ID is that value and then run the rest of the query.

In terms of programming complexity (time), a binary search on a table using the primary key would be O(log N) time complexity where N is the number of total rows in the table. On the other hand, a full table scan would be O(N) time complexity since each row would have to be accessed. So, if we're working with a database containing millions of rows, binary search would be over a million times faster!

IN
```python
query_plan_four = conn.execute("EXPLAIN QUERY PLAN SELECT * FROM facts WHERE id = 20;").fetchall()
print(query_plan_four)
```

OUT
```python
[(2, 0, 0, 'SEARCH TABLE facts USING INTEGER PRIMARY KEY (rowid=?)')]
```

SQLite uses `rowid` to refer to the primary key of a table. The alias `rowid` will be displayed in the query plan, no matter what you name the primary key column for that table!

In order to make efficient queries, we can create an 'index' table that has the column we want to explore as a primary key, and the id column as a normal column (to then be able to relate with the original column).

Check out https://www.sqlite.org/lang_createindex.html

SQLite is able to efficiently use indexes, as it will decide automatically which indexed # table to scan when a query is executed.

The pros of creating indexes is speed, while the con is the space it takes!

Let's create an explain query plan query without the index table and then one with the index table:

IN
```python
query_plan_six = conn.execute("EXPLAIN QUERY PLAN SELECT * FROM facts WHERE population > 10000;").fetchall()
print(query_plan_six)
```

OUT
```python
[(3, 0, 0, 'SEARCH TABLE facts USING INDEX pop_idx (population>?)')]
```

IN
```python
conn.execute("CREATE INDEX IF NOT EXISTS pop_idx ON facts(population);").fetchall()
```

OUT
```python
[]
```

IN
```python
query_plan_seven = conn.execute("EXPLAIN QUERY PLAN SELECT * FROM facts WHERE population > 10000").fetchall()
print(query_plan_seven)
```

OUT
```python
[(3, 0, 0, 'SEARCH TABLE facts USING INDEX pop_idx (population>?)')]
```

So, the output to the last print: instead of ending in USING INDEX pop_idx (population), the query plan ended in USING INDEX pop_idx (population>?). This is to indicate the granularity of the lookup that SQLite had to do for that index.


To conclude, in this scrip I have explored how SQLite accesses data and how to create  and take advantages of indexes. That's it for now!
