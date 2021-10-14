---
title: Resetting the primary key sequence (row count) in Rails
date: 2021-10-01
layout: post
permalink: /resetting-primary-key-sequence-rails
tags:
    - ruby on rails
---

If you import data into a Rails project manually, you'll see that the primary key count in Rails might be off. For example, running `User.last` doesn't show the last row in the User table.

The problem is that the primary key sequence is off. This value is maintained by Postgresql every time you add a new row.

The fix this problem, enter Rails console.

Let's say you know that it's the users table where you want to reset the primary key sequence. Run:

```ruby
 ActiveRecord::Base.connection.reset_pk_sequence!('users')
```

If you want to reset the primary key sequence for all tables in the database, run:

```ruby
ActiveRecord::Base.connection.tables.each do |table|
  ActiveRecord::Base.connection.reset_pk_sequence!(table)
end
```


