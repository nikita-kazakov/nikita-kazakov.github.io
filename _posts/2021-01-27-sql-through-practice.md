---
title: Practicing SQL by Examples.
date: 2021-01-27
layout: post
permalink: /sql-by-examples/
tags: 
    - software development
---

Bottom Line - Practice SQL by solving real problems.

{% include toc %}

# Chinook Sample Database
I'm going to use a modified [Chinook Sample Database](https://github.com/nikita-kazakov/chinook-sample-database) that I created for the examples below.
Because I'm working with Ruby on Rails, I created a Rails project that sets up all the Chinook tables and data.

I modified the tables slightly to make them fit the Rails standard by:

- pluralizing table names.
- renaming the primary key in each table to 'id'.
- changing column names to lowercase and adding underscores between words (snake case).
- adding Rails timestamps to each table (created_at and updated_at)

The [original Chinook Database](https://github.com/lerocha/chinook-database) is also available.

# SELECT

You're going to fetch data using the select statement in SQL. Select is *what you want* SQL to do for you.
Let's try asking SQL to do some basic math for us.

```sql
select 50;
```

|column|
|------|
|    50| 

```sql
select 5+3;
```

|column|
|------|
|    8| 

```sql
select 2*10;
```

|column|
|------|
|    20| 

```sql
select 2^4;
```

|column|
|------|
|    16| 

## Multiple Columns

It's a bit annoying to have to do all these calculations separately. You can add them all to one select statement as long as you separate them by a comma.

```sql
select 
    50, 
    5+3, 
    2*10, 
    2^4;
```

|  column  |  column  |  column  |  column  |
|----------|----------|----------|----------|
|       50 |        8 |       20 |       16 |

We're not limited to only numbers in the select statement. We can also use SQL functions and display text strings.

Let's use the `concat` function to concatenate the value 50 and the string 'cents'.

```sql
select 
    2+2, 
    'fifty', 
    concat(50, ' ', 'cents');
```

|  column  |  column  |  column  |
|----------|----------|----------|
|        4 |    fifty | 50 cents |

## Aliasing Column Names

Our table names aren't very descriptive. Let's change (alias) the name of the first and the last column using `as`.

```sql
select 
    2+2 as simple_arithmetic, 
    'fifty', 
    concat(50, ' ', 'cents') as concat_result;
```

| simple_arithmetic | column | concat_result |
|-------------------|--------|---------------|
|                 4 | fifty  | 50 cents      |

# FROM

In the real world, you're going to want to `select` data from database tables and do something with it. We do this with a `from`.

Let's select the *id* and the *name* columns from the artists table.

**(Show table schematic)**

```sql
select id, name
from artists;
```

| id |       name        |
|----|-------------------|
|  1 | AC/DC             |
|  2 | Accept            |
|  3 | Aerosmith         |
|  4 | Alanis Morissette |

## Column Order
You can easily change the order of the listed columns. Let's say I want to show the name followed by ID. No problem.

```sql
select name, id
from artists;
```

|   name    | id |
|-----------|----|
| AC/DC     |  1 |
| Accept    |  2 |
| Aerosmith |  3 |

## * Splat

What if you want to display all the columns in that table without having to write them out manually in the `select` statement?
That's where the `*` (splat) comes in.

```sql
select *
from artists;
```

<div class="table--overflow" markdown="block">

| id |   name    |         created_at         |         updated_at         |
|----|-----------|----------------------------|----------------------------|
|  1 | AC/DC     | 2021-02-13 22:05:35.844418 | 2021-02-13 22:05:35.844418 |
|  2 | Accept    | 2021-02-13 22:05:35.847811 | 2021-02-13 22:05:35.847811 |
|  3 | Aerosmith | 2021-02-13 22:05:35.849931 | 2021-02-13 22:05:35.849931 |

</div>

You'll see a few ways of writing these select statement in the wild. One way is to specify the table name, dot, and then a splat or column name.

```sql
select artists.*
from artists
```

You can also explicitly define the table where you'll be getting your columns from right in the select statement.
```sql
select artists.id, artists.name
from artists
```

It's not needed if you're just querying one table. However, we'll be joining multiple tables very soon and this technique comes handy.

# Order By

SQL will let you order your rows ascending and descending with the `order by` command.

Let's say I want to select the id and the name from the artists table and order by name in ascending order (alphabetical order).

```sql
select artists.id, artists.name
from artists
order by name
```

| id  |                   name                    |
|-----|-------------------------------------------|
|  43 | A Cor Do Som                              |
|   1 | AC/DC                                     |
| 230 | Aaron Copland & London Symphony Orchestra |
| 202 | Aaron Goldberg                            |

You have two options to order by ascending `asc` and descending `desc`

Let's order by name but in a descending order (reverse-alphabetical).

```sql
select 
	id, 
	name
from artists
order by name desc
```

| id  |      name      |
|-----|----------------|
| 155 | Zeca Pagodinho |
| 168 | Youssou N'Dour |
| 212 | Yo-Yo Ma       |
| 255 | Yehudi Menuhin |

By default, SQL orders the rows by the primary key of the table, which is typically the `id`. 

Try to select all columns from the artists table and order the id in descending order:

```sql
select *
from artists
order by id desc
```

<div class="table--overflow" markdown="block">

| id  |                                        name                                        |         created_at         |         updated_at         |
|-----|------------------------------------------------------------------------------------|----------------------------|----------------------------|
| 275 | Philip Glass Ensemble                                                              | 2021-02-13 22:05:36.197593 | 2021-02-13 22:05:36.197593 |
| 274 | Nash Ensemble                                                                      | 2021-02-13 22:05:36.196375 | 2021-02-13 22:05:36.196375 |
| 273 | C. Monteverdi, Nigel Rogers - Chiaroscuro; London Baroque; London Cornett & Sackbu | 2021-02-13 22:05:36.195165 | 2021-02-13 22:05:36.195165 |
| 272 | Emerson String Quartet                                                             | 2021-02-13 22:05:36.193975 | 2021-02-13 22:05:36.193975 |

</div>


## Big table


<div class="table--overflow" markdown="block">

| id |                  name                   | album_id | media_type_id | genre_id |                                composer                                | milliseconds |  bytes   | unit_price | created_at | updated_at |
|----|-----------------------------------------|----------|---------------|----------|------------------------------------------------------------------------|--------------|----------|------------|------------|------------|
|  1 | For Those About To Rock (We Salute You) |        1 |             1 |        1 | Angus Young, Malcolm Young, Brian Johnson                              |       343719 | 11170334 |          0 | 05:37.6    | 05:37.6    |
|  2 | Balls to the Wall                       |        2 |             2 |        1 |                                                                        |       342562 |  5510424 |          0 | 05:37.6    | 05:37.6    |
|  3 | Fast As a Shark                         |        3 |             2 |        1 | F. Baltes, S. Kaufman, U. Dirkscneider & W. Hoffman                    |       230619 |  3990994 |          0 | 05:37.6    | 05:37.6    |
|  4 | Restless and Wild                       |        3 |             2 |        1 | F. Baltes, R.A. Smith-Diesel, S. Kaufman, U. Dirkscneider & W. Hoffman |       252051 |  4331779 |          0 | 05:37.6    | 05:37.6    |

</div>