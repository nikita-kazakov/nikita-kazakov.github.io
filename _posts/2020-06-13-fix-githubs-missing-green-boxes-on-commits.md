---
id: 7123
title: 'Fix Github&#8217;s missing green boxes on commits'
date: 2020-06-13T03:30:39+00:00
author: Nikita Kazakov
layout: post
guid: https://nikitakazakov.com/?p=7123
permalink: /fix-githubs-missing-green-boxes-on-commits/
site-sidebar-layout:
  - default
site-content-layout:
  - default
theme-transparent-header-meta:
  - default
categories:
  - Uncategorized
tags:
  - Software Development
---
When I setup a new development environment, I&#8217;ll commit my code to GitHub but the green boxes won&#8217;t show my contribution for that day.<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/06/image.png" alt="" class="wp-image-7125" srcset="https://nikitakazakov.com/wp-content/uploads/2020/06/image.png 705w, https://nikitakazakov.com/wp-content/uploads/2020/06/image-300x108.png 300w" sizes="(max-width: 705px) 100vw, 705px" /> </figure> 

It&#8217;s usually because my git email / name is incorrect. The fix is pretty simple. Type the following into the command line:

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">git config --global user.name "Your Name"
git config --global user.email "yourgithubaccountemail@blah.com"</pre>

Try to commit and push your code again to see if your contributions are now showing.

Another reason for contributions not showing up is if you&#8217;re pushing code to a branch other than master.