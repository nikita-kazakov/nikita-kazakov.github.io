---
id: 7089
title: Using Ajax in Rails Forms
date: 2020-05-17T22:21:21+00:00
author: Nikita Kazakov
layout: post
guid: https://nikitakazakov.com/?p=7089
permalink: /using-ajax-in-rails-forms/
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
Sometimes you want to update a form and not refresh the page. This is where AJAX (Asynchronous Javascript) comes handy.

Instead of the controller responding with an html page, we&#8217;ll have the controller respond with Javascript and update the page.

Let&#8217;s create a list of restaurants by creating a Rails model with restaurant name and category.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">rails g model restaurant name:string category:string</pre>

I&#8217;m going to add a few restaurants to the database by going into the console.

```ruby
rails c
Restaurant.create(name:"Burger King", category:"Fast Food")
Restaurant.create(name:"Cheese Cake Factory", category:"Family")
```

```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```

Let's generate a rails controller.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">rails g controller restaurants</pre>

We&#8217;ll generate the standard routes for our restaurant resource in `routes.rb`

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">Rails.application.routes.draw do
  resources :restaurants
end
</pre>

I&#8217;m going to be using [HAML gem](https://github.com/haml/haml-rails) instead of ERB to build out the html. If you need to see what&#8217;s going on in erb, feel free to use the [haml to erb converter](https://haml2erb.org/).

Let&#8217;s add the index action to the restaurants controller and load all of the restaurants into the `@restaurants` instance variable. `@restaurants` is now available for use in our views.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">class RestaurantsController &lt; ApplicationController
  def index
    @restaurants = Restaurant.all
  end
end</pre>

I&#8217;ll create an index view `views/restaurants/index.html.haml`. I&#8217;ll add a simple table. Notice that I&#8217;m using [Bootstrap 4 for styling](https://github.com/twbs/bootstrap-rubygem) but it&#8217;s completely optional.

```haml
%table.table.table-hover
  %thead
    %tr
      %th Name
      %th Category
  %tbody
    %tr
      %td</pre><figure class="wp-block-image size-large">
```
 
![center-aligned-image](https://nikitakazakov.com/wp-content/uploads/2020/05/image-1-1024x213.png){: .align-center}
<img src="https://nikitakazakov.com/wp-content/uploads/2020/05/image-1-1024x213.png" alt="" class="wp-image-7098" srcset="https://nikitakazakov.com/wp-content/uploads/2020/05/image-1-1024x213.png 1024w, https://nikitakazakov.com/wp-content/uploads/2020/05/image-1-300x62.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/05/image-1-768x160.png 768w, https://nikitakazakov.com/wp-content/uploads/2020/05/image-1.png 1398w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

We have a table but there&#8217;s nothing in it. Let&#8217;s add the list of restaurants.

```haml
%table.table.table-hover
  %thead
    %tr
      %th Name
      %th Category
  %tbody
    - @restaurants.each do |restaurant|
      %tr
        %td
          = restaurant.name
        %td
          = restaurant.category
```

<img src="https://nikitakazakov.com/wp-content/uploads/2020/05/image-2-1024x278.png" alt="" class="wp-image-7101" srcset="https://nikitakazakov.com/wp-content/uploads/2020/05/image-2-1024x278.png 1024w, https://nikitakazakov.com/wp-content/uploads/2020/05/image-2-300x82.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/05/image-2-768x209.png 768w, https://nikitakazakov.com/wp-content/uploads/2020/05/image-2.png 1174w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

Let&#8217;s add a link to the index page to add a new restaurant.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">= link_to "Add Restaurant", new_restaurant_path, class:"btn btn-primary", remote: true</pre><figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/05/image-3-1024x317.png" alt="" class="wp-image-7103" srcset="https://nikitakazakov.com/wp-content/uploads/2020/05/image-3-1024x317.png 1024w, https://nikitakazakov.com/wp-content/uploads/2020/05/image-3-300x93.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/05/image-3-768x238.png 768w, https://nikitakazakov.com/wp-content/uploads/2020/05/image-3.png 1290w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

Notice that I added `remote: true` to the `link_to` helper. Statement tells Rails we&#8217;re going to be responding with javascript and there&#8217;s no reason to redirect to another page when the button is clicked.

Go ahead, try to click the button. Nothing will happen.

## Ajax and responding with JS

Let&#8217;s create a `new` action in the controller and load a new restaurant instance into the `@restaurant` instance variable. We&#8217;re going to use this in our form.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">class RestaurantsController &lt; ApplicationController
  def index
    @restaurants = Restaurant.all
  end

  def new
    @restaurant = Restaurant.new
  end
end</pre>

Instead of clicking on the `Add Restaurant` button and going to a new page, we want the form to be rendered on the same page. This means that the `new` action should NOT respond to html. It should instead respond to `js`.

I&#8217;m using the [responders gem](https://github.com/heartcombo/responders) to define how an action in the controller should respond. One line 2 I state that the `new` action should respond to js instead of html.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">class RestaurantsController &lt; ApplicationController
  respond_to :js, only: [:new]

  def index
    @restaurants = Restaurant.all
  end

  def new
    @restaurant = Restaurant.new
  end</pre>

Let&#8217;s return back to the add restaurant button. When you click it, watch your server console. You&#8217;ll see that Rails is trying to process the `new` action as JS but it can&#8217;t find a template to use.<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/05/image-4-1024x161.png" alt="" class="wp-image-7106" srcset="https://nikitakazakov.com/wp-content/uploads/2020/05/image-4-1024x161.png 1024w, https://nikitakazakov.com/wp-content/uploads/2020/05/image-4-300x47.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/05/image-4-768x120.png 768w, https://nikitakazakov.com/wp-content/uploads/2020/05/image-4-1536x241.png 1536w, https://nikitakazakov.com/wp-content/uploads/2020/05/image-4.png 1684w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

We solve this by creating `new.js.erb` under `views/restaurants`.

Refresh your page and click the add restaurants button again. The `new.js.erb` file renders but it&#8217;s empty.<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/05/image-5-1024x175.png" alt="" class="wp-image-7107" srcset="https://nikitakazakov.com/wp-content/uploads/2020/05/image-5-1024x175.png 1024w, https://nikitakazakov.com/wp-content/uploads/2020/05/image-5-300x51.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/05/image-5-768x131.png 768w, https://nikitakazakov.com/wp-content/uploads/2020/05/image-5.png 1508w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

Notice that this file is first processed by erb (ruby) and then by JavaScript. It&#8217;s a JavaScript file. I know that I&#8217;m using HAML but why would I want to process this with erb and then js? Because Ruby Mine won&#8217;t do syntax highlighting if I process it as `new.js.haml`. That&#8217;s the only reason.

We want this file to display a form for us to add new restaurants.

Let&#8217;s add a form to our index page that we&#8217;ll use to add a new restaurant. I&#8217;ll use `form_with` and call on a new instance of a Restaurant. I added the form right above the `link_to` helper. Take note that I added an id `new-restaurant-form` so that I had a way of selecting the form somehow with java script.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">%h1 Restaurants
%table.table.table-hover
  %thead
    %tr
      %th Name
      %th Category
  %tbody
    - @restaurants.each do |restaurant|
      %tr
        %td
          = restaurant.name
        %td
          = restaurant.category

%div#new-restaurant-form.my-3
  =form_with model: Restaurant.new do |form|
    = form.text_field :name, placeholder: 'Name'
    = form.text_field :category, placeholder: 'Category'
    = form.submit

= link_to "Add Restaurant", new_restaurant_path, class:"btn btn-primary", remote: true</pre>

Let&#8217;s create `create` action that will get triggered once the &#8220;create restaurant&#8221; button is clicked. Let&#8217;s also create strong parameters as a private method which helps us create the new restaurant object. In `restaurants_controller.rb`, add:

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">def create
    @restaurant = Restaurant.new(restaurant_params)
    @restaurant.save
  end

  private

  def restaurant_params
    params.require(:restaurant).permit(:name, :category)
  end</pre>

Note that in the `create` action, we&#8217;re grabbing the passed in params from the form we submitted and we&#8217;re filling out a new instance of `@restaurant`. We&#8217;re then saving the restaurant object to the database.

Go to the restaurants page and enter a restaurant and click the &#8220;create restaurant&#8221; button. Nothing happens. Refresh the page manually and you&#8217;ll see your entry in the list.

This is not quite what we want. Let&#8217;s add some magic using Javascript (Jquery in this case).<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/05/image-6-1024x452.png" alt="" class="wp-image-7112" srcset="https://nikitakazakov.com/wp-content/uploads/2020/05/image-6-1024x452.png 1024w, https://nikitakazakov.com/wp-content/uploads/2020/05/image-6-300x133.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/05/image-6-768x339.png 768w, https://nikitakazakov.com/wp-content/uploads/2020/05/image-6.png 1143w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

First I want the form to appear when we click the add restaurant button. By default, I&#8217;m going to apply an HTML class `d-none`(display: none) to hide the form by default. When the page is refreshed, the form is not visible.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">%div#new-restaurant-form.my-3.d-none</pre>

When we render `new.js.erb`, I want to show the form. I can do that using Jquery. Inside of `new.js.erb` add:

<pre class="EnlighterJSRAW" data-enlighter-language="js" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">$('#new-restaurant-form').toggleClass('d-none')</pre>

When the `new.js.erb` action is run, we select the `new-restaurant-form` by id using Jquery and toggle the class to remove display: none. Refresh the page and try to press the add restaurant button. You&#8217;ll see that the form show up and disappears each time you press the button.

However, we want to see the restaurant added to the table.

Let&#8217;s dynamically add a row in our `create.js.erb` file. We&#8217;re calling the `@restaurant` instance variable and grabbing it&#8217;s name and category and inserting those values into the table as a row.

<pre class="EnlighterJSRAW" data-enlighter-language="js" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">$('tbody').after('&lt;tr class="child">&lt;td>&lt;%= j(@restaurant.name) %>&lt;/td>&lt;td>&lt;%= j(@restaurant.category) %>&lt;/td>&lt;/tr>')</pre>

```erb
$('tbody').after('<tr class="child"><td><%= j(@restaurant.name) %></td><td><%= j(@restaurant.category) %></td></tr>')
```



Try to fill out the form now. You&#8217;ll see that the table updates automatically.