---
title: Extracting video metadata with Ruby and Mediainfo gem.
date: 2021-09-21
layout: post
permalink: /mediainfo-video-metadata
tags: 
    - ruby
---

I had to come up with a way to extract video metadata for work. I found [Mediainfo](https://github.com/greatseth/mediainfo) to be a great fit.

It strips video and audio metadata from a video file. It provides metadata without downloading an entire video.

# Install
Install the [MediaInfo CLI](https://mediaarea.net/en/MediaInfo) first. I used the MacOS in development 
and Ubuntu setup in production.

Let's use Brew to install it on a MacOS in development.

```bash
brew install media-info
```

Add the gem script for [MediaInfo from rubygems.org](https://rubygems.org/gems/mediainfo/versions/1.5.0) to 
your `Gemfile`.

```bash
gem 'mediainfo', '~> 1.5'
```

Run `bundle install` to install. Let's jump into the Rails Console and play around.

```ruby
rails console
# add a video url
url = 'https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-mp4-file.mp4'
metadata = MediaInfo.from(url)
metadata = JSON.parse(metadata.to_json)
```

The metadata will be a Ruby hash.