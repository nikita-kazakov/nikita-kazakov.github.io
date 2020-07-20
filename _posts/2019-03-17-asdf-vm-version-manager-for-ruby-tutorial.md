---
id: 6677
title: ASDF VM Version Manager for Ruby Tutorial
date: 2019-03-17T15:29:46+00:00
author: Nikita Kazakov
layout: post
guid: https://nikitakazakov.com/?p=6677
permalink: /asdf-vm-version-manager-for-ruby-tutorial/
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
Using a version manager is critical if you plan on running different projects from GitHub. A project might not be compatible with the version of Ruby you have installed.

We need a way to switch between versions of Ruby without installing and uninstalling them every time. 

I&#8217;ll show you how to switch versions easily using [ASDF-VM](https://asdf-vm.com), a version manager for Ruby and other languages.

Make sure your machine doesn&#8217;t have Ruby installed. Let’s install <a rel="noreferrer noopener" target="_blank" href="https://asdf-vm.com">ASDF-VM</a>.

Although ASDF-VM is not the only version manager on the block, I prefer it because it is easy to install and use. Other popular version managers like <a rel="noreferrer noopener" target="_blank" href="https://rvm.io/">RVM </a>or <a rel="noreferrer noopener" target="_blank" href="https://github.com/rbenv/rbenv">RBENV</a> also do the job.

I’m <a rel="noreferrer noopener" target="_blank" href="https://asdf-vm.com/#/core-manage-asdf-vm">using these instructions</a> to install ASDF-VM below.

Open your terminal and clone the latest ASDF-VM branch.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">﻿git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.7.2</pre>

Let’s add ASDF-VM to our shell so we can run it from any folder.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">echo -e '\n. $HOME/.asdf/asdf.sh' >> ~/.bashrc
echo -e '\n. $HOME/.asdf/completions/asdf.bash' >> ~/.bashrc</pre>

To take effect, close your terminal window and reopen it again. &nbsp;Run:

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">asdf</pre>

You&#8217;ll see something like this:<figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559603244682_image.png) </figure> 

ASDF-VM doesn’t have a GUI interface and those are the commands you can run it with.

Let&#8217;s install Ruby dependencies before installing Ruby.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">sudo apt install build-essential
sudo apt install zlib1g-dev libssl-dev libreadline-dev libgdbm-dev</pre>

We want to install the ASDF-VM ruby plugin. 

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">asdf plugin-add ruby</pre>

  
Let&#8217;s install Ruby through ASDF-VM.  I want to install Ruby version 2.6.2. <a rel="noreferrer noopener" target="_blank" href="https://www.ruby-lang.org/en/downloads/releases/">Other versions are available</a> depending on what you want to run.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">asdf install ruby 2.4.4 </pre>

Run ASDF again and see other commands available to manage your Ruby package.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">asdf</pre><figure class="wp-block-image">

![](https://paper-attachments.dropbox.com/s_B4F8639630B0FBC36DFABA0ACADCD708C18AE4C40D59D285D20FE9A240094838_1559652951496_image.png) </figure> 

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">asdf current</pre>

This tells you that no version is set for Ruby on this machine. &nbsp;To check available versions, run:

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">﻿asdf list ruby</pre>

You’ll see 2.6.2. Let’s set it as the global (screenshot shows local) version to use.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">Asdf global ruby 2.6.2</pre>

Double check:

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">﻿asdf current</pre>

It should say Ruby 2.6.2. To triple check, go ahead and run the version command on Ruby itself in the terminal.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">﻿ruby -v</pre>

Ruby 2.6.2 is installed and is active.