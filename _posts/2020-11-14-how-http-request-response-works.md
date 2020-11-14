---
title: How HTTP Request / Response Works
date: 2020-11-13
layout: post
permalink: /how-http-request-response/
tags: 
    - web development
---

To know how the internet works, we looked at how the [HTTP protocol worked](/how-http-works/). Let's take a look at the two parts of HTTP: Request and Response.

When you're clicking on a website link, you're sending a request to a server. The server reads your request, applies some logic, and sends a response. That response is a page you see on your screen.

But what kind of logic does it apply? Let's say you're registering a new profile on a site. When you submit the form, the server will take your request, with parameters including your name, email, password and add it to the database and send a response back to your screen in the form of a members page.

Another example is when logging into a site. You submit a form with a username and password (request), and the server checks if it's valid (logic), and responds with access or an alert that the credentials are incorrect.

# HTTP Verbs

The HTTP protocol has specific ways of sending and receiving data. When you hear the term REST or RESTful services, this is a reference to 5 verbs.

| Verb | Description|
|------|------------|
| get  | When you click on a link to load a page, you're 'getting' a page. Get is used to only read data. |
| patch  | Used when modifying something in the database. For example, a put request is sent to modify your email in the database |
| put  | An older way to 'patch'. I'm sure there's a niche place for it but as a developer, I haven't used this verb in my workflows. |
| post | Used to create a new resource. For example, when you add a new article to wikipedia, you send a POST request. |
| delete | It's used to delete a specific resource. |

When I'm building a RESTFUL application --- I only use four verbs: get, patch, post, delete. 

These four verbs make up **CRUD**. CRUD stands for create, read, update, delete. 

- Create is done with post.
- Read is done with get.
- Update is done with patch.
- Delete is done with delete.

## CRUD in an example

Let's put these verbs into context. Let's say you want to write an article on Wikipedia. You type in the address in your browser
and your browser sends a **get** request and the browser displays the Wikipedia website.

You fill out a form with the article title and description and click submit. You send a **post** request to create the article in a database.

When you want to edit the article, you make your edits in a form and send a **put** request. The server updates the article with your edits.

If you hate your article and want to delete it, you'll click a delete button and send a **delete** request. The server will delete it from the database.

# How a get request works

Chrome and Firefox provide an easy way to see website traffic using Inspector. Press F12 on your browser to display it.
Let's browse to https://www.wikipedia.org.

Select the `network` tab and refresh the page.

{% include image_center_caption.html 
    caption = "Wikipedia get request in Firefox's browser Inspector."
    image = "/assets/images/2020/how-http-request-response/wikipedia-get-request.jpg"
    alt = "Wikipedia get request in Firefox's browser Inspector."
%}

You'll see that there is a list of get requests. We have a list because as we load the wikipedia page (highlighted in red), the html requests specific images and css files to load as well. Those are requested automatically and you see them in the list.

The headers tab on the right contains header information with a code `200` (OK).

Click on the response tab. You'll see that the server sent HTML to your browser which it then parsed and displayed with images and css. Now you know how a website magically shows up on the screen.



