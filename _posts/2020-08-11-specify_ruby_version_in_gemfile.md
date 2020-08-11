---
title: Why specify ruby version in your gemfile
date: 2020-08-11
layout: post
permalink: /specify-ruby-version-in-gemfile/
tags: ruby
---

# Problem

I had several Ruby and Ruby on Rails projects I was working on that used different versions of Ruby. Each time I'd open a project, I had to set the correct version of Ruby using [RVM](https://rvm.io/). It was a pain.

For example, I'd have to run something like this on every terminal window that I'd use with that project.

```
rvm use 2.6.6
```

# Solution
If you don't already have a Gemfile for your Ruby project, create one. Make sure to specify the Ruby version in the Gemfile.

For example, a Gemfile can look like this:
```ruby
source "https://rubygems.org"
ruby '2.6.6'
``` 

RVM will automatically read the Gemfile and switch Ruby to the correct version the Gemfile specifies. No more manual switching required!