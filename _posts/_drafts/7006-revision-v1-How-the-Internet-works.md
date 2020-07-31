---
id: 7015
title: How the Internet works
date: 2020-02-25T02:00:57+00:00
author: Nikita Kazakov
layout: revision
guid: https://nikitakazakov.com/7006-revision-v1/
permalink: /7006-revision-v1/
---
The internet is made up of millions of interconnected computers that send and receive messages. That&#8217;s it. 

They call it the world wide **web** because computers can send and receive messages through other computers as a chain. <figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/02/computer_networks-1-1024x769.png" alt="" class="wp-image-7008" srcset="https://nikitakazakov.com/wp-content/uploads/2020/02/computer_networks-1-1024x769.png 1024w, https://nikitakazakov.com/wp-content/uploads/2020/02/computer_networks-1-300x225.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/02/computer_networks-1-768x577.png 768w, https://nikitakazakov.com/wp-content/uploads/2020/02/computer_networks-1.png 1404w" sizes="(max-width: 1024px) 100vw, 1024px" /> <figcaption>Connected computers in the world wide web.</figcaption></figure> 

Each computer has two ways to identify it. An **IP Address** and a **Port.**

An IP Address is like a phone number and a port is the extension you dial once you connect to the phone number.

Let&#8217;s say you want to reach the billing department of your car insurance company. You call the car insurance company and then route to the billing department extension.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">192.168.0.1 # IP Address
80 # Port Number

192.168.0.1:80 #short hand to access the IP address with the specific port number.</pre>

By default, the internet runs on port 80.

When you type in `google.com` in your browser to search for something, your computer is really accessing another computer with an IP address and a port number.

But how is it that you can type in `google.com` or `disney.com` without having to know the IP address or port number of the computer you&#8217;re accessing?

## DNS (Domain Naming System)

When typing in `google.com` in your browser, the URL (name) is mapped to an IP address in the background using DNS (Domain Naming System). DNS is a huge database that keeps track of URL names and their IP addresses. Just like a phone book maps names to phone numbers.

There&#8217;s a huge world-wide database of DNS servers. It&#8217;s not all on one machine. When typing in `google.com`, you&#8217;re sending a **request** message to the closest DNS server to you. If that server doesn&#8217;t know the what IP address `google.com` maps to, it sends a request to another server up the hierarchy chain.

## Internet Interaction

When accessing websites, you are using a browser like Firefox, Chrome, or Internet Explorer. That browser is **the client**. When you type in a URL (`google.com`), you send a **request** to a computer and that computer sends you a **response**.