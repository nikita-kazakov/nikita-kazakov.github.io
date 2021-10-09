---
title: Changing git commit date
date: 2021-10-09
layout: post
permalink: /pass-ruby-variables-to-javascript
tags:
    - software dev
---

Sometimes I forget to commit my changes until days later. I prefer these commits show an accurate commit date.

You can change the commit date of any git commit with the `--date` flag.

```bash
# Change commit date to July 22, 2021.
git commit --date="2021-07-22" -m "add tracking code to website"
```