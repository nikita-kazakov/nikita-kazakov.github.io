---
title: How HTTP Request and Response Works
date: 2020-08-08
layout: post
permalink: /how-http-request-response/
---

We previously looked at how [HTTP works](/how-http-works/). Let's look at how communication through HTTP happens through requests and responses.

# Request
When you type an address into the browser, you're making a request. For example, you type in:

```
https://www.bestbuy.com
```

As previously mentioned, `bestbuy.com` is converted to a machine IP address and a port number (80) is added automatically.

You're querying the `bestbuy.com` machine and saying "Hey, can I **GET** information from you?".

You're sending what is known as a GET request. GET is a verb. There are more of these verbs that HTTP protocol understands and uses under the hood.



