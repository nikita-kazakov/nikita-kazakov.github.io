---
title: Writing good git commit messages
date: 2021-10-06
layout: post
permalink: /good-commit-messages
tags:
    - software dev
---

I've written crappy commit messages in the past and I've picked up a few tricks over time that help me write helpful descriptions.

A good commit message should be helpful to the next developer that looks at your code.

# Anti-patterns
Let's look at some poor commit messages
```
git log -3
4dc1e4654 fix css
a1a378d24 spelling fix
3fb78d433 css change
```

These descriptions are vague. Changed css in _what?_ Mention what feature or part of the codebase you changed the css in.

```
git log -1
e7792a29 Launched Hubspot API integration 
```
Let's say the above Hubspot API integration commit had 45 changed files. A year from now, you left the company and your integration needs to be changed. Another developer looks at this commit and three questions come up.

- Was there a ticket / user story opened for this feature?
- What is the pull request for this feature?
- Are there docs?

Let's make it easier it for them.

# A descriptive commit message

When I merge my pull request into the master branch, I squash the pull request commits into one commit because intermediate commits
likely have breaking tests and the developers don't need to see granular details from my work.

That squashed single commit looks something like this:

```
Ticket-108 Launched Hubspot API Integration

https://github.com/my_company/dpp/pull/1369
https://jira.com/link-to-jira-ticket
https://companywiki.com/link-to-wiki-article-on-integration
```

The first line is a quick one line description of what was done. Notice the ticket number in front of the description. Add an empty line.

The next few lines are going to be links. I add a GitHub pull request link, a link to the ticket from Jira / Asana / whatever ticketing tool your company uses. The final url is to the documentation I created for this integration.

The next poor guy that has to revise my code will have documentation and breadcrumbs to follow to understand how the code was integrated into the codebase.
