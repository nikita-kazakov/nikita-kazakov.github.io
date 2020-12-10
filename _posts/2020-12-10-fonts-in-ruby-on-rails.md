---
title: Tips on importing fonts in Ruby on Rails
date: 2020-12-10
layout: post
permalink: /importing-fonts-ruby-on-rails/
tags: 
    - ruby on rails
---

I had a problem where fonts were loading fine in development environment but were failing to load in staging / production. 

First tip — put your fonts folder inside of assets to load them with the asset pipeline.

```bash
.
└── app
    └── assets
        ├── fonts
        │   ├── unicons.eot
        │   ├── unicons.svg
        │   ├── unicons.ttf
        │   ├── unicons.woff
        │   └── unicons.woff2
        ├── images
        └── stylesheets
```

When loading fonts from scss, do not use `url`. Instead, use `font_url` to import fonts. Did you know you could also use `image_url` and `asset_url` in scss with your Rails project?

Here’s an example how it would look like:

```scss

@font-face {
  font-family: 'unicons';
  src: font_url('unicons.eot?34404611');
       font_url('unicons.woff2?34404611') format('woff2'),
       font_url('unicons.woff?34404611') format('woff'),
       font_url('unicons.ttf?34404611') format('truetype'),
       font_url('unicons.svg?34404611#unicons') format('svg');
}
```

Fonts should now be loading properly in development and in production environments.