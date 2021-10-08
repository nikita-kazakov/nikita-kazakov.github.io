---
title: How to pass Ruby (Rails) Variables to Javascript
date: 2021-10-08
layout: post
permalink: /pass-ruby-variables-to-javascript
tags:
    - ruby
---

I had to pass Ruby variables to Javascript in my Ruby on Rails applications on two occasions:

- Send user data to tracking snippets (sends through javascript).
- Integrate payment tokens that use Javascript rather than a ruby gem.

Since Ruby is on the backend and Javascript is on the front end, their integration isn't seamless.
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
  // Javascript will return it as:
  email = bob@mail.com
  // bob@mail.com is not a string. It's a series of characters javascript thinks are a variable or method name.
  // This will result in an error.
```

I find it more reliable to put double quotes around it: `"#{}"`.
```haml
:javascript
  email = "#{@user.email}"
  // Javascript will return it as:
  email = "bob@mail.com"
  // This is valid javascript.
```

The interpolated result will always be a string.

If you're passing in a number, you don't need to use quotes around `#{}`.

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

There are a few ways to escape HTML. You can use `raw`.
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

You want to output the ActiveRecord collection as JSON with `to_json` and escape the results with `raw` or `html_safe`. 
The result will be a JSON (an array with several elements) passed to Javascript.  
You can then iterate on that JSON with a `forEach` or `map` within Javascript.

# Fetching data attributes on HTML tags

You can also pass ruby variables through data attributes on an HTML tag. Let's do that using HAML.

```haml
%div#items{ data: { email: @user.email } }

// This generates this html:
// <div data-email="apm@designpickle.com" id="items"></div>
```

Fetch information with Javascript:
```javascript
document.getElementById('items').getAttribute('data-email')
```

Feel free to pass in ActiveRecord through data attributes like this:

```haml
%div#items{ data: { email: @user.email, orders: @orders.to_json } }
```
