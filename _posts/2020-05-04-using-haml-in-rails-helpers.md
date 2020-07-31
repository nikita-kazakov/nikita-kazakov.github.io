---
id: 7052
title: Using HAML in Rails Helpers
date: 2020-05-04T23:49:33+00:00
author: Nikita Kazakov
layout: post
guid: https://nikitakazakov.com/?p=7052
permalink: /using-haml-in-rails-helpers/
site-sidebar-layout:
  - default
site-content-layout:
  - default
theme-transparent-header-meta:
  - default
categories:
  - Uncategorized
tags:
  - ruby
---
Using HAML in Rails views is great because its more succinct than ERB.

Using HAML in Rails helpers was a source of confusion on my end. Here&#8217;s what I learned about using HAML in helpers.

I wish that I could use HAML directly in Rails helpers just like I use them in Rails views:

```ruby
# application_helper.rb
# ERROR!
  def request_link
    %div
      link_to "Make a Request", root_path
  end
```

However, you&#8217;ll get an error. This is incorrect syntax.

You&#8217;ll have to use `haml_tag` instead as Ruby can parse that in helper.

```ruby
  # application_helper.rb
  def request_link
    haml_tag :li do
      link_to "Make a Request", root_path
    end
  end
```

```haml
-# nav.html.haml
- request_link
```
I tried to create a link using `haml_tag` to generate an html list item and a link within it, and nothing showed up.

You&#8217;re probably thinking the issue is because I wrote `- request_link` instead of `= request_link` to render content, but that wasn&#8217;t the case. 

Finally, I found that instead of using `haml_tags`, I can use Rails `content_tag` instead as shown below:
```ruby
# application_helper.rb
def request_link
  content_tag :li do
    link_to "Make a Request", root_path
  end
end
```
```haml
-# nav.html.haml
= request_link
```

The helper properly renders in my view. Another benefit of using `content_tag` is that I can use the normal HAML rendering equal sign in my views `= request_link`.

## Content tag is flexible

Let's complicate it up a bit.

```ruby
# application_helper.rb
def request_link(classes = "")
    content_tag :div, class: "bg-warning" do
      content_tag :li, class: classes do
        link_to "Make a Request", root_path
      end
    end
end
```

```haml
-# nav.html.haml
= request_link("active hidden-md")
```

I&#8217;m passing an empty class string to `request_link` helper. I&#8217;m also nesting `li` within a `div`.

In my view I&#8217;m passing in two classes to the `request link` helper.

Feel free to pass unobtrusive javascript in as a `data` parameter. That works too!

```ruby
def request_link(classes = "")
    content_tag :div, class: "bg-warning" do
      content_tag :li, class: classes do
        link_to "Make a Request", root_path, data: {toggle: "tooltip", title: "Hover over me!"}
      end
    end
end
```