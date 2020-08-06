---
title: How HTTP Works
date: 2020-08-04
layout: post
permalink: /how-http-works/
---
The internet is made up of millions of interconnected computers that send and receive messages. That's it. 

They call it the world wide **web** because computers can send and receive messages through other computers as a chain. <figure class="wp-block-image size-large">

{% include image_center_caption.html 
    caption = "Connected computers in the world wide web."
    image = "/assets/images/2020/how-http-works/computer_networks-1.png"
    alt = "Connected computers in the world wide web."
%}

Each computer has two pieces of identity. An **IP Address** and a **Port.**

An IP Address is like a phone number and a port is the extension you dial once you connect to the phone number.

Let&#8217;s say you want to reach the billing department of your car insurance company. You call the car insurance company and then route to the billing department extension.

````
192.168.0.1     # IP Address
80              # Port Number
192.168.0.1:80  # short hand to access the IP address with the specific port number.
````

By default, the internet runs on port 80.

When you type in `google.com` in your browser to search for something, your computer is really accessing another computer with an IP address and a port number.

But how is it that you can type in `google.com` or `disney.com` without having to know the IP address or port number of the computer you're accessing?

# DNS (Domain Naming System)

When typing in `google.com` in your browser, the URL (name) is mapped to an IP address in the background using DNS (Domain Naming System). DNS is a huge database that keeps track of URL names and their IP addresses. Just like a phone book maps names to phone numbers.

There's a huge world-wide database of DNS servers. It's not all on one machine. When typing in `google.com`, you're sending a **request** message to the closest DNS server to you. If that server doesn't know the what IP address `google.com` maps to, it sends a request to another server up the hierarchy chain.

# Internet Interaction

When accessing websites, you are using a browser like Firefox, Chrome, or Internet Explorer. That browser is **the client**. When you type in a URL (`google.com`), you send a **request** to a computer and that computer sends you a **response**.

# HTTP is stateless
HTTP is stateless. HTTP protocol itself doesn't hold on to any data. This means that each http request-response is sent independently. The advantage is that if one message get corrupted, it won't affect the other ones.

If data isn't tracked through HTTP, how does Google or Facebook know who is logged in? That happens through the magic of sessions and cookies. We'll get to that later.

# URL

Let's look at the URL below. If every connection computer requires a port number to connect, how come the URL doesn't have one?

It's because browsers like Edge, Chrome, Firefox automatically add the port number (80) for you so you don't have to type it in each time.

```
|--1--||------2-------||-3-|
 http://www.google.com/maps

1 - Protocol
2 - Host
3 - URL Path
```

# Passing in Query String and Parameters
A powerful feature of URLs is the ability to pass in data.

```
http://www.example.com?search=dinosaur&results=10&sort_by=popularity
```

|component| description|
|---------|------------|
|?        |special character that indicates the start of query| 
|search=dinosaur| passed in a key / value pair |
|&        | special character that separates parameters (when you want to add more parameters to the query string |
|results=10      | Passed in parameter. results is the key and 10 is the value. |
|sort_by=popularity      | Another passed in parameter.|

In the next series, we'll take a look at how [HTTP request / response](/how-http-request-response/) works.