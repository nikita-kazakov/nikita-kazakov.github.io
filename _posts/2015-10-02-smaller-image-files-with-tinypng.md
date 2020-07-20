---
id: 235
title: Smaller image files with TinyPNG
date: 2015-10-02T00:00:00+00:00
author: Nikita Kazakov
excerpt: |
layout: post
guid: http://nikitakazakov.com/smaller-image-files-with-tinypng/
permalink: /smaller-image-files-with-tinypng/
restapi_import_id:
  - 5b79ddaa06ba5
  - 5b79ddaa06ba5
categories:
  - Uncategorized
tags:
  - "2015"
  - Web Development
---
<figure> 

![](http://nikitakazakov.com/wp-content/uploads/2018/08/fd9e9-0abxeryeplc7w15ok.jpg)  
</figure> 

I recently stumbled upon <a href="http://tinypng.com" target="_blank" rel="noopener noreferrer">TinyPNG</a> that has the ability to compress your images really well. The compression is lossy, but for the majority of the images I’ve processed, I couldn’t tell the difference. It works by “selectively decreasing the number of colors in the image” and supports png transparency. It also supports jpeg files.

### Usefulness

When I’m developing websites, I need to keep in mind that not all my viewers will have high speed internet. Making sure that images retain a small file size becomes important. Another reason for having a fast loading website is that search engines tend to rank websites based on page load speed.

After creating an image, I run it through this service to get a smaller image out, and then I use it on my sites.

Don’t run an image if it contains private information information on it. Perhaps I’m just paranoid, but I prefer to avoid sending that to another server.

### What about Photoshop’s “save for web” feature?

Apparently this feature in Photoshop is now considered legacy. It is <a href="http://blogs.adobe.com/crawlspace/2015/06/save-for-web-in-photoshop-cc-2015.html" target="_blank" rel="noopener noreferrer">no longer supported and has not been updated in ages.</a> Although that was my go-to tool, I’d rather use newer compression algorithms.

* * *

_Originally published at_ <a href="http://basicdrop.com" target="_blank" rel="noopener noreferrer"><em>www.basicdrop.com</em></a> _on October 2, 2015._