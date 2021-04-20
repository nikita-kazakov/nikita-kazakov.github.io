---
title: ASDF VM Version Manager for Ruby Tutorial
date: 2019-03-17T15:29:46+00:00
layout: post
permalink: /asdf-vm-version-manager-for-ruby-tutorial/
tags:
  - ruby
---

Bottom Line --- You'll need a Ruby version manager if you plan on working with Ruby and Rails.

**2020 Update**: I don't use ASDF anymore. I use [RVM](/how-to-ruby-rvm/) for Ruby / Rails projects.
{: .notice--info}

Using a version manager is critical if you plan on running different projects from GitHub. A project might not be compatible with the version of Ruby you have installed.

We need a way to switch between versions of Ruby without installing and uninstalling them every time.

I’ll show you how to switch versions easily using [ASDF-VM](https://asdf-vm.com), a version manager for Ruby and other languages.

Make sure your machine doesn’t have Ruby installed. Let’s install [ASDF-VM](https://asdf-vm.com).

Although ASDF-VM is not the only version manager on the block, I prefer it because it is easy to install and use. Other popular version managers like [RVM](https://rvm.io/) or [RBENV](https://github.com/rbenv/rbenv) also do the job.

I’m [using these instructions](https://asdf-vm.com/#/core-manage-asdf-vm) to install ASDF-VM below.

Open your terminal and clone the latest ASDF-VM branch.

```bash
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.7.2
```

Let’s add ASDF-VM to our shell so we can run it from any folder.

```bash
echo -e '\n. $HOME/.asdf/asdf.sh' >> ~/.bashrc
echo -e '\n. $HOME/.asdf/completions/asdf.bash' >> ~/.bashrc
```

To take effect, close your terminal window and reopen it again. Run `asdf`.

You’ll see something like this:

{% include image_center_caption.html
caption = ""
image = "/assets/images/imported/asdf-1.png"
%}

ASDF-VM doesn’t have a GUI interface and those are the commands you can run it with.

Let’s install Ruby dependencies before installing Ruby.

```bash
sudo apt install build-essential
sudo apt install zlib1g-dev libssl-dev libreadline-dev libgdbm-dev
```

We want to install the ASDF-VM ruby plugin.

```bash
asdf plugin-add ruby
```

Let’s install Ruby through ASDF-VM. I want to install Ruby version 2.6.2. [Other versions are available](https://www.ruby-lang.org/en/downloads/releases/) depending on what you want to run.

```bash
asdf install ruby 2.4.4
```

Run ASDF again and see other commands available to manage your Ruby package.

```bash
asdf
```

{% include image_center_caption.html
caption = ""
image = "/assets/images/imported/asdf-2.png"
%}

```bash
asdf current
```

This tells you that no version is set for Ruby on this machine. To check available versions, run:

```bash
asdf list ruby
```

You’ll see 2.6.2. Let’s set it as the global (screenshot shows local) version to use.

```bash
asdf global ruby 2.6.2
```

Double check:

```bash
asdf current
```

It should say Ruby 2.6.2. To triple check, go ahead and run the version command on Ruby itself in the terminal.

```bash
ruby -v
```

Ruby 2.6.2 is installed and is active.
