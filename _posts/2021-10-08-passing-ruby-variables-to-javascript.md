---
title: How to pass Ruby (Rails) Variables to Javascript
date: 2021-10-08
layout: post
permalink: /pass-ruby-variables-to-javascript
tags:
    - ruby
---

I often pass Ruby variables to Javascript in Ruby on Rails on two occasions:

- Send user data to tracking snippets (through javascript).
- Integrate payment tokens that use Javascript rather than a ruby gem.

Since Ruby is on the backend and Javascript is on the frontend, their integration isn't seamless.
I'm going to use HAML in the examples below rather than ERB.

You can add in-line javascript in your view templates and interpolate ruby variables. 
HAML supports ruby interpolation under the `:javascript` tag with the `#{}` syntax.

```haml
%h1 Some Headline  
%p This is a paragraph  
  
:javascript
  email = "#{@user.email}"
  alert(email)
```

Using  `#{}` by itself can result in errors. For example, let's say I interpolate:

```haml
:javascript
  email = #{@user.email}
  // Javascript will see it as:
  email = bob@mail.com
  // bob@mail.com is not a string. It's a series of characters Javascript thinks are variables or method names.
  // This results in an error.
```

I find it more reliable to put double quotes around it: `"#{}"`.
```haml
:javascript
  email = "#{@user.email}"
  // Javascript will return it as:
  email = "bob@mail.com"
  // This is valid.
```

The interpolated result will always be a string. If you're passing in a number, you don't need to use quotes around `#{}`.

```haml
:javascript
  quantity = #{@user.age}"
  // No need for quotes as we're passing in a number.
  // quantity = 55
```

# Escaping HTML Characters

If the data I'm passing has quotes, brackets, or some other special character, I have to force Rails to ignore HTML escaping.

```haml
:javascript
  user_email = "#{"This will not 'be escaped' 'properly'"}"
  // The result will be:
  // user_email = "This will not &#39;be escaped&#39; &#39;properly&#39;"
```

There are a few ways to escape HTML. One is to use `raw`.
```haml
:javascript
  user_email = "#{raw "This will not 'be escaped 'properly'."}"
  // It is now escaped properly.
  // user_email = "This will not 'be escaped' 'properly'"
```
Another solution is to use `html_safe`.

```haml
:javascipt
  user_email = "#{"This will not 'be escaped' 'properly'".html_safe}"
```

# Passing Rails ActiveRecord to Javascript

What if you want to pass an ActiveRecord collection to Javascript?

```haml
:javascript
  users = #{@orders.to_json.html_safe}
  // or
  users = #{raw(@orders.to_json)}  
```

You want to send an ActiveRecord collection as JSON with `to_json` and escape the results with either `raw` or `html_safe`. 
The result will be a JSON (an array with several elements) passed to Javascript. 

You can then iterate on that JSON with a `forEach` or `map` within Javascript.

# Fetching data attributes on HTML tags

You can also pass ruby variables through data attributes on HTML tags. Let's do that in HAML.

```haml
#items{ data: { email: @user.email } }

// This generates this html:
// <div data-email="apm@designpickle.com" id="items"></div>
```

Fetching this information with Javascript:
```javascript
document.getElementById('items').getAttribute('data-email')
```

Feel free to pass in ActiveRecord through data attributes like this:

```haml
#items{ data: { email: @user.email, orders: @orders.to_json } }
```

```javascript
// Fetch the JSON in Javascript
document.getElementById('items').getAttribute('data-orders')
```
