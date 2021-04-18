---
title: How to use RVM as a Ruby Version Manager
date: 2021-04-17
layout: post
permalink: /how-to-ruby-rvm/
tags: 
    - ruby
---

This is the article I wish I had when I started software development with Ruby. 

You need to use some kind of Ruby version manager when working with Ruby and Ruby on Rails projects to avoid gem conflicts and easily switch between Ruby versions. 
You have different options to choose from: [RVM](https://rvm.io/), [rbenv](https://github.com/rbenv/rbenv), [asdf](https://github.com/asdf-vm/asdf-ruby).

I use RVM daily and that's what we'll talk about. The reason I’m writing this post is because I ran into a gem error that my colleagues weren’t running into. The problem was that I installed gems from different projects into the same environment  (gemset). Bundler is smart enough to avoid conflicts but I asked too much.

Don’t make the same mistake I did. There’s a better way!

# Why use a Ruby Version Manager?

You probably know that you can directly install Ruby on your MacOS or Linux system. The problem is that there’s not one single version of Ruby and not all projects are on the same version.

For example, let’s say you downloaded and ran open source Ruby project that uses Ruby 1.9.3 and you installed that same version on your MacOS.

A day later, you downloaded a project that uses Ruby 2.3 This version is way better and has more features than Ruby 1.9 The project likely used those newer features. If you try to run the 2.3 version with a 1.9 version of Ruby, you’ll get errors.

So what do you do? You uninstall your current Ruby 1.9 and install 2.3. What a hassle!

Wouldn’t it be nice if you could install multiple versions of Ruby on your machine and simply switch between them? Wouldn’t it be even better if your machine would switch version automatically without you even thinking about it?

That is the beauty of a Ruby version manager and that’s exactly why you need it.

# Installing RVM

I’m using these [official instructions](https://rvm.io/rvm/install). Open your terminal and run this:

`\curl -sSL https://get.rvm.io | bash -s stable --ruby`

Exit your terminal and enter it again. Try to type in rvm. You’ll get an error: rvm: command not found.

If you’re running on MacOS, you want RVM to load whenever you start your terminal. If you’re running a bash terminal, navigate to the folder that has the .bash_profile file. Open it up and add these two lines to it and save it.

```bash
[[ -s "$HOME/.profile" ]] && source "$HOME/.profile" # Load the default .profile
[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm" # Load RVM into a shell session *as a function*
```

Close your terminal and reopen it and type in `rvm`. You should see RVM populate a big list of commands that you can use.

Linux installation instructions will be different. Let google guide you.

# Ruby versions

RVM outputs a big list of things you can run with it. Don’t get intimidated. It’s fairly readable. Treat it like a table of contents.

{% include image_center_caption.html 
    caption = "RVM contains Ruby versions. Ruby versions contain gemsets which contain gems."
    image = "/assets/images/2021/rvm_ruby_nesting_diagram.jpg"
    alt = "RVM contains Ruby versions. Ruby versions contain gemsets which contain gems."
%}

Let’s take a look at what current Ruby versions are installed

```bash
rvm list

# =* ruby-3.0.0 [ x86_64
# => - current
# =* - current && default
#  * - default
```

You can see that ruby-3.0.0 is installed and it is selected by default. Let’s say you want to use an older version of Ruby because your Ruby or Ruby on Rails project need it. Let’s say you need Ruby 2.6.6 installed.

Let’s get a list of all the ruby versions available to us from RVM:

```bash
rvm list known

# MRI Rubies
# [ruby-]1.8.6[-p420]
# [ruby-]1.8.7[-head] # security released on head
# [ruby-]1.9.1[-p431]
# [ruby-]1.9.2[-p330]
# [ruby-]1.9.3[-p551]
# [ruby-]2.0.0[-p648]
# [ruby-]2.1[.10]
# [ruby-]2.2[.10]
# [ruby-]2.3[.8]
# [ruby-]2.4[.10]
# [ruby-]2.5[.8]
# [ruby-]2.6[.6]
```

Bingo. There’s Ruby 2.6.6. Let’s install it: `rvm install ruby-2.6.6`

Let’s check the list again:
```bash
rvm list
# => ruby-2.6.6 [ x86_64 ]
#  * ruby-3.0.0 [ x86_64 ]

# => - current
# =* - current && default
#  * - default
```

You can see that when RVM downloaded ruby-2.6.6, it set it as the current Ruby for this **session**. Session is the keyword. Try to open another terminal window and see rvm list. You’ll see that RVM is back to using the default ruby-3.0.0.

You can manually switch the ruby version by typing in: `rvm use ruby-2.6.6`. Run `rvm list` and you’ll see it switched to 2.6.6!

You can now install different ruby versions and switch between them using RVM.

At this point, you’re probably thinking, this is going to be a pain if I have to switch Ruby versions every time I open a new terminal window. Don’t worry, I’ll show you how you can make RVM do that for you automatically. Before we get there though, let’s talk about gemsets.

# Gemsets

RVM has a gemset idea. Think of it like a drawer. A ruby version that you use through RVM can have different gemsets  (drawers). Those gemsets hold ruby gems. The beauty of this is that you can totally isolate specific gems for a specific project.

![](https://paper-attachments.dropbox.com/s_F247159AFB9659AAEF60B5119EB65B678016363E7E971664989D78D3E2F66DC3_1618706811491_image.png)

This is what I **DIDN’T** do for my projects when I started using RVM. It’s also why I got a gem error that I talked about in the beginning when running a Ruby on Rails project.

Take a look at the hidden RVM folder that contains these ruby versions and gemsets on your MacOS system under .rvm/gems folder. It more or less represents the diagram above.

I now keep a separate gemset for each Ruby on Rails project that I start from scratch or that I work on. That means each project has a clean area for it’s only its own gems. There’s no risk of conflict.

Let’s view the current list of RVM gemsets:

```bash
rvm gemset list
# => (default)
#   global
```

In my own workflows, a project should have it’s own gemset. Let’s create a new gemset. But how the heck do we do that?

```bash
rvm gemset

# Usage:
#   rvm gemset [action]
#   rvm --force gemset [action]

# Actions: copy, create, delete (alias: remove), dir, empty, export, gemdir, globalcache, import, install, list, list_all, name, pristine, rename (alias: move), unpack, update, use
# Look at that! RVM tells you the kind of actions you can take on a gemset. Let's use the create action here.
```

Let's create a gemset container called `chat_app`.

```bash
rvm gemset create chat_app
# ruby-2.6.6 - #gemset created /usr/local/rvm/gems/ruby-2.6.6@chat_app

rvm gemset list # note that chat_app was added to the gemset list.

# => (default)
#    chat_app
#    global
```

Note that it’s still using the default gemset. We want to use the `chat_app` gemset. Let’s switch over to it: `rvm gemset use chat_app`. Confirm it switched by looking at the `rvm gemset list` again.

If you close the terminal and reopen it again, your default selections will be lost. Let’s fix that.

# Generating .ruby-version and .ruby-gemset files

Navigate to the root folder of your Ruby or Ruby on Rails project in the terminal. Before you type in the command below, make sure you actually have ruby 2.6.6 installed with RVM and you created a gemset called chat_app.

`rvm --ruby-version use 2.6.6@chat_app`

RVM just generated two files for you in this directory: .ruby-gemset and .ruby-version. Open them up and take a look at what is inside.

RVM is storing the ruby version and the gemset name automatically for you with this project. You can now close down your terminal and whenever you reopen the terminal, RVM will automatically ensure Ruby 2.6.6 is used with the chat_app gemset. Beautiful!

This means you can switch between many Ruby or Ruby on Rails projects and not have to think about whether the right Ruby version and gemset is used.

# Gemsets duplicate gems

There are folks that say gemsets cause gem duplication and take up unnecessary space on your computer. So what?

This argument made sense a few decades ago when harddrive space was expensive. Today, storage is cheap. If duplication means taking up an extra gigabyte of space over dozens of gemsets, so be it.

I can always delete the gemset( rvm gemset delete gemset_name )I’m not using and restore space. In other words, pick the right battles to fight and don’t worry about things that don’t matter.