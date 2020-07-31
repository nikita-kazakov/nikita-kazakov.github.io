---
id: 7051
title: Git for dummies
date: 2020-05-04T01:46:03+00:00
author: Nikita Kazakov
layout: revision
guid: https://nikitakazakov.com/7046-revision-v1/
permalink: /7046-revision-v1/
---
I&#8217;ve been programming for two years and it wasn&#8217;t until last month that I started to understand git beyond `git pull`, `git merge`, and `git push`. Git scared me.

You try to push your changes and you get messages like:

  * You are now in a detached head state.
  * merge conflicts

Until you visualize the git model, you&#8217;ll be stuck with fear. The model is not difficult to grasp. 

My goal is to explain it the way I understand it. 

At the early stages of programming, there&#8217;s just too much to learn and becoming a git pro won&#8217;t make you a better developer.

However, if you&#8217;ll be working with multiple developers on a single project, you&#8217;ll need to learn how to use git.

## What is git?

Git is a distributed revision control system. That&#8217;s it, easy stuff right?

That sounds complicated and confusing. Let&#8217;s take baby steps and forget the _distributed_ part.

Forget about commits and branches for now.

At the very core, git is a [stupid content tracker](https://git-scm.com/docs/git). Git is tracks content. You&#8217;ve done this before yourself. That&#8217;s called **version control.**

You&#8217;ve done version control yourself. If you&#8217;ve used **Save As** in Word and have saved your documents as:

  * lit\_project\_v1
  * lit\_project\_v2
  * lit\_project\_v3_final

You were using version control. You kept versions of your lit report in case something happened to version 3, you were able to recover yourself to version 2.

Git does this for you. The benefit with git is that you can do this type of version control with _multiple_ people working on the same files. 

Imagine how hard that would be by using **save as** and sending files by email between people.

By the way, git is not the only version control around but it is the most common one today and is worth understanding.

## Git is a map

Git is a map that holds two things: The content of your files and the location of those files. 

It stores this information in a dictionary / hash of keys and values.

Values are bytes of data from the files that you&#8217;re storing. Those files could be music, text, web page or anything else.

You provide git any file and it will generate a hash key for it. That key is a 40 hex-character hash generated with a SHA1 algorithm. That key is unique. It&#8217;s [practically impossible](https://security.stackexchange.com/a/29073) that this key will ever collide with another generated SHA1 hash.

## Install Git

## Storing things with Git

To use git version control on your project, we need to initialize git. Create a folder where you&#8217;ll be putting all your project files and open up the terminal in that folder. To initialize git, type in:

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">git init</pre>