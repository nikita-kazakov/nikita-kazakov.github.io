---
title: How to iterate less on code reviews
date: 2021-03-09
layout: post
permalink: /code-review-iterate-less/
tags: 
    - software development
---

Bottom Line - Don't involve the reviewer prematurely in product management / feature iterations.

# How to iterate less on code reviews

Having at least one other developer review your code and approve it before merging it into production is a good idea. 

## Immediate Approval

The shortest iteration is a thumbs up approval and a merge.

- **Bob** - requests a review
- **You** - review and approve
- code is merged.

## Requested Changes
A longer iteration is a code review with suggestions and requested changes. 

- **Bob** - requests a review
- **You** - review and suggest changes
- **Bob** - makes changes
- **You** - review code / changes and approve
- code is merged.

With requested changes, the reviewer has to look at the pull request code twice before it can be merged.

## Unsustainable iterations

The reviewer doesn't know the entire codebase. He'll have to review code he's not familiar with.

- **Bob** - requests a review
- **You** - review and suggest changes
- **Bob** - makes changes
- **You** - review code / changes and approve
- **Bob** - puts the code on a staging server for a product manager to QA functionality / feature requirements.
- **PM** - finds problems and asks Bob to fix them.
- **Bob** - fixes problems.
- **You** - review code yet again, for the third time. Approve.
- code is merged.

This is a tedious cycle. The reviewer has to look at the code three separate times, usually on different days. The reviewer is likely reviewing multiple pull requests and context switching between all of them is PAINFUL.

## Solution

Bob shouldn't be asking for a pull request review prematurely. Bob should be iterating with the product manager directly until the product manager approves all the functionality in the pull request.

The pull request reviewer doesn't know about Bob's user story. They don't intimately know what the product requirements are. The product manager does however.

- **PM** - Assigns feature ticket to Bob.
- **Bob** - Completes code for ticket and puts the feature on a staging server.
- **PM** - reviews feature on staging and requests changes.
- **Bob** - makes changes
- **PM** - re-checks changes and approves. 

Notice how the iteration cycle is only between Bob and the PM. 

After the PMs approval, a pull request code review can be requested by Bob.

The reviewer does not have worry about whether the code is functionally complete. They just need to review code and make sustainability suggestions.

The iteration overhead is significantly reduced for the reviewer, especially if Bob also [writes good pull request descriptions](/making-good-pull-requests/).


