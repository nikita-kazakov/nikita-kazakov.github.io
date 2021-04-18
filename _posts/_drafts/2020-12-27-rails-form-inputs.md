---
title: Checkboxes and other form inputs in Ruby on Rails
date: 2020-12-27
layout: post
permalink: /form-inputs-ruby-on-rails/
tags: 
    - ruby on rails
---

We looked at how [Ruby on Rails forms worked](/forms-in-ruby-on-rails). Let's look at the different input helpers we can use to create and edit forms.

```bash
rails g resource project name:string description:string user:references
rails g resource task name:string project:references
```

# Button

Most forms have a submit / update buttons. 

```haml
= form_for User.new do |user|
  = user.button
  = user.submit # Another alternative for creating a submit button.
```

Rails form checks whether the resource passed in (user in the example above) is a new resource or an existing one. Rails will automatically change the button label based on that.

If the resource is new (User.new), the label will say "Create [resource]"
If the resource exists, the label will say "Update [resource]"

You can also pass a block to the button helper to change whatever you want about the button. Let's say you want to add custom text to it:

```haml
= user.button do
  %span Custom Text
  -# You could also add complex text logic in here if you wanted to.
end
```

# Checkbox (complicated - come back to this)

Checkboxes should be used when one or more options can be selected from a list.

This helper shows checkboxes. It will return an integer. If the integer is zero, Rails will assume the checkbox was unchecked. If it is better than zero, then Rails will consider it checked.

# Color Field

Let's say you want a user to pick a shirt color they'd like to use in a form. You can use the color input field.

```haml
= form_for User.new do |user|
  = user.color_field(:shirt_color)
  = user.submit
```

You'll see the following parameters with the color hex value:
```bash
"user"=>{"age"=>"0", "shirt_color"=>"#00f900"}
```

Don't forget that you can customize color pickers by using a [3rd party javascript color picker](https://jscolor.com) and integrating it with this Rails `color_field` helper.

# Date Field

This creates an HTML date input field.

```haml
= form_for @user do |user|
  = user.date_field(:created_at)
  = user.submit
```

By default, the date input field will show today's date if it is empty. There are passable options in the example below.

```haml
= form_for @user do |user|
  -# Default date_field:
  = user.date_field(:created_at)
  -# With a default date value:
  = user.date_field(:created_at, value: "2003-11-02")
  -# Let's say you don't want the users picking any dates before today:
  = user.date_field(:created_at, min: Time.zone.now)
  -# Let's say you only want them to select between today and three days from now.
  = user.date_field(:created_at, min: Time.zone.now, max: Time.zone.now + 3.days)
  = user.submit
```
Check out [Mozilla's MDN Docs for information on the date input HTML element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date).

Even though you can specify the min and max date values, you cannot easily block out specific dates without adding custom javascript. If you're going to go down that route, you might as well use a javascript datepicker library.

# DateTime Field

Different browsers poorly support date-time fields. If you're going to be using a date-time picker, you're better off with using something like a [lightweight flatpickr javascript library](https://github.com/flatpickr/flatpickr).

# Email Field

It's pretty much a text field. The advantage of the email field for an email input is that browser plugins can recognize it as the correct email field and provide users email auto fill options.

```haml
= form_for @user do |user|
  = user.email_field(:email)
  = user.submit
```

# File Field

```haml
= form_for @user do |user|
  = user.file_field(:name) # Single File Upload
  = user.file_field(:name, multiple: true) # Multiple File Upload
  = user.submit
```

This allows the user to upload a single or multiple files. Browsers display this field differently. These fields are not easy to style.

# Hidden Field

This is a powerful field that gets used often to pass data that clients shouldn't be selecting. For example, you might want to pass a payment token with a form without displaying it to the client.

```haml
= form_for @user do |user|
  = user.text_field(:name)
  = user.hidden_field(:stripe_token)
  = user.submit     
```

# Number Field

The `number_field` is the same as `text_field` except it's used for numbers and has a spinner associated with it.

You can pass a `min`, `max`, `step` values to it.

# Password Field

You will collect users' password using the `password_field`. On re-rendering the page, this field renders empty for security purposes.

# Radio Button

When you have several options but can only select one.

# Text Area

When you need to enter text that is more than a string. Note that you can pass in the size of the text area.
```haml
= form_for @user do |user|
  = user.text_area(:name, size: "50x10")
  = user.submit
```


