---
title: Javascript Style Guide (Part 1)
date: 2020-10-05
layout: post
permalink: /javascript-styling/
tags: javascript
---

Bottom Line — Follow good style guidelines so that other developers can quickly read your code.

Javascript uses **camelCase** as a standard for naming. Note that you can't start function names or variables names with digits.

```javascript
let bigCat = 1  // GOOD
let big_cat = 1 // BAD
```

Comments are written with `//`.

Use ALL CAPS to represent constants. If you need to use multiple words, add underscores. Don't start or end constants with an underscore.

```javascript
const PI = 3.1415
const FIXED_RATE = 0.125
```

A code block should have the opening brace on the SAME LINE as the function or conditional expression (eg. if statement).
Use a single space between function name and the curly bracket.

```javascript
function hello(){ // BAD. No space.
}

function hello () // BAD. Opening Curl on a different line than function.
{
}

function hello() { // GOOD.
}
```

Use spaces between operators and operands.
```javascript
let apples=4+3      // BAD
let apples = 4 + 3  // GOOD
```

If you're [going to use semicolons](/javascript-semicolons/), terminate each logical line unless the line ends with {, }, or :