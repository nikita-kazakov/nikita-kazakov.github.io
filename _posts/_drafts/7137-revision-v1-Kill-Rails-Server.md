---
id: 7138
title: Kill Rails Server
date: 2020-07-09T17:51:12+00:00
author: Nikita Kazakov
layout: revision
guid: https://nikitakazakov.com/7137-revision-v1/
permalink: /7137-revision-v1/
---
I create a ruby file named kill\_rails\_server.rb. I add:

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">system("kill -9 $(lsof -i tcp:3000 -t)")</pre>

Run that whenever you need to kill the server.