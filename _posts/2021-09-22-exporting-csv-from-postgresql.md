---
title: Exporting to a CSV from Postgresql
date: 2021-09-22
layout: post
permalink: /postgresql-export-csv
tags:
    - sql
---

I had to run a query on a Postgresql database in production and export the CSV data. I couldn't use [Postico](https://eggerapps.at/postico).

Enter psql on the server. Create a Postgresql view (essentially saving your query to a variable).

```sql
CREATE VIEW company_locations AS
    SELECT *
    FROM companies
    WHERE location = 'US';
```

Run this to export a query to a csv and keep the header. We are saving it to 'home/deploy/csv_export.csv' on the
server.  


```shell
copy (select * from view_1) to /local/path/csv_export.csv csv header;
```

Use scp (secure copy) to move `csv_export.csv` to your computer by typing this in your local terminal (not in the PSQL 
terminal).

```shell
scp user@ec2.amazonaws.com:/home/user/csv_export.csv /Users/admin/desktop
```