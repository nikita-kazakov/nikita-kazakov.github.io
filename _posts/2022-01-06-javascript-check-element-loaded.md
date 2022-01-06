---
title: Javascript --- wait until an element is loaded
date: 2022-01-06
layout: post
permalink: /js-wait-until-loaded-element
tags:
    - javascript
---

Javascript is asynchronous and a common pain-point is running a script before a DOM element on the page has loaded.

One way to handle this is by adding a listener to the document which listens for the `DOMEContentLoaded` event.

```javascript
document.addEventListener("DOMContentLoaded", function(){
  // Code here waits to run until the DOM is loaded.
});
```

In complicated scenarios --- when several elements on the page are loading data via AJAX --- the above script doesn't work.

I use the snippet below to check when a specific DOM element is present on the page and then run code. I took it from [Volomike at Stack Overflow](https://stackoverflow.com/a/53269990).

```javascript
    const isElementLoaded = async selector => {
      while ( document.querySelector(selector) === null) {
        await new Promise( resolve =>  requestAnimationFrame(resolve) )
      }
      return document.querySelector(selector);
    };

    // I'm checking for a specific class .file-item and then running code. You can also check for an id or an element.
    isElementLoaded('.file-item').then((selector) => {
        // Run code here.
    });
```

This code is clever as it loops looking for a specific selector and returns a promise.