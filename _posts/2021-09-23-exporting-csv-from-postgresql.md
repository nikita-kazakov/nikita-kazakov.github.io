---
title: Exporting to a CSV from Postgresql
date: 2021-09-23
layout: post
permalink: /postgresql-export-csv
tags:
    - sql
---

I had to run a query on a Postgresql database in production and export the data to a CSV file. I couldn't use [Postico](https://eggerapps.at/postico).

Enter psql on the Postgresql server. Create a Postgresql view (saves the query to a variable).

```sql
CREATE VIEW company_locations AS
    SELECT *
    FROM companies
    WHERE location = 'US';
```

Run the line below to export the view to a csv and keep the header. It is saved to 'home/deploy/csv_export.csv' 
on the server.

```shell
copy (select * from view_1) to /local/path/csv_export.csv csv header;
```

Use scp (secure copy) to move `csv_export.csv` to your computer by typing the line below in your local terminal (not in the PSQL terminal).

```shell
scp user@ec2.amazonaws.com:/home/user/csv_export.csv /Users/admin/desktop
```