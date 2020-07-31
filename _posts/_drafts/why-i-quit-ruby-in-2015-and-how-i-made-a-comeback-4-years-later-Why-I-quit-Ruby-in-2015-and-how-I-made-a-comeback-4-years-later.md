---
id: 6706
title: Why I quit Ruby in 2015 and how I made a comeback 4 years later
date: 2019-05-02T15:58:40+00:00
author: Nikita Kazakov
layout: post
guid: https://nikitakazakov.com/?p=6706
permalink: /why-i-quit-ruby-in-2015-and-how-i-made-a-comeback-4-years-later/
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
Product management was getting stale and I wanted to learn software development. I convinced myself to learn software development although I wasn’t exactly sure where to begin.

Ruby on Rails was a hot framework and that&#8217;s what I would learn. My goal was to start with Ruby the language before starting to learn the Rails framework.

I bought an online Ruby course on July 2015. One month later, I quit.

I quit because I was quickly overwhelmed. It’s one thing to know variables, loops, and blocks. The difficult task is to understand how classes and objects send messages to each other. Throw in setters, getters, and attribute readers, writers, and accessors and it was a recipe for saying screw it, this is too complicated.

I took on Test Driven Development (TDD) while making sense of Ruby. That was a mistake. I couldn&#8217;t see what was testing and what was code.

I was building a text based game and while I could follow directions and type along with the instructor, things fell apart when I tried to build an analog game from scratch.

It was like trying to sip gushing water from a fireman&#8217;s hose.

I quit.

# Returning to Ruby in 2019

Four years passed since I quit Ruby. 

I continued <a rel="noreferrer noopener" aria-label="shipping software as a product manager (opens in a new tab)" href="https://nikitakazakov.com/projects/" target="_blank">shipping software as a product manager</a> in the Oil and Gas industry. As a product manager, its was my job to gather customer requirements and work with my developers to ship software.

But I&#8217;m an engineer and I like to building things. As a developer, you build. You take a programming language and like lego pieces, you build something useful. I felt left out because I couldn&#8217;t build alongside my developers.

A pull in my gut kept nudging me to give software development another chance.

This time I made it. I came back to Ruby by thinking differently. I published my first <a rel="noreferrer noopener" target="_blank" href="https://github.com/nikita-kazakov/Pragmatic-Ruby-Game">text based game as a Ruby gem in March 2019</a>. 

Here’s what worked for me.

# Start from scratch

If you’re new to software development and Ruby is your first language, do not start by learning a framework (Ruby on Rails). You won&#8217;t tell apart what&#8217;s Ruby and what&#8217;s Rails. That’s like telling a baby to jog before crawling. 

Start with the principles of programming first. I highly recommend working through <a rel="noreferrer noopener" target="_blank" href="https://pragprog.com/titles/ltp2/learn-to-program-2nd-edition">Chris Pine’s Learn to Program</a> book. 

Just a fair warning, I stopped reading it by Chapter 9 because it went from zero to _what the heck kind of wizardry is this._ 

# Pragmatic Studio Ruby

I came back to the <a href="https://pragmaticstudio.com/ruby" target="_blank" rel="noreferrer noopener" aria-label="Pragmatic Studio Ruby Course (opens in a new tab)">Pragmatic Studio Ruby Course</a>. Four years ago I gave up on it. This time, concepts were familiar because I read Chris Pine’s Learn to Program book.

In the online course, I worked alongside with the instructors, Mike and Nicole, and slowly added more features to the game until it was complete.

I found <a rel="noreferrer noopener" target="_blank" href="https://launchschool.com/books/ruby/read/introduction">Launch School’s Intro to Ruby book</a> useful as a reference, especially when learning about classes, modules, and objects.

## Skip Test Driven Development (TDD)

If you&#8217;re new to development, <a href="https://nikitakazakov.com/why-skip-testing-if-youre-new-to-software-development/" target="_blank" rel="noreferrer noopener" aria-label="don’t learn testing and development at the same time (opens in a new tab)">don’t learn testing and development at the same time</a>. Just focus on learning Ruby.

I quit Ruby in 2015 because I tried to bite off more than I could chew by learning Ruby and TDD simultaneously.

You’ll have time to come back to testing after you’ve picked up Ruby.

## Use a featured IDE

There’s no shame in using the right tools to help you. Before using RubyMine IDE, I used SublimeText. Although it could be customized for a Ruby environment with plugins, it wasn&#8217;t _plug and play_.

In 2019, I started using RubyMine and it made all the difference. IntelliJ autocomplete was a game changer because I didn&#8217;t have to remember Ruby methods as they would pop up as I started typing.

GUI portion of version control let me commit and push code to GitHub without using the command line interface.

## Use a local environment

Take time to <a rel="noreferrer noopener" target="_blank" href="https://nikitakazakov.com/how-to-install-rubymine-and-setup-a-ruby-environment-on-linux/">setup a local environment for yourself</a> because that’s where you’ll be building future projects anyway.

You have less control over what can be installed with online IDE&#8217;s such as AWS&#8217;s cloud9

## Use Git Version Control

I encourage you to learn the basics of Git. Git is used for code version control. It’s software industry standard.

Remember writing that last minute term paper in high school? Recall how you probably made multiple files:  


  * history\_paper\_v1.txt
  * history\_paper\_v2.txt
  * history\_paper\_v2_final.txt
  * history\_paper\_v2_really final.txt

You were version controlling your term paper.

I recommend watching <a rel="noreferrer noopener" target="_blank" href="https://www.youtube.com/watch?v=BCQHnlnPusY&list=PLRqwX-V7Uu6ZF9C0YMKuns9sLDzK6zoiV&index=1">Coder Train’s Git and Github for Poets Series</a> as a solid starting point.

Push your project to GitHub to keep track of your work. From day one, there’s a paper trail to what you’re doing. You’re building a portfolio right away. Those green boxes are addicting.<figure class="wp-block-image">

<img src="https://nikitakazakov.com/wp-content/uploads/2019/06/s_7CC72309B722DC1CE4F1420DA341449D7FB673CD5CA7F23DE5DF9ACECF69B390_1560611464752_image.png" alt="" class="wp-image-6748" srcset="https://nikitakazakov.com/wp-content/uploads/2019/06/s_7CC72309B722DC1CE4F1420DA341449D7FB673CD5CA7F23DE5DF9ACECF69B390_1560611464752_image.png 860w, https://nikitakazakov.com/wp-content/uploads/2019/06/s_7CC72309B722DC1CE4F1420DA341449D7FB673CD5CA7F23DE5DF9ACECF69B390_1560611464752_image-300x76.png 300w, https://nikitakazakov.com/wp-content/uploads/2019/06/s_7CC72309B722DC1CE4F1420DA341449D7FB673CD5CA7F23DE5DF9ACECF69B390_1560611464752_image-768x196.png 768w" sizes="(max-width: 860px) 100vw, 860px" /> </figure> 

# Learn to Teach

As I continued Pragmatic Studio’s Ruby Course, I’d make notes, screenshots and drawings for myself.

I used Google Docs but recently I’ve been using Dropbox Paper for writing blog posts.

I had close to 150 pages on google docs referencing Ruby.

When I start a new project and I get stuck, I reference my notes. When you take notes while learning, your understanding and recall is greater.

Write your notes as if you’re teaching the material to yourself. If you find a tip or trick, note it down.

After getting comfortable with Ruby, I found my notes were truly valuable when I started writing technical blog posts.

You won’t have writer’s block. Just look back at your notes and a large number of ideas are staring right at you. You’ll realize you’ve learned a lot and you have a different perspective to share with other newcomers.

# Takeaway

What kills your progress is overwhelming yourself. If you’re learning Ruby, reduce friction by using tools that simplify workflows.

You can learn the complicated stuff later.