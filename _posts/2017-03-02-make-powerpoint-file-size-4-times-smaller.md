---
id: 291
title: Make PowerPoint file size 4 times smaller
date: 2017-03-02T00:38:37+00:00
author: Nikita Kazakov
excerpt: |
layout: post
guid: http://nikitakazakov.com/make-powerpoint-file-size-4-times-smaller/
permalink: /make-powerpoint-file-size-4-times-smaller/
restapi_import_id:
  - 5b79ddaa06ba5
  - 5b79ddaa06ba5
categories:
  - Uncategorized
tags:
  - "2017"
  - PowerPoint
  - Presentations
  - Web Development
---
<figure> 

![](http://nikitakazakov.com/wp-content/uploads/2018/08/ac551-1qcgv2znbifthrx9ukcga4w.png)  
</figure> 

**How is this file 40MB?** This file is overflowing with image bureaucracy. I can’t email this PowerPoint.

There were lots of images but they looked small in size. No way did they add up to 40MB.

I tried the PowerPoint compress option but it wasn’t good enough (22MB). **I found a way to half the size of the already compressed PowerPoint** without noticeably destroying image quality.<figure class="wp-caption"> 

![](http://nikitakazakov.com/wp-content/uploads/2018/08/9b7c7-1sxooqbv2lb-zfpldimncfa.png) <figcaption class="wp-caption-text">From 40MB to 9MB in PowerPoint</figcaption></figure> <figure class="wp-caption"> 

![](http://nikitakazakov.com/wp-content/uploads/2018/08/88938-1jwpgijakuy7wteanosmqzg.png) <figcaption class="wp-caption-text">It does make the PointPoint smaller but we can half this size.</figcaption></figure> 

### 4x Smaller Method

Save your PowerPoint as *.pptx

Download <a href="http://www.rarlab.com/download.htm" target="_blank" rel="noopener noreferrer">WinRAR </a>and open your PowerPoint file.

It opens! The *.pptx file is actually a zip file.<figure class="wp-caption"> 

![](http://nikitakazakov.com/wp-content/uploads/2018/08/2d601-1h9pn4rzix275zoyykrsajw.gif) <figcaption class="wp-caption-text">Opening PowerPoint with WinRAR. Go to ppt -> media. Those are all the images in your PowerPoint.</figcaption></figure> 

**These image files are not optimized and are the problem.**

Copy the **media folder** to your desktop.

### Use TinyPNG.com to optimize images

<a href="https://tinypng.com/" target="_blank" rel="noopener noreferrer">TinyPNG.com</a> works magic with png and jpeg files and **makes them smaller**. It will compress them but you likely **won’t see the difference visually**.

Drag and drop the images into TinyPNG and download the optimized smaller images.<figure class="wp-caption"> 

![](http://nikitakazakov.com/wp-content/uploads/2018/08/7f4c7-1ilw-qvaxnesz_tnda3g8la.gif) <figcaption class="wp-caption-text">Converting images using TinyPNG</figcaption></figure> 

Delete the original images from the media folder you opened in WinRAR and add back the optimized images.<figure class="wp-caption"> 

![](http://nikitakazakov.com/wp-content/uploads/2018/08/4442b-1bmal7u0r0nwgenw0ivr8ew.gif) <figcaption class="wp-caption-text">Deleting original images. Adding back the optimized images.</figcaption></figure> 

That’s it! Check your file size. It should be smaller than what PowerPoint could do on its own and the images are in better quality.

**In my case, it was 4x smaller than the original.**

Here’s another example:<figure class="wp-caption"> 

![](http://nikitakazakov.com/wp-content/uploads/2018/08/31af3-1xzfsywmso6pmlqk3womyzg.png) <figcaption class="wp-caption-text">From 8 MB to 2.5 MB in PowerPoint</figcaption></figure> 

*If the images are privacy sensitive, I wouldn’t use TinyPNG as your files will be uploaded to the server and converted. I’d use something like Photoshop instead.