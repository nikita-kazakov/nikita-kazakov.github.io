---
title: The self-documenting code myth
date: 2021-09-26
layout: post
permalink: /self-documenting-code-myth
tags:
    - software dev
---

# The self documenting code myth

Document your code so that the next poor developer that has to extend it or fix it will be thankful you did.

Have you seen code that is less than 2 years old become legacy? That happens when you're left to fix code that another developer wrote but it was left without documentation because it is 'self-documenting'.

Even worse, the developer that wrote it left the company and you have to fix it.

Look --- I get that variable names should be descriptive. I'm also on-board with methods that describe actions. Go ahead --- add integration tests or unit tests in there as well.

It's not enough.

Today's web developer is dealing with APIs and integrating different platforms into a codebase. Without documentation --- those variable names aren't going to tell the next engineer how the pieces fit together with the code you're about to write.

I had to rewrite two business-critical modules this year that were written by developers less than two years ago because no documentation was left. The code was not 'self-documenting'. Both modules integrated with third party applications. I consider this code legacy.

# Code Comments

It's okay to comment your code. If the method cannot be made simpler or more intuitive, please comment on what the method is supposed to do. More importantly, comment on WHY the method is necessary and why another approach didn't work.

Some developers will say that comments get stale and will lie to you.

I've yet to get upset at a developer leaving comments for me to work with. They are almost always useful hints to figure out what they were thinking about as they wrote code.

If change the code and the comment no longer applies then delete it or modify it so that it doesn't become stale. It's the decent thing to do.

# But I have unit tests

Can we agree that writing tests is hard? There's not one standard to follow. BDD, TDD, integration tests and more styles are out there.

What's worse is relying on an overly mocked test suite. The tests are so tightly coupled to how code should work rather than what the code should output that it becomes hard to refactor or extend code.

The developer left a lot of tests for you thinking that test coverage is high but each time you make a small change, you break 5 tests.

The tests have become useless. You'll have to understand the code from scratch and delete most of these tests because they no longer apply. Does that sound a bit familiar and bring on some anxiety?

Tests alone are often not enough to explain how your code integration works.

# Wiki

If your company doesn't have a wiki for engineering, I highly recommend setting one up.

When you write a new feature and it involves 3rd party services,  document the integration.

Let me give you an example. If you're integrating an image service with AWS and you have to set up bucket policies and IAM permissions for the integration, self documenting code is not enough. AWS is a deep rabbit hole and the next poor developer that has to fix your code is going to be lost.

If you're setting up production servers and then you leave the company (which you will), please document how things are set up. Don't assume the next developer knows Dev Ops / Docker / Kubernetes / Deployment like you did.

# Fooled by familiarity

You might think --- but my code is easy to understand! Have you had to go back to code you wrote a year ago in order to extend it and thought 'Who the hell wrote this' only to realize it was you?

That happened to me too!

And we're looking at our own code that should be *very* familiar to us. Imagine how foreign it will look to fresh set of eyes.
