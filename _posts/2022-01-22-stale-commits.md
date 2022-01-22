---
title: Don't leave stale commits in the main branch
date: 2022-01-22
layout: post
permalink: /stale-commits-in-main
tags:
- software dev
---

The problem happens when several pull requests are merged into main and they aren't deployed to production right away. A developer comes along and merges their pull request and deploys the main branch to production assuming only their changes were merged.

The production server starts to throw errors. The developer assumes it's their fault but the code is throwing errors in places they didn't touch.

It wasn't their fault. Other developers didn't stick around to deploy their code and this developer got stuck holding the bag.

# Solution

Treat the main branch as a sacred branch. 
Don't merge your pull requests into the main branch unless you are ready to deploy it to production **right away**. 
This means you're ready to monitor errors right after you deploy for at least 15 minutes. Your teammates will thank you.