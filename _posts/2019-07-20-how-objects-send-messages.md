---
id: 6978
title: How objects send messages in Ruby
date: 2019-07-20T13:22:00+00:00
author: Nikita Kazakov
layout: post
guid: https://nikitakazakov.com/?p=6978
permalink: /how-objects-send-messages/
site-sidebar-layout:
  - default
site-content-layout:
  - default
theme-transparent-header-meta:
  - default
categories:
  - Uncategorized
---
If open IRB (interactive ruby) and type in the following expression `2 + 3`, you&#8217;ll get `5`. If you reverse that with `3 + 2`, you&#8217;ll still get `5`.

Numbers are just one of the many types of objects in Ruby. Whole numbers are an **Integer** type of object.

<pre class="EnlighterJSRAW" data-enlighter-language="ruby" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">2.class     # Integer
4.class     # Integer
32.class    # Integer
2392.class  # Integer</pre>

So what is really happening when you type in `2+3`?<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/02/image-29-1024x556.png" alt="" class="wp-image-6982" srcset="https://nikitakazakov.com/wp-content/uploads/2020/02/image-29-1024x556.png 1024w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-29-300x163.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-29-768x417.png 768w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-29-1536x834.png 1536w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-29.png 1620w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">2 + 3
# Returns 5. But it can be rewritten like this
# to see explicitly how +(3) is actually a message sent
# to the 2 object. 
2.+(3)</pre>

A `+(3)` message is sent to the object `2`. The outer circle shows that the Integer object knows how to handle the `-`, `+`, and `=` message.

The `2` object receives the `+ 3` message. `+` is the message and `3` is the object passed as the parameter with that message. After the message is received, the `2` object returns a new object `5`.

That&#8217;s what is meant by everything is an object. You&#8217;re sending messages to objects and you&#8217;re receiving objects.

Ruby is an expressive language and uses what&#8217;s called _syntactic sugar_ to make certain things appear cleaner to programmers.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">2.+(3) #Without syntactic sugar.
2 + 3 # With Ruby's syntactic sugar. 
</pre>

So what happens when you do `3 + 2`? You&#8217;re sending a `+2` message to the `3` object and it returns a `5` object.

Same idea with any math operations.

Notice that Integer objects are **immutable**&#8211;they don&#8217;t change. When you take `3` and send a `+2` message to it, `3` doesn&#8217;t change. Instead, it returns a new Integer object `5`.

Not all objects are immutable. If we look at a cash register object and send a message `deposit(50)`, the cash value of the object will change. The cash register object is mutable.<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/02/image-30-1024x351.png" alt="" class="wp-image-6984" srcset="https://nikitakazakov.com/wp-content/uploads/2020/02/image-30-1024x351.png 1024w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-30-300x103.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-30-768x263.png 768w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-30-1536x526.png 1536w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-30.png 1646w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

## Stacking Messages

You can also stack messages together on one line.

What happens when you `20 + 10 - 5`?

`20` object receives `+(10)` message. It returns a `30` object. The `30` object receives a `-(5)` message and returns a `25` object.

The object is always on the left and the message is followed by a `.` and a message.

Here&#8217;s how it would look like without Ruby syntactic sugar:

<pre class="EnlighterJSRAW" data-enlighter-language="ruby" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">20 + 10 - 5    # 25 (With syntactic sugar)
20.+(10).-(5)  # 25 (What's actually happening without syntactic sugar)</pre>

## Custom adding method

To drive the point home, let&#8217;s create another way to add numbers in Ruby. Instead of doing `2 + 3`, we&#8217;ll add a new method to the Integer class called `add`.

It&#8217;s frowned upon to _monkey patch_ an existing object with custom methods.

We open up the Integer class and write a `add` method. It will do the same thing as `+` method does. 

<pre class="EnlighterJSRAW" data-enlighter-language="ruby" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">class Integer
  def add(num)
    self + num
  end
end</pre>

It takes itself and adds the given parameter to itself.

<pre class="EnlighterJSRAW" data-enlighter-language="ruby" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">2.add(3)
# 5</pre>

Even the `+` method itself can be modified to give strange results. We can modify the `+` to multiply the two numbers instead.

<pre class="EnlighterJSRAW" data-enlighter-language="ruby" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">class Integer
  def +(num)
    self * num
  end
end

2 + 6  # 12
3 + 5  # 15</pre>

This is why Ruby is flexible. Nothing is sacred and all objects can be dissected and modified. In practice however, you won&#8217;t see developers doing this to standard Ruby objects.

## Strings are objects

Strings are also objects in Ruby.

<pre class="EnlighterJSRAW" data-enlighter-language="ruby" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">puts "hello world"
# outputs hello world on the screen</pre>

`"hello world"` is a string object in Ruby.

<pre class="EnlighterJSRAW" data-enlighter-language="ruby" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">"hello world".class
#String</pre>

Ruby applies syntactic sugar when you type in `"hello world"`. What&#8217;s really happening in the background is the string object is created like this `String.new("hello world")`.

`"hello world"` is then sent as a message to `puts` which displays the string on your screen.

## Why objects?

It&#8217;s because we have an intuitive sense of what objects are in the world. An apple is an object. It has properties like color or a type of apple. You can do something to it (bite it) and it can do something to you (act on your taste buds).

Object oriented programming sets up a framework for describing how pieces of an application talk to each other. It creates a familiar structure of understanding.