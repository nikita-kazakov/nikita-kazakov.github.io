---
title: Do I need to use semicolons in Javascript?
date: 2020-09-20
layout: post
permalink: /javascript-semicolons/
tags: javascript
---

Bottom Line — If you don’t use semicolons --- remember not to start a JavaScript line with ` [ ( ` `.

It’s a heated debate but both sides have valid points.

# People for semicolons

Javascript will automatically insert semicolons where they are missing using Automatic Semicolon Insertion (ASI). However, there are edge cases where it doesn’t do what you want it to do and code errors occur.

Some folks who prefer using semicolons come from other languages that use semicolons. It’s natural to them. It’s an equivalent of a period signifying the end of a statement.

It’s not natural for me to use semicolons because I come from Ruby — a language that doesn’t use them.

# People against semicolons

These folks see semicolons are unneeded syntax because ASI will add them automatically. 

They might come from a language like Python or Ruby that don’t use semicolons. Semicolons are additional mental overhead.

The good news is that it is possible to write JavaScript without semicolons and not get into trouble.

That simple rule is to never start a new line with: `[`, `(`, or ```. [Taken from Feross](https://feross.org/never-use-semicolons/))

# Javascript Linters

Use a linter when writing JavaScript. Ruby has RuboCop and JavaScript has linters available that will check your syntax and style as you write code.

{% include embed_youtube.html id="gsfbh17Ax9I" %}

# Conclusion

Make your own decision as to what is comfortable for you. Either way — make sure you understand how ASI works and where it fails. 

For now, I’ll go with the non-semicolon route until it fails me.
