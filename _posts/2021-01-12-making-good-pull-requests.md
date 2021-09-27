---
title: How to make good pull requests
date: 2021-01-12
layout: post
permalink: /making-good-pull-requests/
tags: 
    - software dev
---

Bottom Line - Don’t waste the reviewer’s time. Don’t make them over-think about things you should have provided ahead of time in the pull request description.

Let’s talk about anti-patterns first before noting down what a good pull request looks like.

## How to make a bad pull request

-   No description
-   Non-descriptive commit messages
-   No screenshots (if applicable)
-   Stale branch that is weeks or months old
-   A ton of changes files without obvious explanation as to the entire structure of the pull request.
-   No link to the feature ticket
-   Merge conflicts

Put yourself in the shoes of your pull request reviewer. The reviewer is likely working on their own code or is reviewing other pull requests not related to yours. The reviewer is likely not familiar with what you wrote. Even if they are slightly familiar, you’re making them think too hard about what was done in this pull request.

By the time the reviewer figures out the point of the pull request, it’s too late. They are now annoyed.

Don’t waste the reviewer’s time.

## How to make a good pull request

Don’t make the reviewer think about menial stuff. Reviewing is already a hard cognitive task.

When you go to a restaurant, before you get your soup, you have the spoon and the napkin right beside you. Imagine if you got the soup but when you asked for the spoon, the server would say “Hey, you figure out how to eat this”.

DO NOT leave the description field blank. A paragraph followed by bullet points of what was done quickly shows exactly what this pull request contains. Add links next to those bullet points that take the reviewer to the feature ticket (Asana, Jira, Trello, etc..)

Add a few screenshots (if applicable) showing exactly what the change was / looks like. No reviewer ever said “These screenshots are annoying and I wish there weren’t any”.

Make sure you regularly merge / rebase code from the master branch into your pull request. Do not let your pull request branch go too stale.

{% include image_center_caption.html 
    caption = "A pull request description with succinct bullet points, links to tickets, and a video link."
    image = "/assets/images/2021/pull_request_description_image.png"
    alt = "A pull request description with succinct bullet points, links to tickets, and a video link."
%}

## Create a demo video

You have a laptop with a built in microphone. Show a demo of what you built / fixed. Record a video and attach it to the pull request.

Go to your pull request bullet points and go through each bullet point and **SHOW** a demo of it in your actual application.

Use your voice. It’s okay to speak and it’s immensely helpful for the viewer that’s watching what you’re doing.

Pretend that the reviewer is sitting right next to you and you’re showing them what you did. It’s okay to be informal.

Keep the video short. Aim for a minute or two. If there are pauses in the video, pause your video recorder while you wait before resuming the recording. Don’t waste the viewers time.

If the code is not straightforward, put the code on your screen and explain it while you’re going through it.

Here’s a real life example of how I do these pull request demo videos. Note that the video is paused several times.

{% include embed_youtube.html id="luHaXbibS0o" %}

There are several recording options out there. In 2021 --- I’m using [Loom](https://www.loom.com/) as they automatically host the video you record. I have also used [screencast-o-matic](https://screencast-o-matic.com).
