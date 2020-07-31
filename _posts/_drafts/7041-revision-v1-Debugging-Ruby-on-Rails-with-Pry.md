---
id: 7132
title: Debugging Ruby on Rails with Pry
date: 2020-06-23T21:44:54+00:00
author: Nikita Kazakov
layout: revision
guid: https://nikitakazakov.com/7041-revision-v1/
permalink: /7041-revision-v1/
---
Pry is a powerful Ruby debugger that is also available as a debugger for Rails using the [pry-byebug](https://github.com/deivid-rodriguez/pry-byebug) gem.

Rails already ships with a byebug debugger gem, however the addition of pry adds awesome syntax highlighting, scoping into a method or class, and running through stack traces.

When I&#8217;m writing code, I&#8217;m actively using pry to understand where I am in code, but to fix errors.

## Adding Pry to a Rails Project

Open your `Gemfile` and add `gem pry-byebug` to your development block. Why only the development block? Because you don&#8217;t want to expose a debugger gem in your production environment. If someone runs pry in production, they can change your code / have unauthorized access to your database.

You can also optionally add the `pry-rails` gem to the development group if you&#8217;d the Ruby console to have fantastic syntax highlighting.

<pre class="EnlighterJSRAW" data-enlighter-language="ruby" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">group :development do
  gem 'pry-rails'
  gem 'pry-byebug'
end</pre>

Run `bundle install`in the terminal to update the `Gemfile`.

## Disable Pry Pager

I highly suggest disabling pry pager as it drove me nuts because pry seemed unresponsive when outputting long results in the terminal that weren&#8217;t showing up.<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/05/May-10-2020-pry-paging-pain.gif" alt="" class="wp-image-7086" /> <figcaption>When your system has a pager enabled, Pry becomes a pain to scroll through. This is how it looks like.</figcaption></figure> 

When you see that colon, press `q` on your keyboard to scroll down all the way.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">Pry.config.pager = false
Pry.commands.alias_command 'c', 'continue'
Pry.commands.alias_command 's', 'step'
Pry.commands.alias_command 'n', 'next'</pre>

To avoid pressing `q` all the time, create a `.pryrc` file in your root Rails project folder. I like to disable the pager and alias the continue, step and break commands to single letters.

I felt like a weirdo when actively using a debugger while developing Rails until I saw this presentation about actively developing software with pry by Joel Turnbull. I&#8217;m not the only one!<figure class="wp-block-embed-youtube wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio">

<div class="wp-block-embed__wrapper">
  <div class="ast-oembed-container">
  </div>
</div></figure>