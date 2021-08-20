---
title: Avoiding bundle exec in Ruby
date: 2021-08-15
layout: post
permalink: /avoid-bundle-exec
tags: 
    - ruby
---

When I mix multiple projects in the same Ruby environment, I end up with different versions of the same gem.

Let's say I'm running Rails 5 and Rails 6 under Ruby 2.7.1.

I run `rails server` and Bundler suggests I run `bundle exec rails server` so that it loads gems from the gemlock file.

I don't like typing extra characters. Here are a few ways to solve the `bundle exec` problem.

# Use RVM
[asdf](https://github.com/asdf-vm/asdf) and [rbenv](https://github.com/rbenv/rbenv) do not solve the `bundle exec` problem because although they create a Ruby versioned path, they do not isolate each rails project into a gemset that is independent from other gems. They rely on bundler to know which versions of gems to run.

[RVM is the Ruby version manager](/how-to-ruby-rvm) that specifically creates gemsets that separate all project gems into their own container.

rbenv does have a (rbenv-gemset plugin)[https://github.com/jf/rbenv-gemset], but in my experience, it's dicey to work with.

The downside of RVM is its deep integration in the MacOS system. It apparently overwrites basic shell commands to make things work. I haven't been bitten by this in my own software development.

# Clean up gems
You can clean up all the gems that aren't being used in your project's gemset by running `bundle clean --force`. That will ensure there are no version conflicts and you won't need to use `bundle exec`.


# Binstubs
You can generate a binstub using Rails 5 and above. The files it generates will be placed in the `bin` folder in the Rails project root directory.

For example, when I ran `sidekiq`, bundler suggested I run `bundle exec sidekiq`.

I generated a bindstub like this:
`bundle binstub sidekiq`

Bundler created a few files in the `bin` directory and bundler knew exactly which version of sidekiq to run.

# Bundler vendor folder
Did you know you can ask bundler to install gems within your specific project folder rather than a system folder that is shared with other gems? [This blog post by Ryan McGeary has more info on how to do that](http://ryan.mcgeary.org/2011/02/09/vendor-everything-still-applies/).

I tried it and although it almost replaced the idea of gemsets for me, I was still encountering places where I had to write `bundle exec`.

# What I settled on
I initially used RVM. The rest of my team used rbenv. I moved over to rbenv but was frustrated that it sometimes initialized and sometimes it didn't. I then moved over to asdf-vm as that was the new hotness but asdf didn't isolate project gems like RVM did.

I'm now back to using RVM because gemsets simplify my life and I don't have to hunt down gem inconsistencies. I no longer have to use `bundle exec`.
