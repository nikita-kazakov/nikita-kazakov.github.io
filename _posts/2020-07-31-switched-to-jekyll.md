---
title: "Why I switched from wordpress to Jekyll (Static Site)"
date: 2020-07-31
permalink: '/wordpress-to-jekyll/'
tags: branding
---

Bottom Line --- My blog is meant for writing. A Jekyll allows me to write with ease and avoid friction I experienced with WordPress.

# Why I switched

I switched because the main purpose of my blog was to have written work. I enjoy writing. A few things in WordPress caused friction in my process.

## Syntax Highlighting

When I switched careers to software development, I wanted to write technical articles. Syntax highlighting plugins do exist for WordPress, but they are a pain to setup and even harder to make them look _just right._

For example, I found a syntax highlighting plugin for Ruby but it didn’t support Rails / HAML syntax. The solution was to use multiple syntax highlighting plugins. No thanks.

## No Database

A static site doesn’t rely on a database. It only needs to load html pages. Compared to a WordPress site, it truly is much faster.

## Hosting

I paid $80 / year for shared hosting when I used WordPress. I won’t complain about the cost as that is not expensive. However, with a static site, I host it for **FREE** on Github pages.

Github pages is much faster than my previous shared hosting provider. I don’t need to use a CDN to make my site faster worldwide.

## WYSIWYG code pollution

It’s taking me hours to convert my WordPress posts to markdown. I didn’t realize how dirty WYSIWYG  (What you see is what you get) text editors are. Sentences are polluted with css tags that shouldn’t be there. I’ll be able to avoid this with Jekyll.

## Writing focused

With Jekyll, I create a markdown text file and I can paste my paragraphs right into it. Done.

## Great Writing Themes

I’m a fan of the [so-simple](https://github.com/mmistakes/so-simple-theme) Jekyll theme. I love how it separates your site by posts, tags, and years. I couldn’t easily do that with WordPress themes. Even better is the instant [search function](http://nikitakazakov.com/search). There are a lot of free [Jekyll themes](https://jekyllthemes.io/free) out there.

## Git Version Control
If you're a software developer, you know how wonderful Git is for version control. I'll never have to worry about files / text disappearing as everything is version controlled.

## I already know Ruby

I develop in Ruby and Ruby on Rails. If I didn't know Ruby, I might have gone with another static site generator like [Hugo](https://gohugo.io) (it's faster). Jekyll is not as easy to setup as WordPress. You need a Ruby environment.

# I’ll miss WordPress

I loved editing in a WYSIWYG editor. I’ll miss directly editing in WordPress’s Gutenberg editor.

I’ll miss using blocks to dynamically add images / youtube videos to a page.

With Jekyll, I have to manually add the image to a folder and use an includes shortcode to show images and videos.

If I was building a business site or an ecommerce site, I wouldn’t use a static site generator. I would use wordpress.

# How I write

I don’t directly write in a markdown file. I don’t like the syntax. I prefer to write my posts in [Dropbox Paper](https://paper.dropbox.com). I then copy and paste the text to [StackEdit](https://stackedit.io/app#) and copy the markdown formatted text to the markdown file. I’ll then push the file up to github and it’s published!