---
id: 7120
title: Troubleshooting undefined method error when updating database rows
date: 2020-02-20T23:11:00+00:00
author: Nikita Kazakov
layout: post
guid: https://nikitakazakov.com/?p=7120
permalink: /troubleshooting-undefined-method-error-when-updating-database-rows/
site-sidebar-layout:
  - default
site-content-layout:
  - default
theme-transparent-header-meta:
  - default
categories:
  - Uncategorized
tags:
  - ruby
---
Sometimes I need to make changes to a Ruby on Rails table in production.

Before doing ANYTHING in production, I create a script and run the script in my local development environment.

If the table that you&#8217;re changing in production doesn&#8217;t have sensitive information, I suggest exporting the table into a CSV sheet as a backup in case something goes wrong.

I&#8217;ll ssh into the production server and run the rails console and check how many records I&#8217;ll be changing on the model `Image`.

```ruby
rails console
Image.count  # 40,000 records
```

I&#8217;ll run a script to take the name string and substitute underscores with spaces.

Note that I&#8217;m using the `find_each` method instead of `each`. We have a lot of records and `each` will load all 40,000 records into memory. Things might crash.

`find_each` will load a batch of 1,000 records by default as it goes through all the `Image` records.

```ruby
Image.find_each do |image|
  changed_name = image.name.gsub("_", " ")
  image.update_columns(name: changed_name)
end
```

One minute into running the script, it returns an error:

```
NoMethodError: undefined method `gsub' for nil:NilClass
from (irb):26:in `block in irb_binding'
from (irb):25
```

It&#8217;s hard to debug in production console. The hint here is that `gsub` was called on something that doesn&#8217;t exist.

In our script, we called `image.name.gsub`.

The `image` is not missing because we&#8217;re iterating through all the existing images using `find_each`. The `name` however is suspicious.

Let&#8217;s run an ActiveRecord query to see if a name is missing for any `Image` records.

```ruby
FreshStockAsset.where(name:nil).count # 5
```
There&#8217;s the problem! Five records are missing a name. I can go through them an give them a name and then re-run the original script. It should run without errors.

A long term solution to this is to think about whether there should be validation on the presence of a name for a saved image.