---
title: How to backup and restore a postgresql database
date: 2021-05-02
layout: post
permalink: /postgresql-backup-restore/
tags: 
    - sql
---

Here's why you might want to do this:

- Backup your database in the development environment in case you accidentally drop it. It’s going to be a pain to restore your tables. 
- You might want to restore a production database in your local environment to work with real life data.

For the examples below, let’s assume the name of the postgresql database is `current_db`.

# Backing up a database

Run the following in the terminal to do a plain-text export to a sql file like this:

`pg_dump current_db > current_db.sql`

Plain text can be large and it might be better to compress it with gzip.

`pg_dump current_db | gzip > current_db.gz`

If you’re using EngineYard or some other managed database platform, the backed up database dump file should already be available for you to download. There’s no reason to stress the production servers by backing up a database manually.

# Restoring a database

If you’re using Ruby on Rails, edit your `database.yml` file. Rename the database to whatever you want it to be called (`current_db` in this example).

```yaml
development:
    <<: *default
    database: current_db
    host: 127.0.0.1
```


Create an empty database in Rails with rails db:create. You can now restore to that database:

`psql current_db < current_db.sql`

If you instead have a dump file, you won’t be able to use the line above. Let’s get a bit more technical and remove any users from the database we are going to import.

`pg_restore --no-owner --schema=public -d current_db current_db.dump`

Depending on the size of the database, this might take a long time to restore. You won’t see a progress bar in the terminal window. As an example, a 25GB database dump file took me over an hour of waiting to restore locally.