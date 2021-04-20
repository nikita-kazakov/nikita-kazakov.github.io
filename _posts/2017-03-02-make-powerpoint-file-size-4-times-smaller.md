---
title: Make PowerPoint file size 4 times smaller
date: 2017-03-02T00:38:37+00:00
layout: post
permalink: /make-powerpoint-file-size-4-times-smaller/
tags: tech
---

Bottom Line --- Your powerpoint file doesn't need to be 100 megabytes. You can quickly batch compress images within it to a reasonable size.

{% include image_center_caption.html
caption = ""
image = "/assets/images/imported/power-1.png"
%}

**How is this file 40MB?** This file is too damn big. I can't email it.

There were lots of images but they looked small in size. No way did they add up to 40MB.

I tried the PowerPoint compress option but it wasn’t good enough (22MB). **I found a way to half the size of the already compressed PowerPoint** without noticeably destroying image quality.<figure class="wp-caption"> 

{% include image_center_caption.html
caption = "From 40MB to 9MB in PowerPoint"
image = "/assets/images/imported/power-2.png"
%}

{% include image_center_caption.html
caption = "It does make the PointPoint smaller but we can half this size."
image = "/assets/images/imported/power-3.png"
%}

# 4x Smaller Method

Save your PowerPoint as *.pptx

Download <a href="http://www.rarlab.com/download.htm" target="_blank" rel="noopener noreferrer">WinRAR </a>and open your PowerPoint file.

It opens! The *.pptx file is actually a zip file.<figure class="wp-caption"> 

{% include image_center_caption.html
caption = "Opening PowerPoint with WinRAR. Go to ppt -> media. Those are all the images in your PowerPoint."
image = "/assets/images/imported/power-4.gif"
%}

**These image files are not optimized and are the problem.**

Copy the **media folder** to your desktop.

# Use TinyPNG.com to optimize images

Drag and drop the images into TinyPNG and download the optimized smaller images.<figure class="wp-caption"> 

{% include image_center_caption.html
caption = "Converting images using TinyPNG"
image = "/assets/images/imported/power-5.gif"
%}

Delete the original images from the media folder you opened in WinRAR and add back the optimized images.<figure class="wp-caption"> 

{% include image_center_caption.html
caption = "Deleting original images. Adding back the optimized images."
image = "/assets/images/imported/power-6.gif"
%}

That’s it! Check your file size. It should be smaller than what PowerPoint could do on its own and the images are in better quality.

**In my case, it was 4x smaller than the original.**

Here’s another example:<figure class="wp-caption"> 

{% include image_center_caption.html
caption = ""
image = "/assets/images/imported/power-7.png"
%}

*If the images are privacy sensitive, I wouldn’t use TinyPNG as your files will be uploaded to the server and converted. I’d use something like Photoshop instead.