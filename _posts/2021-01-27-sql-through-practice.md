---
title: Practicing SQL through examples.
date: 2021-01-27
layout: post
permalink: /sql-by-examples/
tags: 
    - sql
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

You could also use double quotes for aliasing. For example, instead of `simple_arithmetic`, you could write `"simple arithmetic"`. 
You can use spaces with double quotes.

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

SQL will let you order your rows ascending and descending with the `order by` clause.

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

Note that when using `order by`, SQL will order in ascending order by default. For example:
`order by name` and `order by name asc` are exactly the same.

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

# Limits and Offsets

Running a query and listing all the rows can be risky if your table has millions of rows. 
You'll needlessly stress that database server and piss off the database administrator.

Instead we can `limit` our queries to give us a limited number of rows.

```sql
select *
from artists
order by id desc
limit 4
```

| id |       name        |
|----|-------------------|
|  1 | AC/DC             |
|  2 | Accept            |
|  3 | Aerosmith         |
|  4 | Alanis Morissette |

We can also `offset` rows. Let's say we want to get rows 3 to 7. Offsetting rows is useful when paginating results on a website.

```sql
select id, name
from artists
limit 5
offset 2
```

| id |        name         |
|----|---------------------|
|  3 | Aerosmith           |
|  4 | Alanis Morissette   |
|  5 | Alice In Chains     |
|  6 | Antnio Carlos Jobim |
|  7 | Apocalyptica        |

# WHERE

The `where` clause is powerful because you can start to filter down what you want to see in your SQL query.

For example, let's select a name column from the artists table where the name is Metallica. 
Read this sentence and compare to how similar the SQL query below sounds.

```sql
select name
from albums
where
    name = 'Metallica'
```

|   name    |
|-----------|
| Metallica |

## Multiple Where / AND

Can you select the id and the name columns from artists where id is equal to 5, 10, 30?

One way to do it is to give multiple where clauses separated by `or`. You're telling SQL that the `id`
can be 5 or 10 or 30.

```sql
select id, name
from artists
where
    id = 5 or
    id = 10 or
    id = 30
```

A less verbose and more straightforward way to do this is to use the `in`. The `in` takes an array of 5, 10, 30 and gives a result.

```sql
select id, name
from artists
where
    id in (5, 10, 30)
```

| id |      name       |
|----|-----------------|
|  5 | Alice In Chains |
| 10 | Billy Cobham    |
| 30 | Jorge Vercilo   |


Let's take a look at the `AND` operator. Select the tracks where the composer is 'Foo Fighters' and the track length is greater than 300000 milliseconds.

```sql
select *
from tracks
where
	composer = 'Foo Fighters' and
	milliseconds > 300000
```

<div class="table--overflow" markdown="block">

|  id  |     name     | album_id | media_type_id | genre_id |   composer   | milliseconds |  bytes   | unit_price |         created_at         |         updated_at         |
|------|--------------|----------|---------------|----------|--------------|--------------|----------|------------|----------------------------|----------------------------|
| 1014 | Tired Of You |       81 |             1 |        4 | Foo Fighters |       311353 | 10094743 |       0.99 | 2020-10-23 23:38:36.402027 | 2020-10-23 23:38:36.402027 |
| 1015 | Halo         |       81 |             1 |        4 | Foo Fighters |       306442 | 10026371 |       0.99 | 2020-10-23 23:38:36.402027 | 2020-10-23 23:38:36.402027 |
| 1019 | Come Back    |       81 |             1 |        4 | Foo Fighters |       469968 | 15371980 |       0.99 | 2020-10-23 23:38:36.402027 | 2020-10-23 23:38:36.402027 |

</div>

Now narrow down that table and select only the name, composer, milliseconds, and bytes. Also order the table by name in the ascending order.

```sql
select 
    name, 
    composer, 
    milliseconds, 
    bytes
from tracks
where
	composer = 'Foo Fighters' and
	milliseconds > 300000
order by name
```

|     name     |   composer   | milliseconds |  bytes   |
|--------------|--------------|--------------|----------|
| Come Back    | Foo Fighters |       469968 | 15371980 |
| Halo         | Foo Fighters |       306442 | 10026371 |
| Tired Of You | Foo Fighters |       311353 | 10094743 |

Milliseconds are not really intuitive. Can you instead convert milliseconds into seconds show that as an additional column in the table report?

```sql
select 
	name, 
	composer, 
	milliseconds, 
	(milliseconds / 1000) as seconds,
	bytes
from tracks
where
	composer = 'Foo Fighters' and
	milliseconds > 300000
order by name
```

|     name     |   composer   | milliseconds | seconds |  bytes   |
|--------------|--------------|--------------|---------|----------|
| Come Back    | Foo Fighters |       469968 |     469 | 15371980 |
| Halo         | Foo Fighters |       306442 |     306 | 10026371 |
| Tired Of You | Foo Fighters |       311353 |     311 | 10094743 |

Let's make the report even better and convert the bytes column into megabytes and seconds into minutes.

```sql
select 
	name, 
	composer, 
	milliseconds, 
	(milliseconds / 1000) / 60 as minutes,
	(bytes / 1024) as megabytes,
	bytes
from tracks
where
	composer = 'Foo Fighters' and
	milliseconds > 300000
order by name
```


|     name     |   composer   | milliseconds | minutes | megabytes |  bytes   |
|--------------|--------------|--------------|---------|-----------|----------|
| Come Back    | Foo Fighters |       469968 |       7 |     15011 | 15371980 |
| Halo         | Foo Fighters |       306442 |       5 |      9791 | 10026371 |
| Tired Of You | Foo Fighters |       311353 |       5 |      9858 | 10094743 |

You can easily mix `or` and `and` statements. There are different ways to do this and some are cleaner than others.

Can you select name, composer, milliseconds, bytes from the tracks table where the composer is either Chuck Berry or Little Richard AND 
the track size in bytes is smaller than 8,000,000?

First way to do it is below. Notice how we use parenthesis to isolate the or statements together.

```sql
select 
	name, 
	composer,
	milliseconds,
	bytes
from tracks
where 
	bytes < 8000000 and 
    (composer = 'Chuck Berry' or composer = 'Little Richard')
```

A cleaner way is to use the `IN` statement.

```sql
select 
	name, 
	composer,
	milliseconds,
	bytes
from tracks
where 
	bytes < 8000000 and 
	composer in ('Chuck Berry', 'Little Richard')
```

## NOT (negation) and ! (not equal to)

You can also invert a where clause. There are two ways of doing this. 

Select the id and name from the artists table where the artist name is not Aerosmith. Limit the rows to 5.

```sql
select *
from artists
where
	not name = 'Aerosmith'
limit 5
```

| id |        name         |
|----|---------------------|
|  1 | AC/DC               |
|  2 | Accept              |
|  4 | Alanis Morissette   |
|  5 | Alice In Chains     |
|  6 | Antnio Carlos Jobim |

Note that the id equal to 3 is missing from the table. That was Aerosmith. 

In many programming languages, `!=` is not equal to. You can also write `<>` instead of `!=`. Let's use it in our example below.

```sql
select id, name
from artists
where
	name != 'Aerosmith'
limit 5
```

## Null

Nulls are empty cell in the database. To test whether a cell is empty, you can use either `is null` or `is not null` to test that it's not empty. You can't use `=` or `!=` with nulls.

Let's select the tracks where the composer fields are null.

```sql
select 
    id, 
    name, 
    composer
from tracks
where
    composer is null
```

| id |                 name                 | composer |
|----|--------------------------------------|----------|
|  2 | Balls to the Wall                    |          |
| 63 | Desafinado                           |          |
| 64 | Garota De Ipanema                    |          |
| 65 | Samba De Uma Nota S (One Note Samba) |          |
| 66 | Por Causa De Voc                     |          |
| 67 | Ligia                                |          |


## Operators

Below are common operators used with SQL. They are used with the `where` clause.

| Operator  |      What it does     |
|-----------|-----------------------|
| =         | equal                 |
| >         | greater than          |
| <         | less than             |
| >=        | greater than or equal |
| <=        | less than or equal    |
| !=        | not equal             |
| <>        | not equal             |

## Pattern matching (string operators)

Pattern string matching is a powerful feature of a database. You can use `LIKE`, where a string matches a pattern. There's
also `ILIKE`, which a case insensitive version of `LIKE`.

Find the Artists that have the word 'Orchestra' in the name.

```sql
-- This is incorrect as it will search exactly for the word Orchestra.
-- There are zero results
select *
from artists
where name = 'Orchestra'
```

This is where you want to pattern match:

```sql
select id, name
from artists
where
    name like '%Orchestra%'
```

| id  |                                     name                                     |
|-----|------------------------------------------------------------------------------|
| 192 | DJ Dolores & Orchestra Santa Massa                                           |
| 210 | Hilary Hahn, Jeffrey Kahane, Los Angeles Chamber Orchestra & Margaret Batjer |
| 217 | Royal Philharmonic Orchestra & Sir Thomas Beecham                            |
| 220 | Chicago Symphony Chorus, Chicago Symphony Orchestra & Sir Georg Solti        |
| 223 | London Symphony Orchestra & Sir Charles Mackerras                            |
| 224 | Barry Wordsworth & BBC Concert Orchestra                                     |
| 229 | Boston Symphony Orchestra & Seiji Ozawa                                      |
| 230 | Aaron Copland & London Symphony Orchestra                                    |
| 233 | Chicago Symphony Orchestra & Fritz Reiner                                    |
| 234 | Orchestra of The Age of Enlightenment                                        |
| 235 | Emanuel Ax, Eugene Ormandy & Philadelphia Orchestra                          |
| 241 | Felix Schmidt, London Symphony Orchestra & Rafael Frhbeck de Burgos          |
| 243 | Antal Dorti & London Symphony Orchestra                                      |

It gives you the artists name that have the word "Orchestra". But what the heck is `%`? It's a wildcard. By putting `%` before
'Orchestra' says it doesn't matter what comes before the word 'Orchestra'. By putting it afterwards also says it doesn't matter
what comes after 'Orchestra'.

I usually use `ilike` unless the word I'm pattern matching is case specific. For example, I could use `ilike` below and 
match on `orchestra` (lower case). It would return the same thing as above.

```sql
select id, name
from artists
where
    name ilike '%OrCHEstRA%'
```

The table below is taken from the [postgresql docs](https://www.postgresql.org/docs/8.3/functions-matching.html). Here are some examples of `like` matching:

|    Statement     | Result  |
|------------------|---------|
| 'abc' LIKE 'abc' |  true   |
| 'abc' LIKE 'a%'  |  true   |
| 'abc' LIKE '_b_' |  true   |
| 'abc' LIKE 'c'   |  false  |

If you want to use regular expressions (REGEX), you can use `SIMILAR TO` clause. That's a topic beyond this scope. See [more here](https://www.postgresql.org/docs/8.3/functions-matching.html).

## Aggregate Functions

To aggregate means to combine several elements together to get a whole. When building reports, you want sums, averages, and counts of
many rows. This is where aggregate functions come into play.

Let's start with the `count`. Let's say you want to count the number of rows in the artists table.

```sql
select count(*)
from artists
```

| count |
|-------|
|   275 |

The result is 275 rows! The `count` is a function that takes a parameter. We're passing in the `*` splat, which represents a whole row.

What if we want to count the number of composers in the tracks tables and leave out the null values?

```sql

select count(*)
from tracks;
-- The count is 3503

select count(composer)
from tracks;
-- The count is 2525
```

Note that this is NOT the same count as counting all the rows in the tracks table because we're counting the composer rows that are not NULL.

We can do multiple aggregate calculations. 

Let's count all the rows in tracks and sum up the unit_price for all the rows. Let's also alias them to meaningful names.

```sql
select 
    count(*) as track_count, 
    sum(unit_price) as unit_price_sum
from tracks
```

| track_count | unit_price_sum |
|-------------|----------------|
|        3503 |        3680.97 |

Here are some common aggregate functions you can use:

|    Function     |                What it does                 |
|-----------------|---------------------------------------------|
| MIN             | The minimum number                          |
| MAX             | The maximum Number                          |
| SUM             | sum of all the values                       |
| AVG             | average (mean)                              |
| COUNT           | count of the # of values                    |
| COUNT DISTINCT  | count of the # of unique (distinct) values. |

Count DISTINCT will not double count rows that have the same value.

How many unique prices are there in the tracks table?

```sql
select count(distinct unit_price)
from tracks
-- Count is 2.
```

Can you aggregate the average, minimum, and maximum unit_price from the tracks table. Also alias them to more readable column names.

```sql
select 
	avg(unit_price) as avg_price,
	max(unit_price) as maximum_price, 
    min(unit_price) as minimum_price
from tracks
```

| avg_price | maximum_price | minimum_price |
|-----------|---------------|---------------|
|     1.050 |          1.99 |          0.99 |

**Aside** If you are a Ruby or Ruby on Rails developer, don't use Ruby to aggregate thousands of rows of data. This is a common mistake.
SQL is incredibly fast compared to Ruby when it comes to manipulating database values. Now that you know how to aggregate and
group data, use SQL to do the calculation heavy lifting for you instead of iterating with an each block in Ruby.
{: .notice--info}

## Group By

Group By function is incredibly powerful in generating reports. It's also a bit confusing to understand at first.
Group by tells the database how to group a result set.

The question is --- which composer has the most number of tracks? To answer this, let's sum the number of tracks each composer has done in descending order.

```sql
select 
	composer, 
	count(*)
from tracks
where composer is not null
group by composer
order by count desc
```

|    composer     | count |
|-----------------|-------|
| Steve Harris    |    80 |
| U2              |    44 |
| Jagger/Richards |    35 |
| Billy Corgan    |    31 |
| Kurt Cobain     |    26 |


**Gotcha**: If you're mixing aggregate functions and normal column names, you'll need a group by function in your statement otherwise you'll get an error.
{: .notice--danger}

```sql
select 
	composer,
	count(*)
from tracks
-- This will result in an error as you've mixed 
-- composer (column name) with an aggregate function (count*)
```

Can you find the minimum file size (bytes) of a track and group by composer?

```sql
select composer, min(bytes)
from tracks
group by composer
```

|                     composer                     |   min   |
|--------------------------------------------------|---------|
| Clapton/F.eldman/Linn                            | 6006154 |
| Delroy "Chris" Cooper, , Luke Smith, Paul Watson | 3426106 |
| Bruce Dickinson/Janick Gers                      | 3151872 |
| James Hetfield, Lars Ulrich and Kirk Hammett     | 8024047 |
| Pearl Jam & Eddie Vedder                         | 9991106 |

Let's order that table by the minimum file size in ascending order.

```sql
select composer, min(bytes)
from tracks
group by composer
order by min
```

You can see that Samuel Rosa has the smallest track size.

|   composer   |   min   |
|--------------|---------|
| Samuel Rosa  |   38747 |
|              |  161266 |
| L. Muggerud  |  319888 |
| Gilberto Gil | 1039615 |

Let's group by multiple values. Can you group composers by the maximum track time (milliseconds) and then by maximum file size (bytes)?

```sql
select composer, 
	max(milliseconds) as max_time, 
	max(bytes) as max_bytes
from tracks
where
	composer is not null
group by composer
order by 
	max_time desc,
	max_bytes desc
```

It looks like Jimmy Page has tracks with the most track time and largest file size.


|                 composer                 | max_time | max_bytes |
|------------------------------------------|----------|-----------|
| Jimmy Page                               |  1612329 |  52490554 |
| Blackmore/Gillan/Glover/Lord/Paice       |  1196094 |  39267613 |
| Jimmy Page/Led Zeppelin                  |  1116734 |  36052247 |
| Gillan/Glover/Lord/Nix - Blackmore/Paice |   913658 |  29846063 |

## JOINS

## Big table


<div class="table--overflow" markdown="block">

| id |                  name                   | album_id | media_type_id | genre_id |                                composer                                | milliseconds |  bytes   | unit_price | created_at | updated_at |
|----|-----------------------------------------|----------|---------------|----------|------------------------------------------------------------------------|--------------|----------|------------|------------|------------|
|  1 | For Those About To Rock (We Salute You) |        1 |             1 |        1 | Angus Young, Malcolm Young, Brian Johnson                              |       343719 | 11170334 |          0 | 05:37.6    | 05:37.6    |
|  2 | Balls to the Wall                       |        2 |             2 |        1 |                                                                        |       342562 |  5510424 |          0 | 05:37.6    | 05:37.6    |
|  3 | Fast As a Shark                         |        3 |             2 |        1 | F. Baltes, S. Kaufman, U. Dirkscneider & W. Hoffman                    |       230619 |  3990994 |          0 | 05:37.6    | 05:37.6    |
|  4 | Restless and Wild                       |        3 |             2 |        1 | F. Baltes, R.A. Smith-Diesel, S. Kaufman, U. Dirkscneider & W. Hoffman |       252051 |  4331779 |          0 | 05:37.6    | 05:37.6    |

</div>