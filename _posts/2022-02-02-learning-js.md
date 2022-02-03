---
title: How I'd learn Javascript in 2022
date: 2022-02-02
layout: post
permalink: /learning-javascript
tags:
- software dev
- javascript
---

This is the advice I'd give to someone trying to learn or brush up on Javascript fundamentals in 2022.

YouTube videos and internet articles didn't do it for me. I had fundamental gaps and practice problems were missing from random tutorials.

Here's what made Javascript ES6 click into place for me.

# Web Bos's Beginner Javascript Course

I'm a Ruby on Rails developer and I've been able to get by with minimal Javascript over the years. Sprinkles of JQuery were enough.

With the world moving to SPAs (single page applications), I knew I had gaps. ES6 release made Javascript easier to work.

I bought and worked through the [Wes Bos's Beginner Javascript](https://beginnerjavascript.com/) course.

This course was a game-changer for me. It filled the gaps around events, promises, event-driven Javascript, and other fundamentals.

Wes is a great instructor. It felt as if he was sitting next to me and explaining concepts I'd actually use rather than re-hashing ideas from a reference book.

The practice exercises were top notch. I also look forward to doing his [Build 30 things in 30 days in Javascript](https://javascript30.com/) at some point.

# Functional Programming in Javascript

I'm comfortable with Ruby. Ruby is an object oriented language.

Javascript ES6 introduced classes. I thought I could get away with using classes in Javascript. Wrong. I ran into edge cases where OOP (object oriented programming) in Javascript resulted in quirky behavior.

Doug Crockford, the author of _Javascript --- The Good Parts__  recommends avoiding they keyword `this`, classes, and various other things in [Javascript --- The Better Parts (2018)](https://youtu.be/XFTOG895C7c) presentation.

[Fun Fun Function has a great series](https://www.youtube.com/playlist?list=PL0zVEGEvSaeEd9hlmCXrk5yUyqUag-n84) on functional Javascript as an alternative to OO Javascript. I've been using these techniques and found code to be less error prone.

ReactJS has also switched away from classes to hooks. That's another anecdotal reason to avoid using classes in Javascript.

# Event Loop Video
Are you frustrated with the asynchronous nature of Javascript? Is your code littered with `setTimeOut` to wait for something to happen? Mine was also.

Until you understand the Javascript event loop, you'll continue coding in frustration.

Watch this excellent presentation by Philip Roberts [What the Heck is the Event Loop Anyway?](https://youtu.be/8aGhZQkoFbQ)

Combine your new knowledge with Javascript promises and you'll no longer use `setTimeOut`.