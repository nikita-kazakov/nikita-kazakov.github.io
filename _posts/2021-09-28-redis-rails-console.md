---
title: Using Redis as Rails Cache
date: 2021-09-28
layout: post
permalink: /redis-rails-console
tags:
    - ruby on rails
---


Once you have Redis set up as a Rails cache backend for your project, here's how you can explore it in the Rails console.

```ruby
# Writes a value to a Redis key:
Rails.cache.write('pi', 3.14)
# Reads the key from and outputs the value from Redis
Rails.cache.read('pi')
```

But what if you want the Redis cached keys to expire? No problem. Use `Rails.cache.fetch`

```ruby
Rails.cache.fetch('name', expires_in: 10.seconds) { 'bob' }

# or

Rails.cache.fetch('name', expires_in: 10.seconds) do
    # Write code here
end
```

The nice thing about `Rails.cache.fetch` is that it does the reading / writing automatically. If the key isn't stored, Rails.cache.fetch will store it for you and return the result within the code block. If the key was already stored, then it will simply skip the code block and return the cached value from Redis.

So here's how I'd use it in a Rails application:

```ruby
def long_cached_list
    Rails.cache.fetch('list', expires_in: 1.day) do
        User.pluck(:first_name)
    end
end
```

I can run `long_cached_list` method anywhere in my Rails app and it doesn't have to hit the database once it's cached.
