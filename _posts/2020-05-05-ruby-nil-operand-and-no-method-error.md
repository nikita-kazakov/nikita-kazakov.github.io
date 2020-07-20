---
id: 7064
title: 'Ruby nil, &#038;&#038; operand, and no method error'
date: 2020-05-05T18:02:27+00:00
author: Nikita Kazakov
layout: post
guid: https://nikitakazakov.com/?p=7064
permalink: /ruby-nil-operand-and-no-method-error/
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
I wanted to show a link in a Rails application based on whether a person was `current_user.admin?` and `signed_in?`

The code looked something like this:

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">= link_to "Admin Menu", root_path if current_user.admin? && signed_in?</pre>

That would work when I was signed in but as soon as I signed out, I&#8217;d get a no method error.

That happens because when you&#8217;re signed out, there is no `current_user`.

To fix this issue, I wrote a more verbose statement:

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">- if signed_in?
  - if current_user.admin?
    = link_to "Admin Menu", root_path</pre>

I first checked whether a user was `signed_in?`. If they were, then the `current_user` would be available and I could use it.

It works but we can shorten this code by understanding how the ruby `&&` operand is evaluated.

The `&&` operand goes through conditions in order. As soon as it receives a `false`, it returns `false`.

I had problems when evaluating the line below because `current_user` didn&#8217;t exist and Ruby raised an error.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group=""># No method error
current_user.admin? && signed_in?</pre>

However, when I switched the order of these two statements, the error went away.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group=""># works perfectly
signed_in? && current_user.admin?</pre>

This works because the method `signed_in?` will always return a true or false, regardless of whether we&#8217;re signed in or not.

When `signed_in?` is true, Ruby continues to evaluate the second statement `current_user.admin?`. 

When `signed_in?` is false, Ruby doesn&#8217;t even look at `current_user.admin?` and simply returns false. This is why the line below works:

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">= link_to "Admin Menu", root_path if signed_in? && current_user.admin?</pre>

## Safe navigation operator and try

Another alternative is to use the safe navigation operator. If `current_user` doesn&#8217;t exist, you can ask Ruby to fail silently with a nil instead of a no method error.

You can call the `try` method and pass in the method you&#8217;re checking. If it doesn&#8217;t exist, Ruby will return nil instead of an error.

In Ruby 2.3, you can use the shorthand safe navigation operator `&`. Behind the scenes, `&` invokes the `try!` method. 

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">current_user.blah? # No Method Error
current_user.try(:blah) #nil
current_user&.blah #nil</pre>

You can also daisy chain `try` and `&`

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">current_user.try(:blah).try(:fake_method) #nil
# or use the safe navigation operator
current_user&.blah&.fake_method #nil</pre>