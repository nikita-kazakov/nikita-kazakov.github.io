---
title: Coerce string to boolean in Javascript
date: 2022-01-10
layout: post
permalink: /javascript-coerce-boolean
tags:
    - javascript
---

Often I'll have a boolean value passed in as a string. This means an `if` statement will have to look like this:

```javascript
proceed = 'true'

if (proceed === 'true') { 
    // some code here.
}
```

You're probably thinking, why not coerce it.

```javascript
Boolean('true')  //=> true
Boolean('false') //=> true!??!?!?
```
That won't work as a `false` string is also coerced to `true`.

Instead, do this and make your code prettier and easier to understand.

```javascript
proceedIsTrue = proceed === 'true'

if (proceedIsTrue) { 
    // Code runs if true
}
```