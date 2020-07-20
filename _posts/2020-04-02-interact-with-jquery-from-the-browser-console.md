---
id: 7117
title: Interact with JQuery from the browser console
date: 2020-04-02T22:28:00+00:00
author: Nikita Kazakov
layout: post
guid: https://nikitakazakov.com/?p=7117
permalink: /interact-with-jquery-from-the-browser-console/
site-sidebar-layout:
  - default
site-content-layout:
  - default
theme-transparent-header-meta:
  - default
categories:
  - Uncategorized
---
I recently stumbled on this technique where you can load JQuery for ANY page and write JQuery commands right in the browser console. This is great for debugging and exploration.

## Method 1 &#8211; Bookmark Injector

Straight from [this post on stack overflow](https://stackoverflow.com/a/7474386). Create a bookmark in your browser and for the url, paste in:

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">javascript:(function(e,s){e.src=s;e.onload=function(){jQuery.noConflict();console.log('jQuery injected')};document.head.appendChild(e);})(document.createElement('script'),'//code.jquery.com/jquery-latest.min.js')</pre>

Click on the bookmark and look at your console. You&#8217;ll notice it says &#8220;jQuery injected&#8221;. That&#8217;s it, you can now inject JQuery with a single click on any page.

## Method 2 &#8211; Copy / Paste JQuery.min

If the above method didn&#8217;t work for you, you can copy the `jquery.min.js` contents right into the console. This will load up JQuery on any page. I noticed that this method crashes my browser after a few minutes. I don&#8217;t use this method and your results may vary.