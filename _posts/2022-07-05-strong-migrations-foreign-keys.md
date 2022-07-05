---
title: Adding Rails references with strong migrations gem
date: 2022-07-05
layout: post
permalink: /strong-migrations-foreign-keys
tags:
- ruby on rails
---

strong_migrations gem prevents large database tables from locking up when running database migrations. The drawback is that instead of running one easy Rails migration, you end up breaking up migrations into three parts.

Here's how you create a column and add a reference to it, turn it into a foreign key, and run validations using the [strong_migrations gem](https://github.com/ankane/strong_migrations).

# Relationship between two tables

Let's say I want to add a `subscription_id` column on a `tickets` table.

First Migration creates the `subscription_id` column and adds a reference.

```ruby
def change
  add_reference :tickets, :subscription, index: { algorithm: :concurrently }
end
```

The second migration adds a foreign key but without validations to avoid locking up the table.
```ruby
def change
  add_foreign_key :tickets, :subscriptions, validate: false
end
```

The third migration runs validations.
```ruby
def change
  validate_foreign_key :tickets, :subscriptions
end
```

# Self Join Example

I have a `ticket_files` table. I want to add a `parent_id` column to it and ensure it is a foreign key in Rails. A row in the `ticket_files` table can be a parent and that parent can have children that are also rows in the `ticket_files` table.

You'll need to run 3 different migrations.

First migration creates a `parent_id` column and references it.
```ruby
def change  
  add_reference :ticket_files, :parent, index: { algorithm: :concurrently }  
end  
```

The second migration adds a foreign key to this column and specifically doesn't validate it so that if the table has millions of rows, it doesn't lock up.
```ruby
def change  
  add_foreign_key :ticket_files, :ticket_files, column: :parent_id, validate: false  
end
```

The third migration validates the new column.
```ruby
def change  
  validate_foreign_key :ticket_files, column: :parent_id  
end  
```