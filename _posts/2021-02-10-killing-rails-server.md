---
title: How to kill a rails server
date: 2021-02-10
layout: post
permalink: /killing-rails-server/
tags: 
    - ruby on rails
---

I can't be the only one who occasionally tries to start `rails server` and gets:

```bash
Ctrl-C to shutdown server
A server is already running. Check ./tmp/pids/server.pid.
```

Open your terminal and type in (this command will unfortunately close down your browser windows as well.)

```bash
kill -9 $(lsof -i tcp:3000 -t)
```

Now run `rails server` and it will succeed.

## Creating a Ruby File 

Because I won't remember this cryptic looking command, I like to create a separate `ruby-kill.rb` file right in my Rails project directory.

Add this inside the `ruby-kill.rb`:
```ruby
system("kill -9 $(lsof -i tcp:3000 -t)")
```

Run this file whenever you need to kill the rails server.