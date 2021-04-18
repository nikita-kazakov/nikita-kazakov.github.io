---
title: Exploring Javascript Types
date: 2020-10-11
layout: post
permalink: /javascript-types/
tags: javascript
---

Bottom Line — 

Javascript has five data types known as primitives:
- String
- Number
- Boolean 
- Undefined 
- Null

ES6 added two more:
- Symbol
- BigInt

# STRINGS

You can write strings with a single or double quote:

```javascript
'good string'   // single quote
"good string"   // double quote
```

I prefer using double quotes because you can uyse single quotes within them without needing to escape quotes.
```javascript
"He said 'whatever!' to me."
```

## Concatenating Strings
You can concatenate (add) strings together.
````javascript
catName = "Toly"
catAge = 10

"John has a cat named " + catName + "and he is " + catAge + "."     //=> John has a cat named Toly and he is 10.
'desk' + 'top'  // desktop
````

Keep your types separate to maintain sanity.
```javascript
'2' + '3'       //=> '23'. Why? Because '2' and '3' are STRINGS. The output is a string '23'.
2 + 3           //=> 5. Because both are numbers.
```


Check what each type is by using `typeof`.

# Checking Types
Use typeof Operator to see what the type is.

```javascript
typeof 23         // number
typeof '2'        // string
typeof 'bob'      // string
typeof true       // boolean
typeof undefined  // undefined
typeof null       // object (Weird JS. It's this way because this was a type in the first version of JS. JS is backwards compatible and therefore this error still exists.)
typeof [5, 6]     // object
```

## String Interpolation
Javascript has a powerful feature called string interpolation. Use backticks to activate string interpolation. Javascript will evaluate expressions within `${}` and the output will be a string.
````javascript
catName = "Toly"
catAge = 10
`John has a cat named ${catName} and he is ${catAge}.` //=> John has a cat named Toly and he is 10.
````

# Coersion
Moral of the story --- Don't fully count on coersion. Instead, ensure you have a NUMBER type before performing a mathematical operation.

```javascript
'1' + 4                   //=> '14'. It tries to coerce the number 4 into a string. Success. Now it can concatenate two strings. This is IMPLICIT coercion.
'4' - 3                   //=> 1. It coerces '4' into a number. 4 - 3 = 1. Implicit coercion.
Number('4') - 3           //=> 1. Convert a string into a number first. This is EXPLICIT coersion and doesn't require guesswork.
parseInt('4') - 3         //=> 1. Specifically converts string into an integer.
parseInt('3.1415')        //=> 3. parseInt STOPS converting once it reaches an invalid character. period is an invalid character here.
parseInt('34asdf')        //=> 34. letters are invalid.
String(20)                //=> '20'. Coerces number into a string.
```

# Booleans

Setting TRUE or FALSE.

```javascript
let admin = true
let active = false
```

Booleans are used in comparison operators === or > or <. The returned result will either be true or false.


# Undefined

Undefined is the absence of a return.

```javascript
console.log('technically undefined')    // returns undefined because it writes to the console but doesn't return anything.
var person                              //=> undefined because nothing is assigned.
let person                              //=> undefined.
const BLAH                              //=> undefined.
let person = 3                          //=> undefined. Why? Because you're simply assigning a value but not returning anything.

```

Look at this function:

````javascript
function speak() {
          // Will return undefined because you're simply writing a function and not calling it.
}

speak()   //=> Undefined. The function didn't have anything to return even though you called it.      

````

function speak() {
    return 5 // Will STILL return undefined because you're simply writing a function. However, we have a return line now.
}

speak() // 5. The function returns 5.


// =====
// NULL
// =====

// Null represents emptiness or nothing. Like nil in Ruby.
let age = null

# Numbers

Below are examples of numbers in JavaScript. Don't use commas or periods when writing out numbers.
`1, 5, 5.5, -2, 7.66, 299381`

// =====
// Operations
// =====

// Addition, Subtraction, Multiplication
3 + 5       // 8
6 - 2       // 4
7 * 2       // 14
20 / 5      // 4
20 / 6      // 3.33333 (float)
20 / 3.5    // 5.714 (float)

// Remainder. This is not a mathematical modulo.
20 % 5 // 0
20 % 3 // 2. Because you can't get to 20 with a 3. The maximum you can get to is 6x3 = 18. Then you have a remainder of 2 to get to 20.
// Fun fact. The only place I ever had to use modulus was the fizzbuzz challenge (using Ruby).

// NaN - Not a number
0 / 0           // NaN
5 / undefined   // NaN
'hello' / 2     // NaN. Can't coerce into a string.
5 / null        // Infinity. WTF javascript.
NaN == NaN      // false. WTF javascript.

// Javascript also has Infinity but it is WACKY as hell. Not worth remembering because you'll have a lot of WTF Javascript moments.


// =====
// Equality
// =====

// If you want to know two values are identical, use ===. In most languages, you'd use ==. In Javascript however, since the language
// carries baggage from the past == doesn't mean what you think it means. Use ===.

5 === 5         // true
10 === 4        // false
'bob' === 'bob' // true
'Bob' === 'bob' // false (case sensitive!)




// =====
// Data Structures
// =====

// Arrays - Arrays can contain numbers, strings, or booleans.
let numbers = [1, 2, 3, 4, 5]

// Array elements start with zero. Get first element:
numbers[0]  // 1
numbers[numbers.length - 1] // 5. Get last element of array.

// =====
// Objects
// =====

// Objects in Javascript are like Ruby Hashes. It's a key-value pair.
{ fruit: 'apple' }
{ fruit: 'apple', animal: 'cat' }       // have multiple key-value pairs if needed.

// Searching by key and getting the value.
let objectOne = { fruit: 'apple', animal: 'cat' }
objectOne['fruit']      // apple


// =====
// Expressions
// =====

// Use parenthesis liberally to make your mathematical expressions readable.
2 + (5 + 2)         // 9


// Javascript has statements. This is where you declare something.
let treeColor = 'green'

// Javascript expressions can span over multiple lines. Looks ugly though. Just because you could doesn't mean you should.
number = 3 + 4 +
         5 + 6

