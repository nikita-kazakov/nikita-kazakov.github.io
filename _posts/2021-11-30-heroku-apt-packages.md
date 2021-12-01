---
title: How to add apt packages to Heroku
date: 2021-11-30
layout: post
permalink: /heroku-apt-packages
tags:
    - ruby on rails
---

Is there a Linux package that you want to use in Heroku? In my case, I wanted to use [MediaInfo](https://github.com/greatseth/mediainfo) which required an apt package installation. Typically this would be an `apt install mediainfo` command on a Linux machine. But how do you do this in Heroku?

Heroku has a [buildpack library](https://elements.heroku.com/buildpacks) but none of the MediaInfo packages worked for me.

I resorted to using [heroku-buildpack-apt](https://elements.heroku.com/buildpacks/heroku/heroku-buildpack-apt) which let me install ANY apt package on a heroku instance.

Go to Heroku Instance => Settings => Add buildpack.

Add `https://buildpack-registry.s3.amazonaws.com/buildpacks/heroku-community/apt.tgz`

{% include image_center_caption.html
caption = "Add buildpack in heroku"
image = "/assets/images/2021/heroku-apt.png"
%}

In the root folder of your rails project, create a file called `Aptfile`. Put down the names of the apt packages you want to install on each line of that file. For example, let’s say I wanted to install Midnight Commander and MediaInfo. In Linux, I’d run `apt install mc` and `apt install mediainfo`. In the `Aptfile`, I’d put down:

```
# This file is to be used with heroku-buildpack-apt
# It allows you to add custom packages (apt install ...) to a Heroku App.
mc
mediainfo
```

If you have Heroku review apps and you want them to automatically load this buildpack, you can edit the `app.json` file in your Rails project to reflect something like this:

```json
  "environments": {
    "review": {
      "buildpacks": [
        {"url": "heroku-community/apt"},
        {"url": "heroku/nodejs"},
        {"url": "heroku/ruby"}
      ]
    }
  }
```

MediaInfo will automatically get installed each time a new Heroku review app is created.