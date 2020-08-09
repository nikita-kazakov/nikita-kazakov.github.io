---
id: 236
title: Using Jade (Pug) to preprocess HTML
date: 2015-10-19T00:00:00+00:00
layout: post
permalink: /using-jade-pug-to-preprocess-html/
tags:
  - tech
---

Bottom Line: Pug makes HTML tags look a lot less messy.

**2020 Update**: I don't use Pug templating anymore. I do use [HAML](https://haml.info) with Ruby and Ruby on Rails and it is very similar.
{: .notice--info}

HTML looks like soup as you create complex layouts. You have to use opening `<tag>` and closing `</tag>`. They are everywhere and you can’t forget to close one. 

Okay, I know that if you’re using a text editor like <a href="http://www.sublimetext.com" target="_blank" rel="noopener noreferrer">sublime text</a>, it sort of takes care of these problems with plugins. Jade Templating language, now known as Pug, transpiles into HTML and fixes this issue.

<a href="http://www.learnjade.com" target="_blank" rel="noopener noreferrer"><em>Jade</em></a> _is an HTML templating language_. Actually, it is not only for HTML because it also provides an extension to writing javascript. Let me show you HTML vs Jade. One word of warning: If you intend to use PHP, don’t use Jade. It is javascript friendly, and unfortunately doesn’t play well with <% php> tags.

# HTML — Example 1
```html
<body>
    <h1>This is a header</h1>
    <div class="container">
        <h1>Headline 1</h1>
        <p>Yes, this is pretty cool</p>
    </div>
    <div class="container">
        <h1>Headline 2</h1>
        <p>Life is good.</p>
    </div>
</body>
```

# Jade — Example 1

```haml
body 
  h1 This is a header 
  .container 
    h1 Headline 1 
    p Yes, this is pretty cool. 
  .container 
    h1 Headline 2 
    p Life is good.
```

Compare the examples above. Instead of closing tags, Jade relies on indentations. Indentations seem much more intuitive to the eye in seeing parent-child relationships between elements.

Go ahead, go to <a href="http://html2jade.org" target="_blank" rel="noopener noreferrer">HTML2Jade</a> and play with the two formats yourself.

The other advantage of using _Jade is that it supports partials_. This means that if you’re making a static website, you can re-use the same code in your pages. Where is this useful? How about the navigation menu. You’ll likely have the same navigation menu for all your pages, so when you add a new link to it, you don’t have to update all your pages. The partial feature part of Jade will update them for you and _keep your code DRY (Do not Repeat Yourself)._

I’ve noticed a difference in _comprehending the page_ when using Jade in my code. I open the document, and I can quickly understand what is going on.

Since Jade is a templating language, that means that it must be preprocessed before you get an output HTML file. I really like using <a href="https://prepros.io" target="_blank" rel="noopener noreferrer">Prepros</a> to automatically process any Jade files in my selected watch folder. The other great thing about PrePros is that it automatically refreshes the browser for me when it detects changes to the document. If you’re on a Mac, you can use <a href="https://incident57.com/codekit/" target="_blank" rel="noopener noreferrer">CodeKit</a>.