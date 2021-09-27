---
title: Fix GitHub missing green boxes on commits
date: 2020-06-13T03:30:39+00:00
layout: post
permalink: /fix-githubs-missing-green-boxes-on-commits/
tags:
  - software dev
---

When I setup a new development environment, I’ll commit my code to GitHub but the green boxes won’t show my contribution for that day.

{% include image_center_caption.html 
    caption = "Github green boxes."
    image = "/assets/images/2020/git_green_boxes.png"
    alt = "Github commit boxes."
%}

It’s usually because my git email / name is incorrect. The fix is pretty simple. Type the following into the command line:

```
git config --global user.name  "Your Name"
git config --global user.email  "yourgithubaccountemail@blah.com"
```

Try to commit and push your code again to see if your contributions are now showing.

Another reason for contributions not showing up is if you’re pushing code to a branch other than master.
