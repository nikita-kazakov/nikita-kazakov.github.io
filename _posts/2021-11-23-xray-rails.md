---
title: Inspect Element for Rails views with xray-rails
date: 2021-11-23
layout: post
permalink: /xray-rails-gem
tags:
    - ruby on rails
---

All modern browsers have Inspect Element. When I'm working on a Rails page that loads a lot of partials, it's a pain to hunt down where those partials are located. I wish I had Inspect Element for Rails views.

[xray-rails gem](https://github.com/brentd/xray-rails) is the solution.

When I press `cmd + shift + x` on any Rails page in my development environment, it highlights all view partials into clickable boxes.

{% include image_center_caption.html
caption = "Highlights all partials on the page."
image = "/assets/images/2021/xray-rails.png"
%}

When you click on a box, it'll open that partial in your IDE. No more guessing or hunting the partial down through console logs.

To install xray-rails, add this in your `.gemfile`
```ruby
group :development do
  gem 'xray-rails'
end
```

Run `bundle install`.

# Configuration for RubyMine
Inside of RubyMine, go to **Tools > Create Command-line Launcher > Confirm**. Note down the RubyMine path.

Create a config file in your project directory named `.xrayconfig`. Add the script below into the file. If you're using another IDE, just point it to your IDE's path instead.

```
:editor: '/usr/local/bin/mine'
```

You're good to go.