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

When loading fonts from scss, do not use `url`. Instead, use `asset_url` to import fonts.

Here’s an example how it would look like:

```scss

@font-face {
  font-family: 'unicons';
  src: asset_url('unicons.eot?34404611');
  asset_url('unicons.woff2?34404611') format('woff2'),
  asset_url('unicons.woff?34404611') format('woff'),
  asset_url('unicons.ttf?34404611') format('truetype'),
  asset_url('unicons.svg?34404611#unicons') format('svg');
}
```

Fonts should now be loading properly in development and in production environments.